## Context

The `lpcrmbackend-main` platform is deployed on Vercel Serverless. Vercel imposes strict execution timeouts (10s on Hobby) and immediately terminates background threads upon returning an HTTP response. If we synchronously fetch Graph API details for a batch of Meta Leads, we risk hitting the 10s limit, causing Meta to timeout and potentially disable the webhook. 

To make this production-ready and Serverless-safe, we must decouple the webhook ingestion from the data processing using Upstash QStash. We also need to add marketing tracking fields to the `Lead` model so the team can perform ROI analysis, gracefully handle duplicates by triggering follow-ups instead of throwing DB errors, auto-assign new leads, and add UI filters/exports.

## Goals / Non-Goals

**Goals:**
- Decouple webhook ingestion and processing using Upstash QStash.
- Fetch actual lead details (name, phone, raw form data) securely from Meta Graph API.
- Map dynamic form fields (e.g., `full_name` vs `name`) properly to the `Lead` model.
- Prevent duplicate errors by treating re-inquiring Meta leads as follow-ups on the existing lead.
- Capture campaign and ad details (`campaign_name`, `adset_name`, `ad_name`) in the database.
- Automatically assign Meta leads to relevant counselors.
- Add UI filters to easily sort/filter by Campaign and "Today".
- Add Excel export functionality for these filtered views.

**Non-Goals:**
- Full Meta Ads creation/management from within the CRM (this is read-only).
- WhatsApp automation integration (handled separately).

## Decisions

**Decision 1: Asynchronous Processing via Upstash QStash**
- *Rationale*: We must return a 200 OK to Meta instantly to prevent timeouts. The `/api/meta/webhook/` endpoint will only verify the payload and forward it to QStash. QStash will then securely POST the payload to our `/api/meta/process/` endpoint, where we can safely take several seconds to fetch Graph API data and update NeonDB. If `/process/` fails (e.g. Graph API is down), QStash provides automatic exponential backoff retries.
- *Alternatives*: Synchronous processing (risks Vercel timeouts). Vercel Cron jobs (more complex state management).

**Decision 2: Deduplication via FollowUp Tracking**
- *Rationale*: Instead of rejecting duplicate phone numbers, we catch them via `Lead.objects.filter(phone=normalized_phone).first()`. If found, we append a remark to the lead and generate a high-priority `FollowUp` task for the `current_handler` to call the lead back, indicating they just clicked another ad.
- *Alternatives*: Overwriting lead data or creating a duplicate model.

**Decision 3: Adding Fields directly to `Lead` model**
- *Rationale*: Adding `campaign_name`, `ad_name`, `adset_name`, and `raw_form_data` (JSON) directly to `Lead` is simpler for filtering and querying.
- *Alternatives*: Creating a `MetaLeadDetail` OneToOne relation. Keeping it on the `Lead` model improves query performance and Django Admin usability.

## Risks / Trade-offs

- **Risk**: Unverified requests to the `/process/` endpoint.
  - *Mitigation*: QStash signs all outgoing requests. The `/process/` endpoint will use `Receiver` from `upstash_qstash` to verify the signature, ensuring only QStash can trigger processing.
- **Risk**: Unmapped Form Fields.
  - *Mitigation*: The webhook will use a `FIELD_MAPPING` dictionary, but will also save the *entire* raw Meta payload to `raw_form_data` JSONField.

## Migration Plan

1. Create a Django migration to add marketing fields and `raw_form_data` to `leads.models.Lead`.
2. Add `QSTASH_TOKEN`, `QSTASH_CURRENT_SIGNING_KEY`, and `QSTASH_NEXT_SIGNING_KEY` to Vercel environment variables.
3. Split the webhook logic: update `meta_webhook` to push to QStash, and create `meta_process_webhook` for handling logic.
4. Test with Meta's Webhook Testing Tool and QStash local development flow.
5. Deploy backend updates.

## Open Questions

- What is the specific mapping logic for auto-assignment based on Campaigns? (e.g., "UK Campaign" -> Counselor X).
- Should the Excel Export be generated synchronously, or sent via email asynchronously for large datasets? (Assume synchronous for now).

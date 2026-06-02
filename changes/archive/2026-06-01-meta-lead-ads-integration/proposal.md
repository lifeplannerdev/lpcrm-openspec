## Why

Currently, Meta Lead Ads integrations use a placeholder approach that does not fetch actual lead data, map dynamic forms, or extract marketing campaign insights. Furthermore, because the platform is deployed on Vercel Serverless (which limits executions to 10s and kills background threads), synchronous processing of Graph API requests could cause timeouts and lead to Meta disabling the webhook during high-volume spikes. 

We need a robust, Serverless-friendly architecture using Upstash QStash to decouple the webhook receiver from the Graph API processing. This ensures Meta gets an instant 200 OK, while QStash reliably feeds the leads to our processor with automatic retries. Alongside this, we will implement full Graph API fetching, deduplication without errors, auto-assignment, and advanced filtering for ROI analysis.

## What Changes

- Implement a two-step webhook architecture using Upstash QStash:
  1. A receiver view that validates the Meta payload and pushes it instantly to QStash.
  2. A processor view that securely receives the payload from QStash, fetches Graph API data, maps dynamic fields, and handles deduplication gracefully.
- Add new fields to the `Lead` model (like `campaign_name`, `adset_name`, `ad_name`, `meta_lead_id`, and `raw_form_data`) to capture marketing performance details.
- Handle deduplication cleanly by triggering follow-ups on existing leads instead of throwing IntegrityErrors.
- Connect the flow to the assignment system so Meta leads are routed to correct counselors based on campaign rules or default fallback.
- Auto-schedule follow-up tasks upon Meta Lead creation.
- Ensure the CRM frontend has filters (e.g. by campaign, today's leads) and export options to Excel that respect these filters.

## Capabilities

### New Capabilities
- `meta-lead-qstash-queue`: The reliable queuing mechanism for receiving Meta payloads and decoupling them from processing.
- `meta-lead-ads-webhook`: Fetching and normalizing lead details via Graph API, and capturing campaign and ad metadata.
- `meta-lead-deduplication`: Strategy for handling recurring leads gracefully without DB errors, creating follow-up tasks instead.
- `meta-lead-auto-assignment`: Automatic assignment rules mapping Meta leads to counselors based on campaign or fallback.
- `leads-advanced-filtering-export`: The ability to filter leads (e.g., by Campaign, Today) and export those filtered views to Excel.

### Modified Capabilities
- `lead-management`: Extension of the Lead model to support marketing data, raw form storage, and meta identifiers.

## Impact

- **Code/APIs**: `leads.webhooks`, `leads.models`, `leads.views`. We will add a new `process_webhook` endpoint.
- **Dependencies**: Requires `requests` library and `upstash-qstash` Python SDK.
- **Systems**: Modifies database schema. Requires provisioning a QStash token in Vercel environment variables.

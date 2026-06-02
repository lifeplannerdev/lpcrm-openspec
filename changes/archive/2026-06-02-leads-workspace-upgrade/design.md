## Context

The Leads module is currently functioning as a standard data-entry view. To transition into an enterprise-grade Command Center, we need to unify fragmented history logs (remarks, status updates, follow-ups), automate follow-up escalations to prevent lead leakage, and introduce collaboration features (mentions, attachments). The current codebase has legacy components that need cleanup, and the architecture must remain scalable for advanced future integrations like Voxbay.

## Goals / Non-Goals

**Goals:**
- Unify all lead history into a single, high-performance chronological timeline.
- Automate escalation of overdue follow-ups (notifications and reassignments).
- Enable internal team collaboration directly on the lead via `@mentions` and file attachments.
- Refactor the frontend `LeadDetailPage.jsx` into a clean, optimized Command Center.
- Remove redundant or deprecated frontend code in `src/Components/leads/`.

**Non-Goals:**
- Building a drag-and-drop no-code automation builder (we are using hardcoded logic/cron).
- Integrating WhatsApp or full Email tracking in this phase (those require separate infrastructure projects).

## Decisions

**1. Unified Timeline API Implementation**
- **Decision:** Instead of creating a massive new database table for all events, we will create a `UnifiedTimelineAPIView` that queries `RemarkHistory`, `ProcessingUpdate`, `FollowUpHistory`, and `WebhookLog` separately, standardizes their output into a unified JSON schema, and sorts them by timestamp in memory (using Python's `itertools` or Django's `union` if models align).
- **Rationale:** Prevents massive data migrations. Keeps domain models clean while delivering the UX of a single feed.

**2. Follow-Up Escalation System**
- **Decision:** Implement a Django Management Command (`escalate_followups.py`) that can be scheduled via Celery Beat or cron. It will query `FollowUp` models where `status != 'Completed'` and `follow_up_time < now()`.
- **Rationale:** Reliable, background-processed, and doesn't slow down HTTP requests.

**3. Mention System (`@username`)**
- **Decision:** Use Django signals (`pre_save` or `post_save`) on `RemarkHistory`. Regex parses `@username`, queries the User model, and creates a `Notification` object.
- **Rationale:** Decouples mention logic from the views. Ensures mentions work regardless of where the remark is created (API, bulk upload, or UI).

**4. File Attachments**
- **Decision:** New `LeadDocument` model with a `models.FileField`. Frontend uses standard multipart form data.
- **Rationale:** Simplest and most standard Django pattern.

## Risks / Trade-offs

- **Risk (Performance):** Querying 4 different tables for the Unified Timeline could be slow for leads with massive histories.
  - *Mitigation:* Implement server-side pagination for the timeline API. Only fetch the last 20 events by default.
- **Risk (Mention Parsing):** Users with spaces in usernames or typos.
  - *Mitigation:* The frontend will provide an auto-complete dropdown for mentions, ensuring the exact `@username` is sent to the backend.

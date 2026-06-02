## 1. Database and Models

- [x] 1.1 Update `Lead` model in `leads/models.py` to add `campaign_name` (CharField), `adset_name` (CharField), `ad_name` (CharField), `meta_lead_id` (CharField), and `raw_form_data` (JSONField).
- [x] 1.2 Generate and apply database migrations for the new `Lead` model fields.

## 2. QStash and Webhook Architecture

- [x] 2.1 Add `upstash-qstash` to `requirements.txt`.
- [x] 2.2 Refactor `meta_webhook` in `leads/webhooks.py` to act ONLY as a receiver: it logs the payload to `WebhookLog` and pushes the data to Upstash QStash, returning `200 OK` immediately.
- [x] 2.3 Create a new view `meta_process_webhook` in `leads/webhooks.py` that handles requests from QStash, using `Receiver.verify` to validate the Upstash signature.
- [x] 2.4 Update `leads/urls.py` to route to the new `/api/meta/process/` endpoint.

## 3. Data Processing and Deduplication (Inside `meta_process_webhook`)

- [x] 3.1 Implement secure Graph API fetching using the Meta Long-Lived Access Token to retrieve actual lead data.
- [x] 3.2 Add dynamic field normalization to map common Meta form fields (e.g., `full_name` to `name`, `whatsapp_number` to `phone`).
- [x] 3.3 Implement the logic to extract and store the marketing campaign details onto the Lead.
- [x] 3.4 Implement deduplication logic: Catch existing phone numbers with `Lead.objects.filter(phone=...)`, update remarks, and skip `Lead.objects.create`.

## 4. Auto-Assignment and Follow-Up

- [x] 4.1 Implement a `FollowUp` task creation for deduplicated leads so the current handler is notified of a re-inquiry.
- [x] 4.2 Implement auto-assignment rules for new leads based on Campaign Name (or fallback to an Admin).
- [x] 4.3 Ensure a standard "Call" `FollowUp` task is generated for the new assignee upon creation of a new Meta Lead.

## 5. Frontend / Views Integration (Filtering & Export)

- [x] 5.1 Update the backend List/Filter views (e.g., Django Admin or API views) to allow filtering by `campaign_name` and "Created Today".
- [x] 5.2 Implement an Excel Export endpoint/action that takes the currently applied filters and returns a downloadable `.xlsx` file.
- [x] 5.3 Add UI buttons for "Export Excel" and the new filters on the frontend/admin interface.

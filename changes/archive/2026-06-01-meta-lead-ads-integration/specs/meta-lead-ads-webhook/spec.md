## ADDED Requirements

### Requirement: Fetch Lead Details via Graph API
The system SHALL intercept incoming Meta Lead Ad webhook POST requests, extract the `leadgen_id`, and fetch the full lead details using the Meta Graph API.

#### Scenario: Successful API Fetch
- **WHEN** a webhook with a valid `leadgen_id` is received
- **THEN** the system fetches the lead data and extracts name, phone, and form fields
- **THEN** the system logs the successful fetch

### Requirement: Dynamic Field Normalization
The system MUST dynamically map incoming Meta fields (like `full_name`, `student_name`) to the CRM's standard `name` and `phone` fields, while preserving all original data.

#### Scenario: Normalizing unusual field names
- **WHEN** the Meta form provides data as `first_name` and `whatsapp_number`
- **THEN** the system maps these to `name` and `phone` respectively
- **THEN** the system stores the entire unmapped JSON payload in `raw_form_data`

### Requirement: Marketing Campaign Tracking
The system SHALL capture and store marketing attributes (campaign, adset, ad) for every new Meta Lead.

#### Scenario: Storing Ad Context
- **WHEN** the webhook payload includes campaign and ad IDs
- **THEN** the system extracts `campaign_name`, `adset_name`, and `ad_name` and saves them on the Lead model

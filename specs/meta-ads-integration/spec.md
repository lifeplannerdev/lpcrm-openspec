## Purpose
Defines the capabilities for securely ingesting, queuing, fetching, and normalizing lead data directly from Meta (Facebook/Instagram) Lead Ads webhooks, including auto-assignment and deduplication logic.

## Requirements

### Requirement: Meta Ads Webhook Ingestion
The system SHALL provide a webhook endpoint to receive lead data directly from Facebook/Instagram Lead Ads.

#### Scenario: Valid lead ingested
- **WHEN** Meta sends a valid POST request with a hub signature
- **THEN** the system validates the signature and creates a new Lead record in the CRM

#### Scenario: Signature validation fails
- **WHEN** Meta sends a POST request with an invalid signature
- **THEN** the system rejects the payload and logs an error

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

### Requirement: Meta Lead Auto-Assignment
The system SHALL automatically assign incoming Meta Leads to a designated counselor or manager.

#### Scenario: Assigning based on campaign rules
- **WHEN** a Meta Lead is created and the `campaign_name` matches a predefined assignment rule
- **THEN** the system assigns the lead to the specified user
- **THEN** the system schedules a standard FollowUp task for that assignee

#### Scenario: Fallback assignment
- **WHEN** a Meta Lead is created but no specific campaign rule matches
- **THEN** the system assigns the lead to a default fallback user (e.g. an Admin)

### Requirement: Graceful Lead Deduplication
The system MUST NOT throw database integrity errors when a Meta Lead is submitted with a phone number that already exists in the CRM.

#### Scenario: Processing a duplicate Meta Lead
- **WHEN** a Meta Lead form is submitted with a `phone` matching an existing Lead
- **THEN** the system prevents a duplicate Lead record from being created
- **THEN** the system appends a note to the existing Lead's `remarks` indicating the new ad interaction
- **THEN** the system creates a high-priority "Call" `FollowUp` task assigned to the lead's current handler

### Requirement: QStash Message Queue Integration
The system SHALL use Upstash QStash to queue incoming Meta Lead webhook payloads to decouple receiving from processing.

#### Scenario: Enqueuing a Meta Webhook
- **WHEN** the `meta_webhook` endpoint receives a valid POST request from Meta
- **THEN** it pushes the payload to QStash
- **THEN** it immediately returns a `200 OK` response to Meta

### Requirement: Secure Processing Endpoint
The system SHALL process QStash messages securely to prevent unauthorized triggering.

#### Scenario: Processing a queued payload
- **WHEN** the `/api/meta/process/` endpoint is called by QStash
- **THEN** it verifies the request signature using QStash keys
- **THEN** it executes the Graph API fetch and CRM lead creation logic
- **THEN** it returns a `200 OK` or fails to allow QStash to retry

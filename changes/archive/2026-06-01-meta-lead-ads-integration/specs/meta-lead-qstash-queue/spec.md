## ADDED Requirements

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

## ADDED Requirements

### Requirement: Voxbay Webhook Ingestion
The system SHALL provide a webhook endpoint to receive call logs from Voxbay.

#### Scenario: Call logged successfully
- **WHEN** Voxbay sends a valid POST request with call details
- **THEN** the system stores the call log securely

### Requirement: 1-Click Lead Conversion
The system SHALL allow converting an unknown caller from the Voxbay logs into a Lead.

#### Scenario: Unknown caller converted
- **WHEN** a user clicks "Convert to Lead" on an unknown call log
- **THEN** the system redirects to the Lead creation form pre-filled with the caller's phone number

### Requirement: Auto-Queue Follow-ups
The system SHALL automatically create a follow-up task when a call occurs.

#### Scenario: Call triggers follow-up
- **WHEN** a call log is ingested for an existing Lead
- **THEN** the system schedules a follow-up task for the next business day

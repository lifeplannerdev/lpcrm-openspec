## ADDED Requirements

### Requirement: Graceful Lead Deduplication
The system MUST NOT throw database integrity errors when a Meta Lead is submitted with a phone number that already exists in the CRM.

#### Scenario: Processing a duplicate Meta Lead
- **WHEN** a Meta Lead form is submitted with a `phone` matching an existing Lead
- **THEN** the system prevents a duplicate Lead record from being created
- **THEN** the system appends a note to the existing Lead's `remarks` indicating the new ad interaction
- **THEN** the system creates a high-priority "Call" `FollowUp` task assigned to the lead's current handler

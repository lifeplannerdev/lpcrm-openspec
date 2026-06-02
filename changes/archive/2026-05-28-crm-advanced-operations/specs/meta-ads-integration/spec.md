## ADDED Requirements

### Requirement: Meta Ads Webhook Ingestion
The system SHALL provide a webhook endpoint to receive lead data directly from Facebook/Instagram Lead Ads.

#### Scenario: Valid lead ingested
- **WHEN** Meta sends a valid POST request with a hub signature
- **THEN** the system validates the signature and creates a new Lead record in the CRM

#### Scenario: Signature validation fails
- **WHEN** Meta sends a POST request with an invalid signature
- **THEN** the system rejects the payload and logs an error

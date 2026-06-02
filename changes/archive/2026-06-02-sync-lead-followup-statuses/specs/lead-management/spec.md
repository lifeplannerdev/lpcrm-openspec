## ADDED Requirements

### Requirement: Contacted Status Support
The system SHALL support `CONTACTED` as an official status for Leads.

#### Scenario: Validating lead statuses
- **WHEN** a lead is updated via the backend
- **THEN** it SHALL be allowed to be set to the `CONTACTED` status
- **AND** frontend components like Customer Journey SHALL recognize this as the completed "Contacted" milestone

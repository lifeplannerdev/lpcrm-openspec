## ADDED Requirements

### Requirement: FollowUp Status Automation
The system SHALL automatically sync specific FollowUp statuses to the parent Lead.

#### Scenario: Marking a FollowUp as Contacted
- **WHEN** a FollowUp status is updated to `contacted`
- **AND** the parent Lead is in the `ENQUIRY` status
- **THEN** the parent Lead's status SHALL be automatically updated to `CONTACTED`

#### Scenario: Marking a FollowUp as Not Interested
- **WHEN** a FollowUp status is updated to `not_interested`
- **AND** the parent Lead is in the `ENQUIRY` status
- **THEN** the parent Lead's status SHALL be automatically updated to `NOT_INTERESTED`

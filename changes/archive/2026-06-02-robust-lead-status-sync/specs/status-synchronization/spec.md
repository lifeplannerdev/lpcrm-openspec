## MODIFIED Requirements

### Requirement: FollowUp Status Automation
The system SHALL automatically sync specific FollowUp statuses to the parent Lead, including recalculating the Lead status when FollowUps are deleted or reverted.

#### Scenario: Marking a FollowUp as Contacted
- **WHEN** a FollowUp status is updated to `contacted`
- **AND** the parent Lead is in the `ENQUIRY` status
- **THEN** the parent Lead's status SHALL be automatically updated to `CONTACTED`

#### Scenario: Marking a FollowUp as Not Interested
- **WHEN** a FollowUp status is updated to `not_interested`
- **AND** the parent Lead is in the `ENQUIRY` status
- **THEN** the parent Lead's status SHALL be automatically updated to `NOT_INTERESTED`

#### Scenario: Deleting the last Contacted FollowUp
- **WHEN** a FollowUp is deleted or its status is reverted from `contacted`
- **AND** it was the only FollowUp keeping the Lead in `CONTACTED` status
- **THEN** the Lead's status SHALL automatically revert to `ENQUIRY`

#### Scenario: Preserving advanced Lead statuses
- **WHEN** a FollowUp is deleted or its status is reverted
- **AND** the Lead has already advanced to `QUALIFIED`, `CONVERTED`, or another advanced state
- **THEN** the Lead's status SHALL NOT be downgraded

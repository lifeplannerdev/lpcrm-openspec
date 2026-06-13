## ADDED Requirements

### Requirement: Staff On Leave Status
The system SHALL support tracking and filtering staff members who are on leave.

#### Scenario: Filtering by On Leave Status
- **WHEN** an admin selects the "On Leave" tab on the Staff Management page
- **THEN** the system fetches and displays only staff members who have their on-leave status set to true

#### Scenario: Staff Statistics Include On Leave Count
- **WHEN** the Staff Management page loads
- **THEN** the statistics cards display the correct count of staff members who are on leave

## ADDED Requirements

### Requirement: Report Submission Timeouts
The system SHALL flag daily reports that violate timeout constraints (Morning agenda after 10:30 AM, Evening report after 6:00 PM).

#### Scenario: Late morning agenda is flagged
- **WHEN** a user submits a Morning Agenda at 10:45 AM
- **THEN** the report is visually flagged as "Late" in the reports list

#### Scenario: User filters by pending/timeout reports
- **WHEN** a manager clicks the "Pending/Timeout" filter
- **THEN** the grid displays all users who missed the reporting deadline for the current day

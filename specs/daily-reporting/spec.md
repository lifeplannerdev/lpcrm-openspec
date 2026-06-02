# daily-reporting Specification

## Purpose
TBD - created by archiving change crm-production-enhancements. Update Purpose after archive.
## Requirements
### Requirement: Morning and Evening Reports
The system SHALL support creating distinct Morning Agenda and Evening Report entries, capturing the exact submission timestamp.

#### Scenario: Submitting a morning agenda
- **WHEN** user submits a Morning Agenda
- **THEN** system saves the agenda with the current server timestamp to enable late-entry flagging

### Requirement: Next Day's Agenda Carry-Over
The system SHALL support an optional Next Day's Agenda field that pre-fills the following day's Morning Agenda.

#### Scenario: Carrying over agenda
- **WHEN** user fills Next Day's Agenda on Monday evening
- **THEN** system automatically populates Tuesday's Morning Agenda with this content

### Requirement: Report Submission Timeouts
The system SHALL flag daily reports that violate timeout constraints (Morning agenda after 10:30 AM, Evening report after 6:00 PM).

#### Scenario: Late morning agenda is flagged
- **WHEN** a user submits a Morning Agenda at 10:45 AM
- **THEN** the report is visually flagged as "Late" in the reports list

#### Scenario: User filters by pending/timeout reports
- **WHEN** a manager clicks the "Pending/Timeout" filter
- **THEN** the grid displays all users who missed the reporting deadline for the current day


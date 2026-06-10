## MODIFIED Requirements

### Requirement: Daily Reporting System
The system SHALL provide a Daily Reporting feature allowing employees to submit daily status updates (Morning Agenda and Evening Report) and review their past reports.
The system SHALL track completion as a 2-step process per day (50% for Agenda, 100% for Report).
The system SHALL support auto-carryover of agendas: if an employee submits "Next Day's Agenda", the system SHALL automatically populate the "Morning Agenda" for the following day.

#### Scenario: Employee submits a report
- **WHEN** an employee fills out the Daily Report form and submits it
- **THEN** the report is saved as "pending" for manager review

#### Scenario: Agenda Auto-Carryover
- **WHEN** an employee submits the "Next Day's Agenda" field on Monday evening
- **THEN** their Tuesday report is automatically initialized with the "Morning Agenda" field populated, marking that step as complete.

## ADDED Requirements

### Requirement: Policy-Driven Report Timelines
The system SHALL allow administrators to configure specific Report and Agenda deadlines per employee, along with the policy for *when* the Agenda is due (e.g., `EVENING_BEFORE` or `MORNING_OF`).

#### Scenario: Admin configures employee timeline
- **WHEN** an admin sets User A's agenda policy to `MORNING_OF` with a deadline of 10:00 AM
- **THEN** the system expects User A to submit their Morning Agenda on the current day before 10:00 AM.

### Requirement: Granular Lateness Tracking and Filtering
The system SHALL track exact submission timestamps for both the Agenda and the Report independently.
The system SHALL calculate lateness flags (`Late Agenda`, `Late Report`, `On-Time`, `Incomplete`) by comparing the independent submission timestamps against the employee's configured deadlines.

#### Scenario: Late Agenda submission
- **WHEN** an employee submits their Morning Agenda after their configured deadline
- **THEN** the system applies a `Late Agenda` flag to that day's report, even if they submit their Evening Report on time.

#### Scenario: Filtering by granular flags
- **WHEN** an HR user views the Admin Reports page and filters by `Late Agenda`
- **THEN** the frontend requests and displays only reports where the `Late Agenda` flag is active.

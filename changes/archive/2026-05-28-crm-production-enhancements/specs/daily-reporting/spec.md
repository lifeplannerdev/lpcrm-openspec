## ADDED Requirements

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

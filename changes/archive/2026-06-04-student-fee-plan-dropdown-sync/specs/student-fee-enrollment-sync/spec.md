## ADDED Requirements

### Requirement: Student Enrollment and Fee Linkage
The system MUST keep the academic student record and the linked fee account synchronized so both sides reflect the same enrollment state.

#### Scenario: New student enrollment awaits fee setup
- **WHEN** a student is created without an assigned fee plan
- **THEN** the system SHALL mark the student as pending fee setup and expose that state in both academic and accounting views

#### Scenario: Fee account creation updates the student record
- **WHEN** accounting creates a fee account for an enrolled student
- **THEN** the system SHALL link the fee account to the student and show the active fee plan on the student detail screen

### Requirement: Shared Fee State Across Views
The system MUST present the same fee status, balance, and plan summary in the student workspace, trainer view, and accounting workspace.

#### Scenario: Student detail shows the current fee summary
- **WHEN** an authorized user opens a student detail page
- **THEN** the system SHALL display the current fee plan, total due, paid amount, balance due, and overdue amount from the backend source of truth

#### Scenario: Updates reflect in all linked screens
- **WHEN** accounting records a payment or restructures a fee plan
- **THEN** the system SHALL refresh the student-facing and accounting-facing fee summaries so they match the updated ledger

### Requirement: Fee Event Notifications
The system MUST notify the relevant personnel when a student fee state changes in a way that affects onboarding or collections.

#### Scenario: Accounting receives enrollment notification
- **WHEN** a student enrollment is created and the fee plan is still pending
- **THEN** the system SHALL notify accounting that a fee plan must be assigned

#### Scenario: Trainers receive fee-status awareness
- **WHEN** a student fee account becomes overdue, restructured, or settled
- **THEN** the system SHALL make the updated fee state visible to trainers who can view the student

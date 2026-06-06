## MODIFIED Requirements

### Requirement: Advanced Attendance Filtering
The system SHALL provide filters by trainer, location, student status, permission scope, and fee status, and it SHALL exclude dropped or completed students from the attendance marking view.

#### Scenario: Filtering active students for a trainer
- **WHEN** user selects a trainer and location
- **THEN** system lists only the active students that match the criteria and that the user is allowed to see

#### Scenario: Excluding inactive students
- **WHEN** a trainer opens the attendance workspace
- **THEN** the system omits students whose status is Dropped or Completed from the marking list

#### Scenario: Fee-aware attendance warning
- **WHEN** an authorized user opens attendance for a student with an overdue fee account
- **THEN** the system displays the fee status warning without blocking access unless a separate policy says to block it

### Requirement: Toggle-based Attendance
The system SHALL allow authorized users to mark all listed students present or absent with a single toggle action, and trainers SHALL only mark attendance for their assigned students.

#### Scenario: Toggling all present
- **WHEN** user clicks "Mark All Present" toggle
- **THEN** system updates the status of all visible students to present

#### Scenario: Trainer marks a student not assigned to them
- **WHEN** a trainer attempts to mark attendance for a student outside their assignment
- **THEN** the system rejects the change and keeps the record unchanged

### Requirement: Permission-Based Attendance Editing
The system SHALL hide attendance edit actions from users who only have read-only attendance access.

#### Scenario: Read-only user opens attendance
- **WHEN** a user with view-only attendance access opens the attendance page
- **THEN** the system shows attendance history but disables or hides marking controls

### Requirement: Attendance and Fee Policy Hooks
The system SHALL allow attendance policy to react to fee states such as overdue, partially paid, or restructured accounts.

#### Scenario: Policy marks a student for review
- **WHEN** a student has an overdue or restructured fee account
- **THEN** the system can flag the student for review in the attendance workflow without breaking the attendance list

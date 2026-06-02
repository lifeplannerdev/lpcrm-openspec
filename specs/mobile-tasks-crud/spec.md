## ADDED Requirements

### Requirement: Task Creation Form
The system SHALL provide a form to create a new Task.
- The form MUST include fields for Title, Description, Priority, Deadline, and Assigned Staff.
- The form MUST only be accessible to users with the `edit_tasks` permission.

#### Scenario: Authorized user creates a task
- **GIVEN** a user has `edit_tasks` permission
- **WHEN** they tap the Create Task FAB on the Tasks list
- **THEN** they are presented with the Task Creation form
- **WHEN** they submit valid details
- **THEN** the task is created on the backend and they are returned to the Tasks list

### Requirement: Task Details and Status Update
The system SHALL allow users to view detailed information about a task and update its status.

#### Scenario: User updates a task status
- **WHEN** a user taps a task in the list
- **THEN** they are navigated to the Task Details screen
- **WHEN** they change the status dropdown from PENDING to COMPLETED
- **THEN** the backend is updated and the list reflects the new status

## MODIFIED Requirements

### Requirement: Personal Tasks View
The system SHALL provide a dedicated "My Tasks" page to display tasks assigned to the currently logged-in user. The UI SHALL NOT rely on the legacy `role` field to conditionally render components like the "Create Task" button, but rather check if the user's `db_roles` (or `role_names`) intersect with `TASK_ASSIGNERS`.

#### Scenario: Navigating to My Tasks
- **WHEN** the authenticated user clicks the "My Tasks" navigation link or visits `/mytasks`
- **THEN** they see a dedicated page displaying only their assigned tasks.

#### Scenario: Task Assigner viewing My Tasks
- **WHEN** a user who has an assigning role in `db_roles` views My Tasks
- **THEN** the system displays the "Create Task" or "Assign Task" capabilities.

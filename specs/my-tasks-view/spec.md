# my-tasks-view Specification

## Purpose
TBD - created by archiving change add-my-tasks-page. Update Purpose after archive.
## Requirements
### Requirement: Personal Tasks View
The system SHALL provide a dedicated "My Tasks" page to display tasks assigned to the currently logged-in user.

#### Scenario: Navigating to My Tasks
- **WHEN** the authenticated user clicks the "My Tasks" navigation link or visits `/mytasks`
- **THEN** they see a dedicated page displaying only their assigned tasks.

### Requirement: Task Filtering by User ID
The frontend SHALL pass the current user's identifier when fetching tasks for the My Tasks page to ensure data isolation from other users' tasks.

#### Scenario: API Request
- **WHEN** the My Tasks page mounts
- **THEN** it sends a request to the backend task endpoint, explicitly querying for tasks assigned to the current user (e.g. `?user=<user_id>`).


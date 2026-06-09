## Purpose
Defines the capabilities and requirements for Task Management, including UI views (Kanban, My Tasks), filtering, company segregation, and asynchronous task processing.

## Requirements

### Requirement: Task Kanban Interface
The system SHALL display tasks in a drag-and-drop Kanban board layout.

#### Scenario: Dragging a task to a new status
- **WHEN** user drags a task card from one column to another
- **THEN** system updates the task's status based on the destination column

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

### Requirement: Advanced Multi-Date Filtering for Tasks
The system SHALL support filtering tasks by multiple dynamic date ranges simultaneously (e.g. Today, Yesterday, Specific Date) as well as Month and Year dropdowns.

#### Scenario: User filters by Today
- **WHEN** a user clicks the "Today" filter on the Kanban board
- **THEN** the board only displays tasks due today

#### Scenario: Filter tasks by specific month and year
- **WHEN** user selects a specific month (e.g., "February") and year (e.g., "2024")
- **THEN** the task list and task statistics reflect only tasks whose creation or deadline falls within that specific month and year

### Requirement: Backend Task Time Filtering
The backend API (`/api/tasks/` and `/api/tasks/stats/`) SHALL accept `date_filter`, `month`, and `year` query parameters to filter tasks.

#### Scenario: Fetch filtered tasks
- **WHEN** a GET request is sent to `/api/tasks/` with `month=2` and `year=2024`
- **THEN** the API returns tasks matching February 2024.

### Requirement: Task Company Assignment
The Task Kanban system SHALL segregate tasks by company and respect the per-page company switcher.

#### Scenario: Admin with dual access creates task
- **WHEN** user with both `access_lp` and `access_flag` creates a Task
- **THEN** a dropdown field for "Company" (`LP` or `FLAG`) is displayed, and the Assignee dropdown only shows staff members from that selected company

#### Scenario: Viewing Task Kanban
- **WHEN** viewing the Task Kanban board
- **THEN** the board only fetches and displays tasks belonging to the company selected in the page's Company Switcher

### Requirement: Centralized Task Registration
The system SHALL enforce a standardized convention where all asynchronous tasks and scheduled automations are defined in `tasks.py` modules within their respective Django apps.

#### Scenario: Adding a new background task
- **WHEN** a developer creates a new automation for the `leads` app
- **THEN** the task is defined in `leads/tasks.py` using the `@shared_task` decorator

### Requirement: Asynchronous Execution Priority
The system SHALL process critical webhooks (like incoming Leads) asynchronously to immediately return a 200 OK response to the caller, preventing timeouts.

#### Scenario: Processing an external webhook
- **WHEN** a Meta Lead Ad webhook is received
- **THEN** the system pushes the payload to the Celery broker, returns 200 OK, and processes the lead creation asynchronously

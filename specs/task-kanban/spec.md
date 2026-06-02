# task-kanban Specification

## Purpose
TBD - created by archiving change crm-production-enhancements. Update Purpose after archive.
## Requirements
### Requirement: Task Kanban Interface
The system SHALL display tasks in a drag-and-drop Kanban board layout.

#### Scenario: Dragging a task to a new status
- **WHEN** user drags a task card from one column to another
- **THEN** system updates the task's status based on the destination column

### Requirement: Advanced Multi-Date Filtering for Tasks
The system SHALL support filtering tasks by multiple dynamic date ranges simultaneously (e.g. Today, Yesterday, Specific Date).

#### Scenario: User filters by Today
- **WHEN** a user clicks the "Today" filter on the Kanban board
- **THEN** the board only displays tasks due today

#### Scenario: User filters by Specific Date
- **WHEN** a user selects a specific date from a date picker on the Kanban board
- **THEN** the board only displays tasks due on that specific date

### Requirement: Task Company Assignment
The Task Kanban system SHALL segregate tasks by company and respect the per-page company switcher.

#### Scenario: Admin with dual access creates task
- **WHEN** user with both `access_lp` and `access_flag` creates a Task
- **THEN** a dropdown field for "Company" (`LP` or `FLAG`) is displayed, and the Assignee dropdown only shows staff members from that selected company

#### Scenario: Viewing Task Kanban
- **WHEN** viewing the Task Kanban board
- **THEN** the board only fetches and displays tasks belonging to the company selected in the page's Company Switcher


## ADDED Requirements

### Requirement: Task Company Assignment
The Task Kanban system SHALL segregate tasks by company and respect the per-page company switcher.

#### Scenario: Admin with dual access creates task
- **WHEN** user with both `access_lp` and `access_flag` creates a Task
- **THEN** a dropdown field for "Company" (`LP` or `FLAG`) is displayed, and the Assignee dropdown only shows staff members from that selected company

#### Scenario: Viewing Task Kanban
- **WHEN** viewing the Task Kanban board
- **THEN** the board only fetches and displays tasks belonging to the company selected in the page's Company Switcher

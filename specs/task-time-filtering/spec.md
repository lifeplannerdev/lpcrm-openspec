# task-time-filtering Specification

## Purpose
TBD - created by archiving change task-year-month-filter. Update Purpose after archive.
## Requirements
### Requirement: Month and Year Filters
The system SHALL provide explicit month and year dropdown filters on the Tasks Management page.

#### Scenario: Filter tasks by specific month and year
- **WHEN** user selects a specific month (e.g., "February") and year (e.g., "2024")
- **THEN** the task list and task statistics reflect only tasks whose creation or deadline falls within that specific month and year

### Requirement: Backend Task Time Filtering
The backend API (`/api/tasks/` and `/api/tasks/stats/`) SHALL accept `month` and `year` query parameters to filter tasks.

#### Scenario: Fetch filtered tasks
- **WHEN** a GET request is sent to `/api/tasks/` with `month=2` and `year=2024`
- **THEN** the API returns tasks matching February 2024.


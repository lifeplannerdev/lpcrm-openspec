## Why

Users currently lack the ability to filter tasks by specific months and years. In order to review historical tasks or plan for specific periods, an explicit month and year filter is necessary on the Tasks Management page.

## What Changes

- Add a "Month" dropdown filter (e.g., January, February, etc.) to the `Tasks Management` page.
- Add a "Year" dropdown filter (e.g., 2024, 2025, 2026) to the `Tasks Management` page.
- Update the `TaskListCreateAPIView` and `TaskStatsAPIView` in the backend to accept and process `month` and `year` query parameters to filter tasks by their `created_at` or `deadline` date (likely `deadline` or `created_at`, to be defined in design).
- Ensure the frontend passes these new filter states to the API requests.

## Capabilities

### New Capabilities
- `task-time-filtering`: Add explicit month and year filtering to task lists and statistics.

### Modified Capabilities
- None

## Impact

- Frontend: `TasksPage.jsx` (or equivalent tasks management page) will have new filter dropdowns.
- Backend: `tasks/views.py` will have updated `get_queryset` logic for task filtering and stats.
- No database schema migrations are required since the data already has timestamps.

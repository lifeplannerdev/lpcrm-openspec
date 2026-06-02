## Context

Currently, the Tasks Management page provides filters for status and priority, but lacks explicit date filters for month and year. A simple date picker exists for a specific day, but to view historical tasks for a specific month/year, explicit dropdowns are needed.

## Goals / Non-Goals

**Goals:**
- Add Month and Year dropdowns to the Tasks Management frontend (`TasksPage.jsx`).
- Update `tasks/views.py` (`TaskListCreateAPIView`, `TaskStatsAPIView`) to filter by `month` and `year`.

**Non-Goals:**
- Adding a full calendar date-range picker.

## Decisions

- **Filter Field**: We will filter based on `created_at` (month and year) for tasks to align with how reporting usually works.
- **Backend Implementation**: Use Django's `__year` and `__month` lookups on `created_at` in the `get_queryset` method.
- **Frontend Implementation**: Use standard HTML `<select>` elements styled with the existing Tailwind classes.

## Risks / Trade-offs

- **Risk**: Performance hit on large tables when filtering by `__month` and `__year`.
  - **Mitigation**: Add a database index on `created_at` if performance becomes an issue (currently not needed for the expected scale).

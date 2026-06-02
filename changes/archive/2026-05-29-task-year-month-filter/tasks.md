## 1. Backend Updates

- [x] 1.1 Update `TaskListCreateAPIView` in `tasks/views.py` to accept `month` and `year` query params and filter `created_at__month` and `created_at__year`.
- [x] 1.2 Update `TaskStatsAPIView` in `tasks/views.py` to accept and apply the same `month` and `year` filters.

## 2. Frontend Updates

- [x] 2.1 Add `selectedMonth` and `selectedYear` state variables to `Tasks Management` page.
- [x] 2.2 Add Month and Year dropdown UI components to the filter bar.
- [x] 2.3 Update API fetch calls for tasks and stats to pass the new `month` and `year` parameters.

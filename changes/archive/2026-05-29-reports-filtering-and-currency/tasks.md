## 1. Backend Updates

- [x] 1.1 Update `AllDailyReportsView` and `AdminReportStatsView` in `reports/views.py` to accept `employee_id`, `status`, `date_filter`, and `search` query parameters.
- [x] 1.2 Implement `.filter()` chains to accurately parse and combine these filters simultaneously (AND logic).

## 2. Frontend Report Filters

- [x] 2.1 Update `ReportsPage.jsx` and `StaffReportsPage.jsx` (and any related components) to include `selectedEmployee`, `selectedDate`, `selectedStatus`, and `searchTerm` state variables.
- [x] 2.2 Add UI components for these filters to the page header or filter bar.
- [x] 2.3 Fetch the list of active employees from the backend and populate the Employee dropdown.
- [x] 2.4 Update API fetch calls for the reports to pass the active query parameters to the backend endpoints.

## 3. Currency Symbol Update

- [x] 3.1 Locate the rendering of penalty amounts in `PenaltyManagementPage.jsx`.
- [x] 3.2 Replace all occurrences of `$` with `₹` in the frontend formatting logic.

## 4. Fixes Based on Feedback

- [x] 4.1 Update `ReportsPage.jsx` to fetch employees from `/staffs/` instead of `/accounts/staff/`.
- [x] 4.2 Update `ReportsPage.jsx` date filter to use an `<input type="date">` for selecting specific dates.
- [x] 4.3 Initialize `companyFilter` state to `user?.company || 'LP'` in `ReportsPage.jsx` and `PenaltyManagementPage.jsx` to apply correct default company filter.
## Why

To enhance the tracking and monitoring of reports, the HR department and management need robust filtering mechanisms on the Reports page. This allows users to easily query pending or successful reports submitted today by specific employees. Additionally, the penalty section currently displays the incorrect currency symbol ($) and needs to be updated to the Indian Rupee (₹).

## What Changes

- Add multiple active filtering options to the `Reports` sections (Staff Reports / All Reports).
- Include an `Employee` filter dropdown to review reports on an individual employee basis.
- Include a `Date` filter (e.g., Today) and `Status` filter (e.g., Pending, Successful).
- Add a text-based search option for reports.
- Ensure all filters can be applied simultaneously on the backend.
- Update the currency symbol in the `Penalty` section from `$` to `₹`.

## Capabilities

### New Capabilities
- `reports-advanced-filtering`: Detailed filtering options for reports (by employee, date, status, search keyword).

### Modified Capabilities
- NoneGEINBYHBYHBYBHBNHN


## Impact

- Frontend: `ReportsPage.jsx` and `StaffReportsPage.jsx` (or equivalent components) will require new filter bar UI components. `PenaltyManagementPage.jsx` will have its text updated.
- Backend: `reports/views.py` will require updated `get_queryset` filtering logic for the list endpoints to accept and parse multiple query parameters (employee ID, status, date range).

## Context

Currently, the Reports pages (`My Reports`, `Staff Reports`, `All Reports`) may have limited or basic filtering options. The HR department requires a robust filtering engine to quickly aggregate reports for daily reviews (e.g., all pending reports submitted by specific employees today). The penalty section also uses the `$` symbol which is incorrect for the local currency (`₹`).

## Goals / Non-Goals

**Goals:**
- Implement a composite filtering system for Daily Reports that processes:
  - Employee ID (Select dropdown of staff)
  - Date / Date Range (e.g., Today, Yesterday, Custom)
  - Status (Pending, Completed, etc.)
  - Search keyword (text matching on agenda, etc.)
- Update the frontend filter bar to include these inputs seamlessly.
- Replace `$` with `₹` globally in the Penalty UI.

**Non-Goals:**
- Complete overhaul of the report data model.

## Decisions

- **Filtering Logic**: The Django Rest Framework `ListAPIView` (e.g., `AllDailyReportsView`, `AdminReportStatsView`) will parse query params (`employee_id`, `status`, `date_filter`, `search`) and apply chained `.filter()` operations on the QuerySet. This ensures all active filters act as an `AND` query.
- **Frontend Employee List**: To populate the Employee filter dropdown, the Reports page will fetch the list of active employees from the existing `/api/staff/` endpoint (or a similar employee list API).
- **Currency Update**: Direct text replacement in the React components rendering the Penalty amounts.

## Risks / Trade-offs

- **Risk**: Fetching the full list of employees for the dropdown might be slow on large databases.
  - **Mitigation**: Use a lightweight endpoint or the existing staff list context if available. Only fetch active employees.

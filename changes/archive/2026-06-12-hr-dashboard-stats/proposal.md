## Why

HR users currently receive a "Failed to load dashboard statistics" error because the dashboard strictly requires the `ADMIN` role to load the stats API, despite the frontend allowing access to anyone with `staff:view_any` permission. Additionally, HR users need stats relevant to their roles (Active Staff, Leave, Candidates, Assets), rather than Leads and Students.

## What Changes

- Modify `DashboardStatsAPIView` to return selective metrics based on user permissions instead of demanding the `ADMIN` role.
- Add backend queries for HR-specific stats: Staff on Leave, Pending Candidates, and Available Assets.
- Update the frontend `AdminStatsGrid` to conditionally render only the metric cards the backend returns.
- Provide custom HR cards using lucide-react icons for the newly exposed HR stats.

## Capabilities

### New Capabilities
- `hr-dashboard-metrics`: View HR-specific dashboard metrics including active staff, staff on leave, pending candidates, and available assets.
- `dashboard-stats`: Dynamic permission-based retrieval of dashboard statistics.

### Modified Capabilities

## Impact

- **Backend (`accounts/views.py`)**: `DashboardStatsAPIView` logic changing from role check to permission check.
- **Frontend (`DashboardOverview.jsx`, `AdminStatsGrid.jsx`)**: Handling dynamic metric arrays instead of hardcoding Leads, Staff, and Students.

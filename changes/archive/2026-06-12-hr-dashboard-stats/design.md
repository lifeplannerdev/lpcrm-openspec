## Context

The current `DashboardStatsAPIView` is hardcoded to restrict access strictly to users with the `ADMIN` role. However, the frontend allows users with `staff:view_any` (like HR) to access the dashboard overview page. As a result, HR users see a "Failed to load dashboard statistics" error. Instead of just suppressing the error, we want to provide meaningful metrics to HR.

## Goals / Non-Goals

**Goals:**
- Modify `/stats/` API to support permission-based fine-grained metric access.
- Expose HR-specific stats (Staff on Leave, Pending Candidates, Available Assets) alongside existing stats.
- Update frontend `DashboardOverview` to gracefully handle sparse metrics.
- Add specific visual metric cards for HR stats in the frontend `AdminStatsGrid`.

**Non-Goals:**
- Completely overhauling the role or permission system structure.
- Migrating other API endpoints to permission-based checking at this time.

## Decisions

- **Selective Dictionary Return**: Instead of raising a `PermissionDenied` error entirely, the API will build a dictionary of metrics. It checks each underlying dynamic permission (e.g., `leads:read_tenant`, `staff:read_tenant`) and attaches the stat only if the user has permission.
- **Frontend Graceful Handling**: The frontend `fetchData` callback currently expects `data.total_leads || 0`. This will be changed to strictly check for `undefined`, falling back to `null` if the metric is omitted. `AdminStatsGrid` will check if a stat `!== null` to determine if a specific card should render.
- **HR Stats Queries**: We will add queries to `Candidate`, `Asset`, and `User` models to retrieve the HR stats efficiently using basic `Count`.

## Risks / Trade-offs

- **Risk: Increased API payload logic** → Mitigation: Keep the permission checks simple and use `.count()` to avoid heavy database queries.

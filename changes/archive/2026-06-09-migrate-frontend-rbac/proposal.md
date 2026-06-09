## Why

The backend has recently been updated to use a Many-to-Many Role-Based Access Control (RBAC) system via the `db_roles` field, completely removing the legacy `role` string field from the `User` model. This has caused 500 Internal Server Errors in production because several serializers are still trying to expose the removed `role` field. Concurrently, the frontend still relies heavily on the `role` field for user rendering, permission checks, and form submissions. Migrating the frontend directly to use `db_roles` (and `role_names`) ensures architectural consistency and eliminates these errors permanently without relying on backend workarounds.

## What Changes

- **BREAKING**: Remove the `role` field from all `User` and `Employee` serializers (`leads`, `tasks`, `hr`, `trainers` apps).
- **BREAKING**: The frontend will no longer expect or send `role` in API requests.
- Update frontend UI components to rely exclusively on `db_roles` or `role_names` for role checks and display text.
- Modify the "Add Staff" and "Edit Staff" forms to solely use the `db_roles` array and eliminate the `role` selection.
- Update Dashboard headers, Staff details pages, and Call analytics to map `role_names` rather than `role`.

## Capabilities

### New Capabilities
*(None)*

### Modified Capabilities
- `authorization`: The requirements for defining how users are checked for roles and permissions are modified to only rely on `db_roles` instead of `role`.
- `task-management`: The task management views and employee lists will now rely on `db_roles` for UI rendering.

## Impact

- **Affected Code**: `accounts`, `leads`, `tasks`, `trainers`, `hr` serializers in the backend. Several Pages in the React frontend (e.g., `AddStaffPage`, `EditStaffPage`, `StaffPage`, `StaffDetailsPage`, `CallAnalyticsPage`, `DashboardOverview`, `AllFollowUpsPage`, `AssetManagementPage`).
- **APIs**: User list, Lead list, Task list, Employee list, and Staff creation/update endpoints.
- **Systems**: Core user and authentication rendering in the UI.

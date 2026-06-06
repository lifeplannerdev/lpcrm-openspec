## Why

The backend permission system was recently upgraded to a dynamic Hybrid Permission Engine returning a nested JSON object (`{"resource": ["action"]}`). However, across the frontend application, dozens of legacy authorization checks are still querying the deprecated flat array structure (`user.permissions.includes(...)`) or hardcoded string roles (`user.role === 'ADMIN'`). This causes pages to crash or falsely reject authorized users. We need to systematically migrate the entire frontend UI to use the new `usePermissions` hook and its `hasPermission()` evaluator.

## What Changes

- Migrate all `.includes()` checks for legacy string permissions (e.g., `edit_tasks`, `edit_staff`, `manage_fees`) to the new resource-action notation (e.g., `tasks:edit_any`, `staff:edit_any`, `fees:edit_any`).
- Replace inline role evaluations (`user.role === 'ADMIN'`) with capability evaluations (`hasPermission('staff:view_any')`).
- Wrap rendering blocks in the `<Can perform="resource:action">` component where applicable for cleaner component rendering.

## Capabilities

### New Capabilities

None. This focuses on rewriting legacy authorization checks to utilize existing capabilities.

### Modified Capabilities

- `authorization`: All components MUST utilize the `PermissionsContext` hook for checking user privileges rather than interpreting raw user payloads directly.

## Impact

- **Affected Code**: Dozens of frontend pages and components (e.g. `TasksPage.jsx`, `StaffPage.jsx`, `FeesManagementPage.jsx`, `LeadsTable.jsx`).
- **Impact**: Stabilizes UI rendering under the new permission system and removes all hardcoded role checks, making the frontend completely role-agnostic and ready for fully dynamic RBAC in Phase 2.

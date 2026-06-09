## Why

Currently, the Role Management UI displays all legacy permission strings (like `view_staff_reports` and `manage_asset`) alongside newly implemented RBAC scoped permissions (`resource:action`). However, the backend silently drops any permission string without a colon (`:`). This creates a critical disconnect where administrators believe they are assigning or revoking permissions in the UI, but the backend ignores these toggles entirely. We need to complete the migration to the RBAC system by converting all legacy permission strings to the `resource:action` format across the entire application.

## What Changes

- **BREAKING**: Replace all legacy permissions in the `AppPermission` table and `ROLE_PERMISSIONS` seed configuration with proper `<resource>:<action>` scoped strings (e.g., `view_my_reports` -> `reports:read_own`).
- Update the frontend routing and navigation requirements (`roles.js`) to rely strictly on the new `resource:action` format.
- Create a Django data migration to automatically convert existing `AppPermission` records to the new format so no existing roles lose access during the upgrade.
- Update the `PermissionService` backend logic if necessary, though it should natively support the new scoped strings.
- Audit all views and serializers to ensure they are no longer relying on legacy strings.

## Capabilities

### New Capabilities
- `legacy-permissions-migration`: Establishes the new `<resource>:<action>` conventions for all remaining resources that were still using legacy strings (like `dashboard`, `reports`, `assets`, `penalties`, `tasks`).

### Modified Capabilities

## Impact

- **Database**: `accounts_apppermission` rows will be updated/renamed. Role mappings in `role_permissions` will point to the newly named permissions.
- **Backend API**: Endpoints checking for specific legacy permissions (e.g., `view_all_tasks`) must be updated.
- **Frontend**: Navigation, `PermissionRoute` wrappers, and UI checks (e.g., `Can` component) will need to check the proper `<resource>:<action>` scopes.

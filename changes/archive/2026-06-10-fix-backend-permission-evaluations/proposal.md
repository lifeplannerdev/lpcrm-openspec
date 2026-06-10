## Why

When migrating from legacy permission strings to the new RBAC structure, we updated the strings and mapped roles in the database correctly. However, we missed updating the code that evaluates these permissions. The backend still checks `request.user.permissions` (which is a JSON array of old strings) instead of utilizing the `has_dynamic_permission(user, '<perm>')` helper that checks the new `db_roles` -> `AppPermission` mappings. This mismatch causes `403 Forbidden` errors across the application.

## What Changes

- Search the backend python files for any occurrences of `request.user.permissions` or `user.permissions` that are used in `in` checks.
- Replace these checks with `has_dynamic_permission(request.user, '<new-resource:action-string>')`.
- Refactor helper functions like `_has_perm(user, perm)` (e.g., in `trainers/views.py`) to internally use the `has_dynamic_permission` function from `accounts/permissions.py`.

## Capabilities

### New Capabilities
None

### Modified Capabilities
- `permission-evaluation`: The underlying implementation of permission checking is fully migrating from static JSON lists to DB-backed roles. (No spec requirement changes, just an implementation fix to fully realize the `migrate-legacy-permissions` change).

## Impact

- All REST API endpoints that require `permissions` will now correctly validate using the new RBAC system.
- Files updated: `leads/permissions.py`, `tasks/permissions.py`, `trainers/views.py`, `fees/views.py`, `reports/permissions.py`, and other backend views checking `user.permissions`.

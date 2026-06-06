## Why

The `User` model was recently migrated from using a single string-based `role` field to a Many-to-Many `db_roles` relationship. However, numerous `.role` attribute references remain throughout the codebase (in signals, views, and serializers). Because the `role` field no longer exists on the `User` object, any code attempting to access `user.role` or `instance.role` throws an `AttributeError`, causing `500 Internal Server Errors` on multiple critical endpoints (such as `/api/staff/create/` and `/api/followups/today/`).

## What Changes

- **BREAKING**: We will systematically replace all `.role` attribute accesses on `User` instances across the entire backend with logic that queries the new `db_roles` relationship.
- We will audit the `accounts`, `leads`, `tasks`, `reports`, `credentials`, and `trainers` apps to remove these legacy references.
- Logic checking for a specific role (e.g., `if user.role == 'ADMIN':`) will be updated to check the Many-to-Many field (e.g., `if user.db_roles.filter(name='ADMIN').exists():`).

## Capabilities

### New Capabilities
None.

### Modified Capabilities
- `user-role-management`: The way role checks and permissions are enforced across the backend is being updated to rely purely on the many-to-many `db_roles` relationship rather than a flat string field.

## Impact

- **Affected Code**: 
  - `accounts/signals.py`, `accounts/views.py`
  - `leads/serializers.py`, `leads/views/leads.py`, `leads/views/followups.py`, `leads/views/assignments.py`
  - `tasks/views.py`
  - `reports/views.py`
  - `credentials/views.py`
  - `trainers/signals.py`
- **APIs**: The logic and contract of existing APIs remain identical, but they will no longer crash with 500 errors.

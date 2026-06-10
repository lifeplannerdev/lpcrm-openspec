## Context

The backend has transitioned from a JSON-based list of legacy permission strings to a DB-backed RBAC system where permissions are linked to `db_roles`. However, the API endpoints and serializers still reference `request.user.permissions` expecting the old JSON list. This is causing `403 Forbidden` errors across the board because the JSON array is now effectively obsolete. 

## Goals / Non-Goals

**Goals:**
- Replace direct `user.permissions` access checks with the `has_dynamic_permission()` helper.
- Fix all remaining permission evaluation logic on the backend.

**Non-Goals:**
- Changing the schema of the `AppPermission` table or the DB-backed RBAC structure.
- Modifying frontend code (already completed).

## Decisions

**Decision 1: Use `has_dynamic_permission(user, perm)` helper everywhere.**
Instead of parsing `user.permissions` array, the code must use the established helper in `accounts.permissions.has_dynamic_permission`. This helper automatically checks the database-backed roles/permissions and uses a cache attached to the request object `_dynamic_perms_cache` to minimize repeated DB queries per request.

**Decision 2: Update wrapper functions instead of replacing them.**
Functions like `_has_perm(user, perm)` in `trainers/views.py` will be updated internally to return `has_dynamic_permission(user, perm)` instead of being ripped out, keeping the diff clean and maintaining localized logic where needed.

## Risks / Trade-offs

- **Risk:** We miss some instances of `.permissions` access.
  - **Mitigation:** Run a regex search for `\.permissions` across the `lpcrmbackend-main` repository and manually inspect each usage to ensure it is replaced.
- **Risk:** Cache staleness in `_dynamic_perms_cache`.
  - **Mitigation:** Since it's attached to the `user` object in the request scope, it only persists for the lifetime of that single request. It will not become stale during a single HTTP cycle.

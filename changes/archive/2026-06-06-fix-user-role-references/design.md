## Context

The `User` model was previously using a single string-based `role` field. A recent migration (`0032_migrate_legacy_roles.py`) replaced this with a Many-to-Many `db_roles` relationship to a `Role` model. However, many parts of the application still use `user.role` or `instance.role`, which causes `AttributeError` when accessed, resulting in `500 Internal Server Error`s across various endpoints (`/api/staff/create/`, `/api/followups/today/`).

## Goals / Non-Goals

**Goals:**
- Eliminate all instances of `user.role` or `instance.role` in the codebase.
- Replace string-based role checks with robust Many-to-Many `db_roles` queries (e.g. `.filter(name=...).exists()`).
- Restore full functionality to endpoints currently crashing (staff creation, fetching follow-ups, etc.).

**Non-Goals:**
- Changing the underlying business logic of who has access to what. (We are purely updating the syntax of how access is verified).
- Altering the `User` or `Role` database schema.

## Decisions

- **Direct Query vs Property Helpers**: Instead of re-implementing `@property def role(self):` on the `User` model to return a single role as a fallback (which might be ambiguous if a user has multiple roles), we will update the explicit `.filter().exists()` checks throughout the code. This ensures correctness and embraces the Many-to-Many architecture.
- **Handling Permissions checks in views**: Where `user.role in FULL_ACCESS_ROLES` is used, we will update it to check if any of the user's `db_roles` are in that list, e.g., `user.db_roles.filter(name__in=FULL_ACCESS_ROLES).exists()`.

## Risks / Trade-offs

- **[Risk]** Performance impact of querying `db_roles` dynamically on every request.
  **Mitigation**: Django's `prefetch_related('db_roles')` is already used in many serializers, and the number of roles per user is very small. The overhead will be negligible compared to the alternative.

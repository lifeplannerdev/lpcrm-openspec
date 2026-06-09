## Context

The backend has transitioned from a legacy permission array stored directly on the `User` model to a robust Role-Based Access Control (RBAC) system defined in `accounts.permissions` and managed via DB Roles. However, the `CredentialPermission` class in the `credentials` app still strictly checks the legacy `request.user.permissions` array. Since normal users (like counsellors, HR, etc.) do not have `credentials:view` seeded into their legacy JSON arrays, the API returns a 403 Forbidden on the `list` endpoint, rendering them unable to view credentials that have been properly assigned/shared with them in the database.

## Goals / Non-Goals

**Goals:**
- Eliminate the 403 Forbidden block for standard users accessing the `GET /api/credentials/` list endpoint.
- Replace legacy JSON array permission checks with `has_dynamic_permission()` for the credentials API.
- Ensure that read visibility is securely enforced exclusively by the existing `get_queryset()` logic (which correctly scopes access to shared and created credentials).

**Non-Goals:**
- We will not modify the frontend UI routing. If the user can successfully fetch from the API, the page will render correctly.
- We will not change how `shared_users` or `shared_roles` are assigned.

## Decisions

- **Unblock Read Actions**: We will return `True` for `list`, `retrieve`, `history`, `requests`, and `propose_update` actions in `CredentialPermission.has_permission`.
  *Rationale*: Read actions should not require a global `credentials:view` permission string. The `get_queryset` method correctly filters down to *only* credentials the user is allowed to see. If they have none, they see an empty list. Object-level access is already enforced via `has_object_permission`.
- **Adopt Dynamic Permissions**: For write operations (e.g., `create`, `update`, `approve_request`), we will replace the `request.user.permissions` array lookup with `has_dynamic_permission(request.user, 'credentials:manage')`.
  *Rationale*: This aligns the credentials app with the new system. Only users whose DB Roles explicitly grant `credentials:manage` can perform global administrative writes, while creators retain access through `has_object_permission`.

## Risks / Trade-offs

- **Risk**: Opening up the `list` endpoint could accidentally expose all credentials if `get_queryset` is flawed.
  **Mitigation**: The existing `get_queryset` explicitly scopes access: `Q(created_by=user) | Q(shared_users=user) | Q(shared_roles__in=user.db_roles.all())`. This is completely safe and robust.

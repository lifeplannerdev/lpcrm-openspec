## Why

When a credential is shared with a standard user, they cannot access it because `CredentialPermission` in the backend explicitly requires the user's `permissions` JSON field to contain `credentials:view` or `credentials:manage` just to hit the list or retrieve endpoints. Since we have migrated to a dynamic, DB-backed Roles/Permissions system (RBAC), normal users no longer have hardcoded strings in that JSON field, resulting in an immediate `403 Forbidden` error. This completely breaks the credential sharing feature. We must update the credentials permissions logic to align with the new system.

## What Changes

- Modify `CredentialPermission` to permit `list`, `retrieve`, `history`, and `requests` actions for *all* authenticated users, trusting the `get_queryset` and object-level permissions to enforce visibility.
- Remove legacy JSON `request.user.permissions` checks in `CredentialPermission` and `CredentialCategoryPermission`.
- Replace legacy permission checks with the modern `has_dynamic_permission(request.user, 'credentials:manage')` for write operations (create, update, delete).

## Capabilities

### New Capabilities
None.

### Modified Capabilities
- `authorization`: Extends the new DB-driven dynamic RBAC model fully into the Credentials Vault.
- `credentials-vault`: Minor requirement update to clarify that credential visibility is controlled by object-level sharing and query filtering, not by a global API view gatekeeper.

## Impact

- **Affected Code**: `lpcrmbackend-main/credentials/views.py`
- **APIs**: All `GET`, `POST`, `PATCH`, `DELETE` endpoints for `/api/credentials/` and `/api/credential-categories/`
- **Systems**: Credentials Vault access for standard users

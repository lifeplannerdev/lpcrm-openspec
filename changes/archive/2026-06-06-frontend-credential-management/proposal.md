## Why

The backend Django API for the Credentials Vault already fully supports editing credentials, deleting credentials, and sharing them with specific users or roles. However, the React frontend currently lacks the user interface to access these features. Creators and Admins have no way to edit or delete their credentials, and cannot assign `shared_users` or `shared_roles` when adding or editing a credential. This change will build out the missing frontend UI components to fully utilize the existing backend capabilities.

## What Changes

- Add "Edit" and "Delete" icon buttons to the Credential cards for authorized users (Creators and users with `credentials:manage` permission).
- Update the `AddCredentialModal` to include multi-select dropdowns for assigning `shared_users` and `shared_roles`.
- Allow the `AddCredentialModal` to be reused as an `EditCredentialModal`, populating existing data including assigned users and roles.
- Add confirmation dialogs before deleting a credential.

## Capabilities

### New Capabilities
- None. This purely exposes existing backend capabilities to the frontend.

### Modified Capabilities
- `credentials-vault`: The "Premium Vault Interface" requirement is changing to include UI controls for editing, deleting, and sharing credentials.

## Impact

- **Backend Models**: No changes required.
- **Backend API**: No changes required.
- **Frontend UI**: `CredentialsVault.jsx` will get new action buttons. `CredentialModals.jsx` will be updated to include new form inputs for sharing and handle `PATCH` requests for edits.

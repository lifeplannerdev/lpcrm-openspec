## Why

The organization currently lacks a centralized, secure location to store shared credentials for emails, social media accounts, vendor platforms, and other services. This leads to insecure credential sharing (e.g., via chat or unencrypted documents) and makes it difficult to manage access when staff join or leave the organization.

## What Changes

- Create a new "Credentials Vault" module within the CRM.
- Implement an encrypted storage mechanism for passwords and sensitive secrets.
- Add granular sharing controls allowing credentials to be shared with specific users, roles, or kept private.
- Build a premium UI for viewing, copying, and managing credentials securely.
- **Password Timeline**: Maintain a decryptable history of all previous passwords.
- **Update Request Workflow**: Shared users cannot overwrite passwords directly; they must submit a change request that is manually approved by an admin or the credential owner.

## Capabilities

### New Capabilities
- `credentials-vault`: Covers the secure storage, retrieval, and sharing of shared organizational credentials.

### Modified Capabilities
- `authorization`: Extends the granular permissions engine to include `view_credentials`, `manage_credentials`, and `share_credentials` flags.

## Impact

- **Backend**: Requires new models for encrypted credential storage, access control logic, credential history, and update requests.
- **Frontend**: New UI screens added to the MainTabNavigator (or Menu grid) protected by role-based permissions, including a timeline view and an approvals queue.
- **Security**: Introduces encryption/decryption keys for sensitive fields. Historical passwords remain encrypted and decryptable.

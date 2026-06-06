## Context

Currently, the organization does not have a safe and central place to store and share credentials (e.g., admin passwords, social media accounts, specific software licenses). These are often shared via chat applications, leading to insecure storage and making it impossible to revoke access easily when someone leaves. We want a centralized "Credentials Vault" integrated directly into the CRM, reusing our existing roles and permissions engine.

## Goals / Non-Goals

**Goals:**
- Provide a secure, encrypted mechanism to store passwords/secrets in the database.
- Integrate granular permissions (`view_credentials`, `manage_credentials`, `share_credentials`).
- Build a premium UI to view, create, edit, and copy credentials easily.
- Allow credentials to be assigned/shared with specific roles or specific users.
- Provide a decryptable timeline of previous passwords.
- Implement an update request workflow for shared users to propose password changes securely.

**Non-Goals:**
- We are not building a full-fledged enterprise password manager like 1Password (no browser extensions, no auto-fill).
- We are not implementing hardware-backed keys or HSMs. We will use standard symmetric encryption at the application layer.

## Decisions

- **Encryption Strategy**: We will use `Fernet` (symmetric encryption from Python's `cryptography` library) to encrypt the `password` / `secret` fields before saving them to PostgreSQL, and decrypt them when requested via the API. This ensures that a database leak does not expose raw passwords. The `FERNET_KEY` will be stored in the Vercel environment variables.
- **Sharing Mechanism**: The `Credential` model will have Many-to-Many relationships to both `User` (specific users) and `Role` (specific roles). If a credential has no users/roles assigned, it is private to the `created_by` user.
- **Update Workflow & Approvals**: We introduce `CredentialUpdateRequest`. Shared users cannot modify the `Credential` directly. They submit a request. The vault owner or users with `manage_credentials` can approve it.
- **Password Timeline**: When a password is changed or an update request is approved, the previous encrypted password is moved to `CredentialHistory`. These historical records remain decryptable so users can view old passwords if needed.

## Risks / Trade-offs

- **Risk: Key Management**: If the `FERNET_KEY` is lost or rotated without re-encrypting the database, all credentials become irrecoverable.
  - **Mitigation**: Document the key management process carefully and ensure the key is backed up securely in Vercel's environment settings.
- **Risk: Frontend Caching**: Passwords might be cached in the browser or Redux state.
  - **Mitigation**: We will not fetch passwords in list views. Passwords will only be fetched (or decrypted on the client, or sent decrypted by the server) when the user explicitly clicks an "Unmask" or "Copy" button. Wait, actually, the server can just send the decrypted password in the detail API. We should ensure the frontend clears this from state when the component unmounts.

## 1. Backend Data Model & Encryption

- [x] 1.1 Update `FERNET_KEY` requirement in the Django settings and verify `cryptography` library is installed
- [x] 1.2 Create the `Credential` Django model (title, username, encrypted_password, url, notes)
- [x] 1.3 Create the `CredentialHistory` model to store historical encrypted passwords
- [x] 1.4 Create the `CredentialUpdateRequest` model for the approval workflow
- [x] 1.5 Add ManyToMany fields on `Credential` for `shared_users` and `shared_roles`
- [x] 1.6 Add `cryptography.fernet` helper methods on the models for encrypting and decrypting
- [x] 1.7 Create and run the Django migration

## 2. Backend Permissions & Roles

- [x] 2.1 Update `permission_templates.py` to seed `view_credentials`, `manage_credentials`, and `share_credentials` to Admin roles
- [x] 2.2 Re-run the `seed_roles` management command to apply the new permissions to existing roles

## 3. Backend API

- [x] 3.1 Create `CredentialSerializer` (masking the password field in lists)
- [x] 3.2 Create `CredentialDetailSerializer` that includes the decrypted password (only accessible if authorized)
- [x] 3.3 Create `CredentialHistorySerializer` and `CredentialUpdateRequestSerializer`
- [x] 3.4 Create a ViewSet for Credentials (`list`, `create`, `retrieve`, `update`, `destroy`)
- [x] 3.5 Implement object-level permissions in the ViewSet (Only allow viewing if `created_by == user` OR user in `shared_users` OR user's role in `shared_roles` OR user is admin)
- [x] 3.6 Create endpoints to submit, approve, and reject `CredentialUpdateRequest`
- [x] 3.7 Add API routing for `/api/credentials/` and related endpoints

## 4. Frontend UI Foundation

- [x] 4.1 Update `config/roles.js` (or similar) to recognize the new credential permissions
- [x] 4.2 Add "Credentials Vault" to the Main Menu or sidebar (visible only if `view_credentials` is true)
- [x] 4.3 Create the `CredentialsVault` React page using the premium glassmorphic UI design

## 5. Frontend Features

- [x] 5.1 Add "Add Credential" modal to securely save new passwords
- [x] 5.2 Implement password unmasking (`decrypted_password` field toggle via `CredentialDetail` API)
- [x] 5.3 Add the "Propose Update" modal for shared users
- [x] 5.4 Build the "Update Requests" view for admins (approve/reject actions)
- [x] 5.5 Integrate the `CredentialHistory` timeline modal to show previous passwords
- [x] 5.6 Wire up backend API calls to the React components using `useApi`
- [x] 5.7 Protect actions based on permissions (`credentials:manage` vs `credentials:view`) pending requests

## 6. Verification

- [ ] 6.1 Test backend encryption directly via Django shell
- [ ] 6.2 Test API object-level permissions as a non-admin user
- [ ] 6.3 Test frontend creation, viewing, and copying of a credential

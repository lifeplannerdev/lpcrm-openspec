## 1. Credential Actions (Edit & Delete)

- [x] 1.1 In `CredentialsVault.jsx`, add an `Edit` button (pencil icon) next to the history icon on the credential card. Ensure it opens the `AddCredentialModal` with `editData={cred}`.
- [x] 1.2 In `CredentialsVault.jsx`, add a `Delete` button (trash icon) next to the edit icon.
- [x] 1.3 Ensure these buttons are only visible if the user is the creator (`cred.created_by === user.id`) or has the `credentials:manage` permission.
- [x] 1.4 Create a `handleDelete(id)` function in `CredentialsVault.jsx` that prompts for confirmation using `window.confirm`, calls `DELETE /api/credentials/<id>/`, and refreshes the list on success.

## 2. Sharing UI (Users & Roles)

- [x] 2.1 In `CredentialModals.jsx`, update the `AddCredentialModal` state to fetch `staff` from `/api/users/?is_staff=true` (or the equivalent endpoint) and `roles` from `/api/roles/` on mount.
- [x] 2.2 Add a multi-select field (or checkbox list) to the `AddCredentialModal` for `shared_users`.
- [x] 2.3 Add a multi-select field (or checkbox list) to the `AddCredentialModal` for `shared_roles`.
- [x] 2.4 Ensure `formData.shared_users` and `formData.shared_roles` correctly map back to arrays of IDs when submitted via POST/PATCH.

## 3. Verification

- [x] 3.1 Verify that an admin or creator can click Edit, change the title, and save it successfully.
- [x] 3.2 Verify that an admin or creator can delete a credential successfully.
- [x] 3.3 Verify that a new credential can be created and shared with a specific user, and that the selected user correctly persists when editing that credential.

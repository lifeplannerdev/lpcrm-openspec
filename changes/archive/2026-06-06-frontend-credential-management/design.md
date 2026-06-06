## Context

The backend API for the Credentials Vault supports full CRUD operations and granular sharing via `shared_users` and `shared_roles`. However, the React frontend currently lacks the UI components to utilize these features. We need to add "Edit" and "Delete" buttons to the credential cards, and enhance the Add/Edit form to support selecting users and roles for sharing.

## Goals / Non-Goals

**Goals:**
- Add "Edit" (pencil) and "Delete" (trash) buttons to the credential cards in `CredentialsVault.jsx`.
- These buttons should only be visible if the user is the creator or has `credentials:manage` permissions.
- Update `CredentialModals.jsx` (`AddCredentialModal`) to fetch the list of available staff and roles from the backend.
- Add multi-select dropdowns to the modal to assign `shared_users` and `shared_roles`.
- Wire the Delete button to the `DELETE /api/credentials/<id>/` endpoint with a confirmation prompt.

**Non-Goals:**
- Changes to the backend models or views (they are already correct).
- Building complex custom multi-select components from scratch (we will use simple `<select multiple>` or a similar lightweight approach).

## Decisions

- **UI Placement**: The Edit and Delete buttons will sit next to the existing "History" button on the credential card, visible on hover.
- **Form State**: `AddCredentialModal` already accepts an `editData` prop and handles `PATCH` vs `POST`. We just need to add the `shared_users` and `shared_roles` array fields to the form UI, and ensure they are populated when `editData` is passed.
- **Fetching Users/Roles**: The modal will fetch `/api/users/` (or similar staff endpoint) and `/api/roles/` on mount to populate the sharing dropdowns.

## Risks / Trade-offs

- **Risk**: The user/role API endpoints might be named differently or require specific permissions.
  - **Mitigation**: We will check the `accounts` or `users` endpoints used elsewhere in the CRM to fetch staff and roles safely.

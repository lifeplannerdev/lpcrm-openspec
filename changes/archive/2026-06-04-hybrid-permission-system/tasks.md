## 1. Backend: Permission Engine

- [x] 1.1 Create `PermissionService` in Django to evaluate legacy roles and companies into JSON payload.
- [x] 1.2 Define the base dictionary of generic permissions for 'admin' and 'manager' roles.
- [x] 1.3 Update the login endpoint (or JWT token generator) to include the calculated `permissions` in the response.
- [x] 1.4 Update the `/api/user/me` endpoint to also return the `permissions` payload so session restores work correctly.

## 2. Frontend: Permission Context

- [x] 2.1 Create a `PermissionsContext` in React to store the `permissions` object globally.
- [x] 2.2 Update the `AuthProvider` or login logic to save the `permissions` from the API response into the `PermissionsContext`.
- [x] 2.3 Create a generic `<Can>` wrapper component (e.g., `<Can perform="leads:edit">`).
- [x] 2.4 Create a `usePermissions` hook to allow programmatic permission checks (e.g., hiding a column in a table).

## 3. Frontend: Component Migration

- [x] 3.1 Migrate `StaffPermissionsModal.jsx` to use the `<Can>` component instead of legacy role checks.
- [x] 3.2 Audit other components for hardcoded role logic and replace them with `<Can>` or `usePermissions`.
- [x] 3.3 Test rendering with an 'admin' token vs a 'manager' token to ensure the UI updates correctly based on the payload.

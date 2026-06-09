## Why

When users refresh a page that requires permissions (like `/leads`), the application redirects them to the dashboard (`/`). This happens because the `PermissionsContext` relies on a `useEffect` to derive permissions from the `user` object. During the initial render after `AuthContext` finishes loading, the permissions state is empty, causing `<PermissionRoute>` to falsely evaluate the user as unauthorized. 

## What Changes

- Modify `PermissionsContext.jsx` to derive the `permissions` object synchronously during render instead of relying on a separate `useState` updated via `useEffect`.

## Capabilities

### New Capabilities

### Modified Capabilities
- `permission-evaluation`: Modify the internal timing of permission resolution to happen synchronously with authentication loading.

## Impact

- Frontend context (`lpcrm-frontend-main/src/context/PermissionsContext.jsx`).
- Routing stability during page reloads.

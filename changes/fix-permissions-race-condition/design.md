## Context

When a user refreshes the page on a protected route, `<PermissionRoute>` renders immediately after `AuthContext` finishes loading. The `PermissionsContext` currently uses a `useEffect` hook to update a state variable `permissions` from `user.permissions`. Because `useEffect` runs asynchronously after the render cycle, the permissions object is temporarily empty (`{}`), causing the routing logic to redirect the user back to the dashboard as a false-negative authorization check.

## Goals / Non-Goals

**Goals:**
- Eliminate the one-render-cycle delay in `PermissionsContext` to resolve the routing race condition.
- Maintain existing authorization logic for actual permissions.

**Non-Goals:**
- Change the structure or schema of the `permissions` object.

## Decisions

- **Synchronous derivation**: We will remove the `useState` and `useEffect` hooks for `permissions`. Instead, `permissions` will be derived synchronously during the render cycle: `const permissions = user?.permissions || {};`. This ensures that when `useAuth` finishes loading, the permissions are instantly available without delay.

## Risks / Trade-offs

- **None**: This is purely a performance and correctness fix by removing unnecessary state duplication.

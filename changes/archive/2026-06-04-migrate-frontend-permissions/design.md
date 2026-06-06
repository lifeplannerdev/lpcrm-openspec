## Context

The UI relies heavily on explicit string checks (e.g., `user.permissions.includes('edit_tasks')`) or role checks (e.g., `userRole === 'ADMIN'`). Because the backend now returns a dynamic JSON object containing resource-specific granular actions (`{"tasks": ["edit_any", "delete_any"]}`), these legacy checks either fail entirely or bypass the granular system.

## Goals / Non-Goals

**Goals:**
- Strip all `.includes()` checks targeting `user.permissions` across the frontend.
- Implement the `usePermissions` hook across roughly 15-20 identified legacy files.
- Ensure the frontend remains robust when handling the new dynamic dictionary from the backend.

**Non-Goals:**
- We are not modifying the backend or the API responses; the `PermissionService` has already been implemented.

## Decisions

**Decision 1: Use `hasPermission('resource:action')` for granular logic**
- Instead of checking `edit_tasks`, we will map logic to the corresponding resource action:
  - `edit_tasks` -> `hasPermission('tasks:edit_any') || hasPermission('tasks:edit_tenant') || hasPermission('tasks:edit_own')` (We can use a broader `hasAnyPermission('tasks')` or write a custom helper where needed).
  - Since many legacy checks were broad, we will use the `hasAnyPermission(resource)` hook function created previously for generic view/edit gates, and `hasPermission(resource:action)` for specific destructive gates.

**Decision 2: Remove Hardcoded `isAdmin` checks**
- Some UI elements check `user.role === 'ADMIN'` to display features. We will replace these by checking if the user has wildcard or global read access to `staff` (e.g., `hasPermission('staff:view_any')`), naturally deriving "admin" capabilities from actual capabilities rather than titles.

## Risks / Trade-offs

- **Risk**: By generalizing `hasAnyPermission()`, we might accidentally expose a button (like Edit) to a user who only has `read` access.
- **Mitigation**: We must carefully use `hasAnyPermission` ONLY for view gates. For action gates like "Assign Tasks" or "Manage Fees", we MUST check `hasPermission('resource:edit_any')` explicitly.

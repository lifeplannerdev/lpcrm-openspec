## Context

The newly introduced Hybrid Permission System dynamically resolves a user's permissions into a JSON dictionary (e.g. `{"leads": ["read", "create"]}`). However, the existing `Navbar` component and its dependency `config/roles.js` statically check an array of string-based legacy permissions (`["view_leads"]`). This schema mismatch causes the navbar to render as empty because `Array.isArray()` evaluates to `false` on the dictionary payload.

## Goals / Non-Goals

**Goals:**
- Update the `masterNavigation` array in `roles.js` to map each navigation item to its new equivalent resource and action (e.g., `leads:read_any` or `leads:read`).
- Update `Navbar.jsx` (and potentially `DesktopNavbar.jsx` / `MobileNavbar.jsx` if logic is passed down) to filter navigation items using the `hasPermission` function from the `usePermissions` hook.

**Non-Goals:**
- Completely rewrite the routing architecture.
- Modify the backend payload generation (already completed).

## Decisions

**Decision 1: Use `usePermissions()` hook over manual object traversal**
- *Rationale*: We already created a robust `usePermissions()` context hook that handles wildcards (`*`) and format splitting correctly. This centralizes all authorization logic on the frontend. We will pass `hasPermission` into a filtering utility instead of the raw permissions object, or we will do the filtering directly within the `Navbar` component where the hook is instantiated.

**Decision 2: Update `masterNavigation` required permissions**
- *Rationale*: Each item in `roles.js` needs a valid `resource:action` string.
  - Leads -> `leads:read_own` (or any read permission, since `hasPermission` could check generic access if we modify it, or we just map it to something they'd definitely have like `leads:read_any` or maybe we need a special method `hasAnyPermission(resource)`).
  - *Refinement*: The navigation should be visible if the user has *any* read access to the resource (`read_own`, `read_tenant`, `read_any`). The `hasPermission` function in `PermissionsContext` currently strictly matches the exact string. We will modify `PermissionsContext.jsx` to support checking if a user has access to a specific resource generally (e.g., `hasPermission('leads:read')` checking any read action). Or we just update the hook to support `resource:read` as a catch-all for `read_own`, `read_tenant`, `read_any`.

## Risks / Trade-offs

- **Risk**: A user has `leads:read_own` but the navbar checks for `leads:read_any`, so they can't see the Leads tab.
- **Mitigation**: Update `PermissionsContext.hasPermission` to gracefully treat `leads:read` as a check for *any* read permission (e.g., `read_own`, `read_tenant`, `read_any`), ensuring the tab is visible if they have any level of read access.

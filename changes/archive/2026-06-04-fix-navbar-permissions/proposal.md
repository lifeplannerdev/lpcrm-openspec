## Why

The recently implemented Hybrid Permission System completely changed the payload format of user permissions from an array of strings (e.g., `["view_leads"]`) to a nested JSON object (e.g., `{"leads": ["read"]}`). The frontend `Navbar` component, specifically the `roles.js` configuration, expects an array. Since it encounters a JSON object, it returns an empty navigation array, resulting in an empty dashboard sidebar for all users, including ADMINs. We need to wire the navigation components to use the new `usePermissions` hook.

## What Changes

- Update `roles.js` to define navigation items with required resources and actions (e.g. `leads:read_any` or `leads:read`) instead of legacy string matching.
- Refactor `Navbar.jsx` (and potentially `roles.js` functions) to utilize the new `usePermissions` hook (`hasPermission`) instead of the legacy `permissions.includes()` check.

## Capabilities

### New Capabilities

None. This is a fix for existing components.

### Modified Capabilities

- `navigation`: The frontend navigation system must evaluate permissions using the new `PermissionsContext` hook and dot/colon notation (e.g. `leads:read`) rather than legacy array lookups.

## Impact

- **Affected Code**: `src/config/roles.js`, `src/Components/layouts/Navbar.jsx`, `src/Components/layouts/DesktopNavbar.jsx`, `src/Components/layouts/MobileNavbar.jsx`
- **Impact**: Restores navigation visibility based on the new Hybrid Permission Engine.

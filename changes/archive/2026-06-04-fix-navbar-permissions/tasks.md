## 1. Modify Permissions Hook

- [x] 1.1 Update `PermissionsContext.jsx` to export a `hasAnyPermission(resource)` function or modify `hasPermission` to accept just the resource name (e.g., `leads`) and return true if the user has any action allowed for that resource.

## 2. Refactor Roles Config

- [x] 2.1 Update `src/config/roles.js` to change `requiredPermission` from legacy strings (e.g. `view_leads`) to the new resource notation (e.g. `leads`).
- [x] 2.2 Update `getMenuForPermissions` in `src/config/roles.js` to either accept the `hasPermission` function directly or be moved/rewritten so it doesn't hardcode array parsing. (e.g. `export const getFilteredMenu = (hasPermission) => masterNavigation.filter(item => hasPermission(item.requiredPermission));`)

## 3. Update Navbar Components

- [x] 3.1 Refactor `src/Components/layouts/Navbar.jsx` to consume `getFilteredMenu` and pass in `hasAnyPermission` or `hasPermission` from the `usePermissions` hook.
- [x] 3.2 Ensure `DesktopNavbar.jsx` and `MobileNavbar.jsx` render the filtered navigation array correctly.

## 4. Verification

- [x] 4.1 Verify the navigation bar renders successfully for an `ADMIN` user with full access.
- [x] 4.2 Verify the navigation bar renders successfully for a restricted user, hiding unauthorized tabs.

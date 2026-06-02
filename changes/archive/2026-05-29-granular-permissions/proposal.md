## Why

The current Role-Based Access Control (RBAC) system is too rigid and relies on hardcoded strings across the frontend and backend. This makes it impossible to grant exceptions (e.g., giving a specific Admission Manager access to Reports) without either giving it to all Admission Managers or creating an entirely new role. Migrating to a granular, template-based permission system will allow exact control over what screens and actions each individual user can access, while keeping Roles as a convenient template for initial setup.

## What Changes

- **BREAKING**: Replace hardcoded role checks (`user.role === 'ADMIN'`) with granular permission checks (`user.permissions.includes('edit_tasks')`) across the frontend UI.
- Introduce a new JSON array on the Django `User` model to store granular permissions.
- Introduce Role Templates in the backend that populate a user's permissions when their role is assigned.
- Introduce a new "Permissions Management" UI in the frontend (accessible only to Admins) to manage individual user permissions.
- Update API endpoints to check granular permissions instead of roles.

## Capabilities

### New Capabilities
- `granular-permissions-engine`: The core backend logic for storing, assigning, and checking individual user permissions based on templates.
- `permissions-management-ui`: The frontend interface for Admins to view and toggle specific permissions for any user in the system.

### Modified Capabilities
- `user-auth`: The login payload will now include a `permissions` array alongside the user role.

## Impact

- **Frontend Navigation**: The `src/config/roles.js` will be heavily refactored to map tabs to required permissions rather than roles.
- **Frontend Components**: Any component conditionally rendering based on `user.role` will need updating.
- **Backend Auth**: Login token payloads will carry more data (`permissions` list).
- **Backend APIs**: DRF permission classes across all apps (`tasks`, `trainers`, etc.) will be updated to check `user.permissions`.

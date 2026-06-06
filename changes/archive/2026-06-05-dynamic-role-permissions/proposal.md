## Why

The current roles and permissions system relies on hardcoded role presets and fallbacks. To scale effectively and provide administrators with clear control over specific people's access, roles and permissions must be managed dynamically through a database and an intuitive frontend interface, ensuring that permission checks across the platform are fully aligned with DB-stored policies.

## What Changes

- **Database-Driven Roles and Permissions:** Move all hardcoded roles and permissions out of the codebase and into standard relational database tables.
- **Role and Permission Management APIs:** Introduce full CRUD endpoints to manage roles, assign permissions to roles, and assign roles to users.
- **Frontend Management UI:** Create a dynamic interface to view, create, edit, and delete roles, and toggle their associated permissions.
- **System-Wide Permission Enforcement:** Update every existing page and backend endpoint that checks roles or permissions to solely rely on the newly defined dynamic system, removing any legacy hardcoded checks.
- **BREAKING:** Hardcoded role and permission fallback logic will be completely removed, requiring an initial database seed for the system to function correctly.

## Capabilities

### New Capabilities
- `dynamic-roles-permissions-management`: The ability to perform CRUD operations on roles and assign fine-grained permissions to these roles dynamically via backend APIs and a frontend UI.

### Modified Capabilities
- `backend-hybrid-permissions`: Removing the hardcoded legacy fallback evaluation for permissions, forcing strict reliance on DB records.
- `permissions-management-ui`: Expanding from just individual user permissions to also include managing generic role definitions and templates dynamically.

## Impact

- **Database**: New tables (`roles`, `permissions`, `role_permissions`, `user_roles`).
- **Backend APIs**: Existing permission generation logic will lose hardcoded fallbacks; new APIs added for role/permission management.
- **Frontend**: New administrative screens for Role Management; existing permission checks continue using the global store but may require backend re-sync when roles change.

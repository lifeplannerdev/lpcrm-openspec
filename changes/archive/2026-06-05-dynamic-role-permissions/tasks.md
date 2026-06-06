## 1. Database Schema & Seeding

- [x] 1.1 Create migration for `roles`, `permissions`, `role_permissions`, and `user_roles` tables
- [x] 1.2 Create seed script to populate default/legacy roles (MD, CEO, HR, etc.) into the database, mapped to their correct permissions
- [x] 1.3 Ensure seed script revokes any existing hardcoded admin bypasses (`is_superuser=True` or `ADMIN` role) from all users, EXCEPT creating exactly one superuser named `admin` with password `admin`

## 2. Backend APIs for Roles & Permissions

- [x] 2.1 Implement API endpoint to list all available permissions (`GET /api/permissions`)
- [x] 2.2 Implement API endpoints for Roles CRUD (`GET /api/roles`, `POST /api/roles`, `PUT /api/roles/:id`, `DELETE /api/roles/:id`)
- [x] 2.3 Implement API endpoints for Role-Permissions management (fetch permissions for role, update permissions for role)
- [x] 2.4 Implement API endpoint for User-Roles management (assign role to user)

## 3. Backend Authorization Logic Update

- [x] 3.1 Update the `backend-hybrid-permissions` payload generation to read user roles and permissions dynamically from the database
- [x] 3.2 Remove legacy hardcoded fallback evaluation logic from the backend
- [x] 3.3 Ensure all backend endpoints check permissions based on the new DB-driven system seamlessly

## 4. Frontend Role Management UI

- [x] 4.1 Create Role List page showing existing roles
- [x] 4.2 Create Role Editor page/modal to define role name and attach granular permissions
- [x] 4.3 Update existing User/Staff Management page to allow assigning DB-backed roles instead of hardcoded presets
- [x] 4.4 Perform exhaustive audit and update of all 25+ frontend screens, tabs, and buttons to exclusively use the `<Can>` wrapper driven by the DB payload
## 5. Verification & Testing

- [x] 5.1 Test database migrations and seeding script in a staging/local environment
- [x] 5.2 Verify that logging in with an existing user loads correct DB-backed permissions
- [x] 5.3 Test creating a new custom role, assigning it to a user, and verifying their access changes appropriately

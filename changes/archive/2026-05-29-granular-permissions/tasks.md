## 1. Backend Data & Settings Setup

- [x] 1.1 Add `permissions` JSONField to custom `User` model in `accounts/models.py`
- [x] 1.2 Create `accounts/permission_templates.py` containing default permissions for each role
- [x] 1.3 Update User creation and role-update signals/logic to populate `permissions` from templates

## 2. Backend Migration Script

- [x] 2.1 Write and run a Django management command to assign the default template permissions to all existing users based on their current roles

## 3. Backend Authorization & API

- [x] 3.1 Create `HasPermission` DRF permission class
- [x] 3.2 Update DRF permission classes across apps (`tasks`, `trainers`, etc.) to use the new granular permission checks instead of checking roles
- [x] 3.3 Update Login/Auth serializer to include the `permissions` array in the response payload

## 4. Frontend Navigation & Routing

- [x] 4.1 Refactor `src/config/roles.js` to map navigation tabs to required permissions rather than roles
- [x] 4.2 Update layout/sidebar rendering logic to use `user.permissions` for determining tab visibility

## 5. Frontend Component Refactoring

- [x] 5.1 Refactor `TasksPage.jsx`, `TaskViewPage.jsx`, and `TaskCreationPage.jsx` to check `user.permissions.includes('edit_tasks')`
- [x] 5.2 Refactor `LeadsPage.jsx` and related lead pages to check granular permissions
- [x] 5.3 Refactor `StaffPage.jsx`, `PenaltyManagementPage.jsx`, and other pages currently relying on hardcoded role arrays

## 6. Permissions Management UI

- [x] 6.1 Create `StaffPermissionsModal.jsx` (or add section to Staff Profile) to view and edit a user's permissions array
- [x] 6.2 Implement frontend API calls to update the user's `permissions` array (`PATCH /api/accounts/staff/<id>/`)
- [x] 6.3 Update `StaffPage.jsx` and `StaffDetailView` to expose this new permissions editor

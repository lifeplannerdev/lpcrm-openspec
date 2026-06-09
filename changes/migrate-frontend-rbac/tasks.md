## 1. Backend Serializers Update

- [x] 1.1 Remove `'role'` from `UserSimpleSerializer` in `leads/serializers.py`
- [x] 1.2 Remove `'role'` from `EmployeeSerializer` in `tasks/serializers.py`
- [x] 1.3 Remove `'role'` from `StaffListSerializer` in `hr/serializers.py`
- [x] 1.4 Remove `'role'` from `TrainerUserSerializer` in `trainers/serializers.py`

## 2. Frontend User Context & Display Updates

- [x] 2.1 Update `DashboardOverview.jsx` to render `role_names` securely without falling back to `role`
- [x] 2.2 Update `StaffDetailsPage.jsx` to render `role_names`
- [x] 2.3 Update `StaffPage.jsx` (Staff directory list) to rely on `role_names` exclusively
- [x] 2.4 Update `CallAnalyticsPage.jsx` to map `role_names` through `getRoleLabel()`

## 3. Frontend Component Logic & Permissions Updates

- [x] 3.1 Update `AllFollowUpsPage.jsx` filtering logic to check against `role_names` array rather than `user.role` string
- [x] 3.2 Update `AssetManagementPage.jsx` to ensure admin filter uses `role_names` properly
- [x] 3.3 Update `MyTasksPage.jsx` task assigners logic
- [x] 3.4 Update `FeesManagementPage.jsx` access checks

## 4. Frontend Forms Migration

- [x] 4.1 Update `AddStaffPage.jsx` initial state, validation, and payload preparation to omit `role` entirely
- [x] 4.2 Update `EditStaffPage.jsx` fetching and updating logic to remove `role` mappings the fetched staff object and omit `role` entirely

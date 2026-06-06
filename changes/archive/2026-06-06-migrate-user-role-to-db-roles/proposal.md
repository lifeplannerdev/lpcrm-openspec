## Why

The backend `User` model currently has a legacy `role` field with static choices (`ROLE_CHOICES`). However, the frontend has migrated to using dynamic, database-driven roles (`db_roles`). When adding a new staff member, the frontend no longer sends the `role` field, which causes a `400 Bad Request` because the backend still enforces `role` as required. To resolve this inconsistency and fully adopt the dynamic role-based access control (RBAC) system, we must completely migrate away from the legacy `role` field.

## What Changes

- **BREAKING**: Remove the `role` field from the `User` model in `accounts/models.py`.
- **BREAKING**: Update all backend views and serializers that rely on `user.role` or `request.user.role` (e.g., `if user.role == 'ADMIN'`) to instead check `db_roles` or check for specific permissions via `AppPermission`.
- Create a database migration to remove the `role` column.
- Update `StaffCreateSerializer` and `StaffUpdateSerializer` to remove `role`.
- Remove legacy `role` properties on the `User` model (e.g., `is_business_head`, `is_cm`, `is_hr`).
- Provide alternative checks using `db_roles` for special flows like Trainer branch assignment.

## Capabilities

### New Capabilities
- `dynamic-rbac`: Full transition to database-driven roles (`db_roles`) for all authentication, authorization, and role-based logic across the backend APIs.

### Modified Capabilities
- None

## Impact

- **Models**: `accounts.User`
- **Serializers**: `accounts.serializers.StaffCreateSerializer`, `accounts.serializers.StaffUpdateSerializer`, `accounts.serializers.StaffListSerializer`, `accounts.serializers.StaffDetailSerializer`, `accounts.serializers.LoginSerializer`
- **Views**: Multiple views in `accounts/views.py` (e.g., `DashboardStatsAPIView`, `ActivityLogListView`, `StaffCreateView`, `StaffUpdateView`, `EmployeeListAPI`) that check `user.role`.
- **Database**: A migration will be created, potentially requiring data migration if we need to preserve legacy roles by automatically mapping them to `db_roles` before dropping the column.

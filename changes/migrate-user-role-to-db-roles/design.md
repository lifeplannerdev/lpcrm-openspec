## Context

The system has historically relied on a static `role` field on the `User` model (`ROLE_CHOICES` like `ADMIN`, `TRAINER`, `HR`). Recently, a dynamic role-based access control (RBAC) system (`Role` and `AppPermission` models linked to `User.db_roles`) was introduced. The frontend `AddStaffPage` and `ProfessionalInfoSection` were updated to exclusively use `db_roles` (multi-select), dropping the legacy `role` select dropdown. However, the backend still enforces `role` as required, resulting in a `400 Bad Request` when creating staff.

## Goals / Non-Goals

**Goals:**
- Eliminate the `400 Bad Request` during staff creation by removing the legacy `role` field requirement.
- Fully migrate all backend authorization checks to use the dynamic `db_roles` or `permissions`.
- Provide a clean and consistent authorization architecture across the backend.

**Non-Goals:**
- Changing the frontend UI components (they are already correct).
- Introducing new permissions or roles; we are only migrating the checks.

## Decisions

- **Drop `role` from `User` model**: We will remove the `role` field and the `ROLE_CHOICES`. This ensures no legacy code can accidentally depend on it.
- **Migration Strategy**: 
  - Before dropping the column, we will need to ensure that existing users have their legacy `role` properly mapped to a corresponding `Role` in `db_roles`. (A data migration will be written).
- **Refactoring Authorization Logic**: 
  - Change hardcoded role checks (e.g., `user.role == 'ADMIN'`) to check for specific permissions using the `PermissionService` or check if the user belongs to a specific dynamic role by name if permission checks are too granular.
  - Remove legacy properties like `is_business_head`, `is_cm`, `is_hr` or reimplement them using `db_roles.filter(name='HR').exists()`.
- **Handling Trainer Profile Logic**: 
  - In `StaffCreateView` and `StaffUpdateView`, the check `if role == 'TRAINER'` will be updated to check if `'TRAINER'` is among the names of the associated `db_roles`.

## Risks / Trade-offs

- **Risk: Missed Authorization Checks** → A view or endpoint might still rely on `user.role` which could cause a `500 Server Error` if missed. Mitigation: We will comprehensively search the codebase for `.role` access on `User` objects.
- **Risk: Data Loss during Migration** → We could lose the primary role of existing users if the data migration fails. Mitigation: The data migration will iterate over all users and assign the appropriate `Role` to `db_roles` before the schema migration drops the `role` column.

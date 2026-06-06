## 1. Serializers Updates

- [x] 1.1 Remove `role` from `StaffCreateSerializer.Meta.fields` in `accounts/serializers.py`.
- [x] 1.2 Remove `role` from `StaffUpdateSerializer.Meta.fields` in `accounts/serializers.py`.
- [x] 1.3 Remove `role` from `StaffListSerializer.Meta.fields` and `StaffDetailSerializer.Meta.fields`.
- [x] 1.4 Update `LoginSerializer` to remove legacy `role` from the returned user dictionary payload.

## 2. Views and Business Logic Updates

- [x] 2.1 Update `DashboardStatsAPIView.get` to check `if not request.user.db_roles.filter(name='ADMIN').exists():` instead of `request.user.role != "ADMIN"`.
- [x] 2.2 Update `ActivityLogListView.get_queryset` to remove checks like `user.role not in ('ADMIN', 'BUSINESS_HEAD', 'CEO')` and use `db_roles.filter(name__in=['ADMIN', ...])`.
- [x] 2.3 Update `CurrentUserAPIView` to stop returning `user.role`.
- [x] 2.4 Update `StaffCreateView.create` to check if `'TRAINER'` is in the provided `db_roles` instead of `role == 'TRAINER'`.
- [x] 2.5 Update `StaffUpdateView.update` to similarly check `db_roles` for `'TRAINER'`.
- [x] 2.6 Update `EmployeeListAPI.get` to filter by `db_roles__name__in=...` instead of `role__in=...`.
- [x] 2.7 Update any other files in `accounts/views.py` referencing `.role` on `User`.

## 3. Database Migration

- [x] 3.1 Create a data migration in `accounts` to iterate over all `User` instances, fetch the corresponding `Role` matching the legacy `role` string, and add it to `user.db_roles` (if not already present).
- [x] 3.2 Remove the `role` field from the `User` model in `accounts/models.py`.
- [x] 3.3 Remove `ROLE_CHOICES` from `User` model.
- [x] 3.4 Update properties like `is_business_head`, `is_cm`, and `is_hr` to query `db_roles` instead of `role`.
- [x] 3.5 Generate and apply the schema migration (`makemigrations` and `migrate`).

## 4. Verification

- [x] 4.1 Test staff creation from the frontend without the legacy `role` field to verify the `400 Bad Request` is gone.
- [x] 4.2 Verify Dashboard Stats still restrict access properly to Admins.
- [x] 4.3 Verify Trainer branch assignment still works correctly during staff creation and update.

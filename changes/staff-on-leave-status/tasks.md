## 1. Backend Updates

- [x] 1.1 Add `is_on_leave = models.BooleanField(default=False)` to the `User` model in `accounts/models.py`.
- [x] 1.2 Generate and apply the database migrations for the new field.
- [x] 1.3 Update `StaffListSerializer` and `StaffDetailSerializer` in `accounts/serializers.py` to include `is_on_leave`.
- [x] 1.4 Update `StaffListView.get_queryset` in `accounts/views.py` to handle `status=on_leave` by filtering `is_on_leave=True`.
- [x] 1.5 Ensure `active` status filters in `StaffListView` enforce `is_on_leave=False`.

## 2. Frontend Updates

- [x] 2.1 Update `fetchStaff` in `StaffPage.jsx` to map `status: staff.is_on_leave ? 'on_leave' : (staff.is_active ? 'active' : 'inactive')`.
- [x] 2.2 Update `StaffPage.jsx` status tabs array to include `{ id: 'on_leave', label: 'On Leave' }`.
- [x] 2.3 Update the "On Leave" stats card value in `StaffPage.jsx` to dynamically count staff where `s.status === 'on_leave'`.

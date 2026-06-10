## Why

Currently, the system only supports marking staff as Active (`is_active=True`) or Inactive (`is_active=False`). However, the frontend (`StaffPage.jsx`) requires an "On Leave" tab to filter staff members who are temporarily on leave. By adding an `is_on_leave` field to the backend `User` model, we can accurately track leave status without losing the active/inactive state, enabling the UI to filter correctly and correctly display their status throughout the CRM.

## What Changes

- Add `is_on_leave = models.BooleanField(default=False)` to the `User` model in `accounts/models.py`.
- Run migrations to apply this schema change to the database.
- Update `StaffListView` in `accounts/views.py` to filter `is_on_leave=True` when the `status=on_leave` query parameter is provided.
- Update `StaffPage.jsx` to include an "On Leave" tab and pass the `status=on_leave` parameter to the API.
- Update the Staff stat counters in `StaffPage.jsx` to accurately reflect the count of staff on leave.

## Capabilities

### New Capabilities
None

### Modified Capabilities
- `staff-management`: Add requirement for filtering staff by "On Leave" status based on the new `is_on_leave` field.

## Impact

- **Database**: Migration for `User` model required.
- **API**: `/api/staff/` endpoint filtering behavior will be extended to support `status=on_leave`.
- **Frontend**: The Staff Grid on `StaffPage.jsx` will support a new tab and correctly populate the `On Leave` statistics card.

## Context

The `staff-management` feature lacks an ability to filter staff who are temporarily "On Leave". The frontend Staff Grid is supposed to have an "On Leave" tab, but the backend `User` model currently only tracks boolean `is_active`, preventing us from properly tracking staff who are inactive strictly due to being on leave versus those who have departed.

## Goals / Non-Goals

**Goals:**
- Introduce `is_on_leave` field to `User` model.
- Extend backend staff filtering to support `status=on_leave` using this new field.
- Add an "On Leave" tab to the frontend `StaffPage.jsx`.
- Update dashboard and page statistics to report "On Leave" count correctly.

**Non-Goals:**
- Do not migrate `is_active` to a string-based `status` choice field, as this would require extensive refactoring of Django's default authentication backend behaviors. A separate boolean is safer.

## Decisions

- **Add `is_on_leave` BooleanField**: Instead of converting `is_active` into a string status, we will add an independent `is_on_leave` boolean. This integrates cleanly with Django's `AbstractUser` without breaking built-in auth mechanics.
- **Frontend Filter Logic**: The frontend will pass `status=on_leave` and the backend will map this to `is_on_leave=True`. The "active" status will map to `is_active=True` and `is_on_leave=False`, while "inactive" remains `is_active=False`.

## Risks / Trade-offs

- **Risk**: Other queries might still count `is_on_leave=True` as fully "active" if they only check `is_active=True`.
  - **Mitigation**: We will review `EmployeeListAPI` and other staff aggregations to ensure `is_on_leave` is excluded where appropriate.

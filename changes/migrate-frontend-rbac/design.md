## Context

The backend recently migrated its User roles implementation from a single `role` field to a robust Many-to-Many RBAC field named `db_roles`. The `role` field was subsequently removed from the Django `User` model. This causes 500 Internal Server errors anywhere serializers try to include `'role'`. The frontend relies heavily on `role` for rendering user titles, deciding which actions are allowed, and processing staff creation and update forms. 

## Goals / Non-Goals

**Goals:**
- Completely remove the `role` field from all affected backend serializers.
- Refactor the React frontend to seamlessly adapt to the new `db_roles` (or `role_names`) format.
- Ensure `AddStaffPage` and `EditStaffPage` function correctly using arrays of roles rather than single string role assignments.
- Update UI components (like `DashboardOverview` and `StaffDetailsPage`) to render arrays of roles correctly.

**Non-Goals:**
- Complete redesign of the frontend styling.
- Adding new roles to the database.
- Modifying backend views except for serializer `Meta.fields`.

## Decisions

- **Remove `role` from Backend Serializers**: `leads`, `tasks`, `trainers`, and `hr` app serializers will have `'role'` removed from their `fields`.
- **Frontend Role Extraction**: The frontend will rely on `role_names` (an array of strings returning the role names, which is already present on `user` objects) for rendering UI texts (e.g., `user.role_names.join(', ')`).
- **Frontend Form Adjustments**: In `AddStaffPage` and `EditStaffPage`, the `formData` will exclusively use `db_roles` array (list of role IDs) for form submission and validation, ignoring `formData.role`.
- **Permission Checking**: The frontend will use `.some()` or `.includes()` on `role_names` to replace direct equality checks `user.role === 'ADMIN'`.

## Risks / Trade-offs

- **Risk**: Some parts of the frontend might have hardcoded legacy role mappings that break if `role_names` has a slightly different casing or naming.
  **Mitigation**: We will ensure `.toUpperCase()` or `.toLowerCase()` is used universally when doing array checks, mirroring previous logic.
- **Risk**: Removing `role` from the API response might break components that aren't updated.
  **Mitigation**: A comprehensive search for `role` in the `src` directory will be used to ensure all access points are refactored.

## Context

The backend uses a `PermissionService` that parses user permissions. This service explicitly drops any permission string that does not contain a colon (`:`). Because of this, legacy permission strings like `view_staff_reports` or `manage_asset` are never sent to the frontend.
The `Role Management` UI reads all `AppPermission` records from the database and allows administrators to assign these legacy strings. However, because they are stripped out by the backend later, checking these boxes in the UI has no effect on the user's actual access to those features.

To fix this disjoint, we must transition the entire application to the RBAC format (`<resource>:<action>`).

## Goals / Non-Goals

**Goals:**
- Convert all existing legacy permission strings in the database to the `resource:action` format (e.g., `reports:read_all`, `assets:manage`).
- Update `seed_roles.py` and `permission_templates.py` to seed only `<resource>:<action>` formatted strings.
- Ensure the frontend UI navigation and `PermissionRoute` wrappers correctly check for the new resource scopes.
- Write a Django data migration to automatically rename existing `AppPermission` records so existing roles maintain their access levels seamlessly.

**Non-Goals:**
- We are not changing the core logic of `PermissionService` (it will continue dropping non-colon strings, which is fine since all strings will now have colons).
- We are not restructuring the frontend `PermissionsContext` logic.

## Decisions

- **Django Data Migration:** Rather than just updating the seed file, we will create an explicit data migration `RunPython` script to rename `AppPermission` rows. This ensures that any roles (even custom ones created by admins) that were assigned `manage_asset` will automatically get `assets:manage`.
- **Naming Conventions:**
  - `view_my_reports` -> `reports:read_own`
  - `view_staff_reports` -> `reports:read_all`
  - `view_all_tasks` -> `tasks:read_all`
  - `view_my_tasks` -> `tasks:read_own`
  - `edit_tasks` -> `tasks:edit_any`
  - `manage_asset` -> `assets:manage`
  - `view_asset` -> `assets:read_any`
  - `view_staff_assets` -> `assets:read_tenant`
  - `edit_penalties` -> `penalties:edit_any`
  - `view_penalties` -> `penalties:read_any`
  - `view_candidates` -> `candidates:read_any`
  - `edit_candidates` -> `candidates:edit_any`
  - `view_overview` -> `dashboard:read`
  - `view_staff` -> `staff:read_tenant`
  - `edit_staff` -> `staff:edit_any`
  - `delete_staff` -> `staff:delete_any`
  - `view_leads` -> `leads:read_tenant`
  - `view_students` -> `students:read_tenant`
  - `edit_students` -> `students:edit_any`
  - `view_fees` -> `fees:read_tenant`
  - `manage_fees` -> `fees:manage`
  - `restructure_fees` -> `fees:restructure`
  - `record_partial_payment` -> `fees:partial_payment`
  - `issue_fee_notice` -> `fees:issue_notice`
  - `view_fee_reports` -> `fees:view_reports`
  - `mark_attendance` -> `attendance:mark`
  - `view_attendance_docs` -> `attendance:view_docs`
  - `view_voxbay` -> `voxbay:read`
  - `access_flag` -> `staff:access_flag`
  - `edit_staff_contact_logic` -> `staff:edit_contact_logic`

## Risks / Trade-offs

- **Risk: Breaking existing custom roles or frontend views.**
  - *Mitigation:* The data migration will carefully map the exact old string to the exact new string. We will do a full text search (`git grep`) across both frontend and backend repositories to ensure no lingering references to the old strings remain.

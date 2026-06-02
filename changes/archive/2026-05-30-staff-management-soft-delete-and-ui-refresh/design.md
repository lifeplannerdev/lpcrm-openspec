## Context

The system currently allows hard deletion of staff members. This has resulted in data integrity issues where historical activities or leads assigned to a deleted staff member reference a null or non-existent user. To fix this, we are shifting to a "soft delete" model where staff can be made "inactive" but their records persist. At the same time, the staff management UI needs a "premium" visual upgrade, including dynamic micro-animations, refined colors, and highly optimized layouts.

## Goals / Non-Goals

**Goals:**
- Replace staff hard deletion with soft deletion (inactive toggle).
- Prevent inactive staff from authenticating.
- Upgrade the visual aesthetics of the "Staff Management", "Edit Staff Member", and "Permissions" modals to a premium standard.
- Ensure all filters, searches, and buttons function flawlessly and performantly.

**Non-Goals:**
- Re-architecting the entire granular permissions engine (just the UI).
- Adding new roles or changing the core role-based access control (RBAC).

## Decisions

- **Database Approach:** Rely on Django's built-in `is_active` flag for the User model rather than a custom `deleted_at` field. This instantly integrates with Django's authentication backends to prevent login.
- **API Strategy:** Modify the DELETE endpoint for staff to return a 405 Method Not Allowed, or remove it entirely. The Update (PATCH) endpoint will be the sole mechanism for toggling `is_active`.
- **UI Design System:** Use modern layout primitives (glassmorphism accents, shadow-sm, rounded-2xl cards) combined with headless components for robust filtering and toggles.
- **Frontend State:** Staff lists will filter out inactive users on the main view by default, but provide an "Inactive" tab for viewing soft-deleted profiles.

## Risks / Trade-offs

- **Risk:** Existing queries throughout the app might not check `is_active=True`, causing inactive users to appear in dropdowns (like lead assignment).
  - **Mitigation:** Conduct a rigorous audit of all user-fetching endpoints (e.g., `/api/employees/list/`, `/api/leads/available-users/`) to ensure they filter `is_active=True`.
- **Risk:** Admin might still need a way to permanently purge test users.
  - **Mitigation:** Accept this trade-off for now; database admins can purge via shell if absolutely necessary. The UI will strictly enforce soft deletes.

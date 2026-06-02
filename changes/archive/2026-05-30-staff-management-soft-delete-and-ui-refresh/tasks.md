## 1. Backend Modifications

- [x] 1.1 Remove or disable DELETE endpoints for staff management to prevent hard deletion
- [x] 1.2 Update staff fetching APIs (e.g., `/api/employees/list/`, `/api/leads/available-users/`) to handle `is_active` correctly
- [x] 1.3 Ensure the Staff update (PATCH) API securely allows toggling the `is_active` field
- [x] 1.4 Update token views/serializers to explicitly reject authentication for `is_active=False` users

## 2. Frontend: Staff Management Grid & Filters

- [x] 2.1 Remove all "Delete" (trash icon) buttons from the Staff Management UI
- [x] 2.2 Upgrade Staff Grid UI with premium glassmorphism, `rounded-2xl` cards, and vibrant status badges
- [x] 2.3 Implement the "All Staff", "Active", and "Inactive" tabs to filter by `is_active` status
- [x] 2.4 Verify and optimize Search, Department, and Branch filter components

## 3. Frontend: Edit Staff & Permissions UI

- [x] 3.1 Redesign "Edit Staff Member" modal with structured sections (Personal, Professional) and premium inputs
- [x] 3.2 Ensure the "Active Status" toggle in the Edit form successfully updates the backend `is_active` flag
- [x] 3.3 Redesign the "Manage Granular Permissions" modal with clean spacing and clear, modern toggles

## 4. Validation

- [x] 4.1 Test staff deactivation and verify that the deactivated user cannot log in
- [x] 4.2 Verify that deactivated staff still render correctly in historical data (e.g., Lead Timeline)
- [x] 4.3 Ensure all new premium UI elements, filters, and tabs render flawlessly without breaking existing functionality

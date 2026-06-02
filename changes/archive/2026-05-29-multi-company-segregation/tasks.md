## 1. Database Updates

- [x] 1.1 Add `company` CharField to Task, User/Staff, Lead, Student, and Penalty models.
- [x] 1.2 Add `company` CharField to Report and Attendance models (if applicable).
- [x] 1.3 Create and run Django migrations, setting the default value to `LP` for all existing records.

## 2. Permissions Engine Updates

- [x] 2.1 Update `accounts/permission_templates.py` to include `access_flag` for ADMIN, CEO, HR, and CM roles (who are natively LP employees).
- [x] 2.2 Run `python manage.py migrate_permissions` to seed this new permission to existing executive users.

## 3. Backend API Filtering

- [x] 3.1 Create `CompanyFilterMixin` in the backend that intercepts `get_queryset`, extracts `?company=` parameter, validates access (user's own company OR `access_flag`), and filters by `company`.
- [x] 3.2 Apply `CompanyFilterMixin` to TaskViewSet, StaffViewSet, LeadViewSet, and other core ViewSets.
- [x] 3.3 Ensure validation logic in serializers requires a valid company when creating records, matching the user's permitted companies.

## 4. Frontend UI Components

- [x] 4.1 Create a reusable `CompanySwitcher` React component.
- [x] 4.2 Integrate `CompanySwitcher` into the TopNav or individually on page headers.
- [x] 4.3 Update API interceptors or service functions to append `?company=` when the switcher state changes.
- [x] 4.4 Update `StaffPage.jsx`, `TasksPage.jsx`, etc., to reload data when the selected company changes.

## 5. Frontend Integration

- [x] 5.1 Integrate `CompanySwitcherTab` into `StaffPage.jsx`, updating local state and appending `?company=` to fetch calls.
- [x] 5.2 Integrate `CompanySwitcherTab` into `TaskKanban.jsx` and `LeadsPage.jsx` (if applicable).
- [x] 5.3 Update "Add Staff" and "Edit Staff" modals to conditionally show a "Company" dropdown if the user has dual access.
- [x] 5.4 Update "Add Task" modal to show a "Company" dropdown and filter potential assignees based on the selected company.

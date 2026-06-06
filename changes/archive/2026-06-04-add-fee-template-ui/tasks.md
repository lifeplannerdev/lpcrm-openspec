## 1. UI Components Setup

- [x] 1.1 Add a "Create Template" button to `FeesManagementPage.jsx`, visible only if `canManageFees` is true.
- [x] 1.2 Create a state variable for managing the template creation modal (`isTemplateModalOpen`).
- [x] 1.3 Create a state variable for the new template form data (`newTemplateForm`).

## 2. Modal Implementation

- [x] 2.1 Implement the basic modal structure for creating a template.
- [x] 2.2 Add form inputs for `company` (defaulting to the current company context), `code`, `name`, and `plan_type` (select).
- [x] 2.3 Add dynamic fields based on `plan_type`:
  - If `ONE_TIME` or `PACKAGE`: show `total_amount`.
  - If `INSTALLMENT`: show `total_amount`, `installment_count`, `installment_amount`.
  - If `MONTHLY`: show `total_amount`, `registration_amount`, `monthly_amount`, `duration_months`, `due_day`.
- [x] 2.4 Add form inputs for `course_label` and `notes`.

## 3. Integration

- [x] 3.1 Implement a `handleCreateTemplate` function that submits the `newTemplateForm` data via POST to `${API_BASE_URL}/fees/catalog/`.
- [x] 3.2 Ensure the modal closes, resets the form, and shows an error or success message.
- [x] 3.3 After successful creation, re-fetch the template catalog (`fetch(`${API_BASE_URL}/fees/catalog/...`)`) and update the `templates` state so the new template is immediately available in the dropdown.

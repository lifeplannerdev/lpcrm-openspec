## Context

The system supports `AcademicBatch` which allows admins to group students. During student enrollment (`AddStudentPage.jsx`), an admin selects the `AcademicBatch` and then manually selects a `FeePlanTemplate`. To streamline operations, the system should allow assigning a default fee template directly to the `AcademicBatch` so that it auto-selects during enrollment.

Since LP does not have students or batches (it only goes up to Leads), `AcademicBatch` is exclusively used by the FLAG company. Therefore, linking a global `AcademicBatch` to a company-scoped `FeePlanTemplate` (FLAG) is safe.

## Goals / Non-Goals

**Goals:**
- Add `default_fee_template` to `AcademicBatch`.
- Update API serializers to expose the new field.
- Update `AcademicBatchesPage.jsx` to allow selecting the default fee template.
- Update `AddStudentPage.jsx` to pre-select the fee template when a batch is chosen.

**Non-Goals:**
- We are not adding a `company` field to `AcademicBatch` at this time, as business logic dictates it is exclusively used for FLAG.
- We are not enforcing that the student MUST use the default fee template; it is only a suggestion/pre-selection.

## Decisions

- **ForeignKey with `SET_NULL`:** The `default_fee_template` field on `AcademicBatch` will be a ForeignKey to `fees.FeePlanTemplate` with `on_delete=models.SET_NULL`. This ensures that if a fee template is deleted or deactivated, the batch is not deleted along with it.
- **Frontend Pre-selection:** In `AddStudentPage.jsx`, an `onChange` handler for the Academic Batch dropdown will inspect the selected batch's `default_fee_template` value and update the fee template dropdown state automatically.

## Risks / Trade-offs

- **Risk:** An admin might select a deactivated fee template.
  - **Mitigation:** The frontend `AcademicBatchesPage.jsx` dropdown will only display `is_active=True` fee templates for selection.
- **Risk:** Cross-company data leak if LP tries to create batches.
  - **Mitigation:** LP does not manage students/batches based on the established RBAC business rules, so this is a non-issue in production.

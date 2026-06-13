## 1. Backend Updates

- [x] 1.1 Add `default_fee_template` ForeignKey to `fees.FeePlanTemplate` (with `on_delete=models.SET_NULL`, `null=True`, `blank=True`) to the `AcademicBatch` model in `trainers/models.py`.
- [x] 1.2 Generate and apply the database migrations for the new field (`makemigrations trainers` and `migrate trainers`).
- [x] 1.3 Update `AcademicBatchSerializer` in `trainers/serializers.py` to include the `default_fee_template` field.

## 2. Frontend Updates

- [x] 2.1 Update `AcademicBatchesPage.jsx` to fetch active fee templates from the backend API.
- [x] 2.2 Update the Create/Edit Academic Batch form/modal in `AcademicBatchesPage.jsx` to include a select dropdown for `default_fee_template`.
- [x] 2.3 Ensure the `AcademicBatchesPage.jsx` submission logic correctly sends the `default_fee_template` ID to the backend.
- [x] 2.4 Update `AddStudentPage.jsx` to automatically set the `fee_template` field when a user selects an `academic_batch` that has a `default_fee_template` configured.

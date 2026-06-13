## Why

Currently, when an admin adds a student and selects an Academic Batch, they must manually search for and select the corresponding fee template. To streamline enrollment and reduce errors, the system should automatically suggest or pre-select the correct default fee template associated with the chosen academic batch.

## What Changes

- Add a `default_fee_template` ForeignKey to the `AcademicBatch` model in the backend.
- Expose `default_fee_template` in the `AcademicBatchSerializer` API response.
- Update the frontend `AcademicBatchesPage.jsx` to include a dropdown for selecting the default fee template when creating or editing a batch.
- Update the frontend `AddStudentPage.jsx` to pre-select the default fee template when the user selects an academic batch during enrollment.

## Capabilities

### New Capabilities
None.

### Modified Capabilities
- `academic-management`: The system must support configuring a default fee template on an academic batch and surfacing it as the suggested fee plan during student enrollment.

## Impact

- **Backend Models:** `AcademicBatch` in `trainers/models.py`.
- **Backend Serializers:** `AcademicBatchSerializer` in `trainers/serializers.py`.
- **Frontend Pages:** `AcademicBatchesPage.jsx` and `AddStudentPage.jsx`.

## 1. Database and Models

- [x] 1.1 Create `Asset` model in `hr/models.py` with fields: name, type, serial_number, status, company, assigned_to (FK to User), and attachment (CloudinaryField).
- [x] 1.2 Run `makemigrations` and `migrate` to create the new asset tables in the database.
- [x] 1.3 Verify that default Django permissions (`view_asset`, `add_asset`, `change_asset`, `delete_asset`) are correctly generated for the new model.

## 2. Backend API and Views

- [x] 2.1 Implement an API ViewSet/endpoints for the `Asset` model supporting CRUD operations.
- [x] 2.2 Ensure the Asset API filters results properly based on the `company` field (LP vs FLAG) and enforces access permissions.
- [x] 2.3 Update the existing Staff Profile/Details API view (e.g., in `accounts/views.py` or `hr/views.py`) to include a serialized list of attached assets for the given staff member.
- [x] 2.4 Expose the new asset permissions in the list of available permissions returned to the frontend for the Permission Assign Screen.
- [x] 5.1 Verify that the backend endpoints are secure and correctly scope returned data based on the Company flag ("LP" vs "FLAG").
- [x] 5.2 Finalize UI walkthrough and verify all form validations work appropriately without errors.

## 3. Frontend - Asset Management UI

- [x] 3.1 Create the primary Asset Management page with a premium, engaging UI (incorporating glassmorphism, hover states, and clear typography).
- [x] 3.2 Implement the top-level "LP" and "FLAG" company separation tabs to toggle the displayed asset lists.
- [x] 3.3 Build the Add/Edit Asset modal or form, including fields for uploading attachments and a searchable dropdown for `assigned_to`.

## 4. Frontend - Staff Integration

- [x] 4.1 Modify the Staff Profile/Details component to include an "Assigned Assets" section displaying the fetched asset list.
- [x] 4.2 Update the Staff Permission Assignment screen (modal or page) to ensure the newly exposed Asset permissions (`view_asset`, `manage_asset`) appear as toggleable options.

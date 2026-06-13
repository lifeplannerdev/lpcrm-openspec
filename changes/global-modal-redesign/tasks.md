## 1. Asset Management Modal Redesign

- [x] 1.1 Update `AssetManagementPage.jsx` Add/Edit Asset Modal to use fixed container (`max-h-[90vh]`) and internal scroll (`overflow-y-auto` on form body).
- [x] 1.2 Move Save/Cancel buttons to a fixed footer in the Asset Modal.
- [x] 1.3 Tighten vertical paddings (e.g., `py-2.5` to `py-2`) for input fields in the Asset Modal.

## 2. Lead Management Modal Redesign

- [x] 2.1 Update `LeadsPage.jsx` Add/Edit Lead Modal to use fixed container and internal scroll.
- [x] 2.2 Move Save/Cancel buttons to a fixed footer in the Lead Modal.
- [x] 2.3 Tighten vertical paddings for input fields in the Lead Modal.

## 3. Fees Management Modal Redesign

- [x] 3.1 Update `FeesManagementPage.jsx` Add/Edit Fees Modal to use fixed container and internal scroll.
- [x] 3.2 Move Save/Cancel buttons to a fixed footer in the Fees Modal.
- [x] 3.3 Tighten vertical paddings for input fields in the Fees Modal.

## 4. Candidate Details Modals Redesign

- [x] 4.1 Update Edit Candidate Modal in `CandidateDetailPage.jsx` to use fixed container and internal scroll.
- [x] 4.2 Update Add Payment Modal in `CandidateDetailPage.jsx` to use fixed container and internal scroll.
- [x] 4.3 Move action buttons to fixed footers in both modals.

## 5. Role & Task Modals Redesign

- [x] 5.1 Update `RoleManagementPage.jsx` Edit Role/Permissions Modal to use fixed container and internal scroll.
- [x] 5.2 Update `TaskViewPage.jsx` Create Task Modal to use fixed container and internal scroll.

## 6. Miscellaneous Modals Redesign

- [x] 6.1 Identify any remaining modals (e.g., Attendance Docs, Credentials) and apply the same structural redesign.
## 7. Branch Management Implementation

- [x] 7.1 Create `Branch` model in `hr/models.py` and update `Location` model with a foreign key to `Branch`.
- [x] 7.2 Create migrations and run them.
- [x] 7.3 Update `hr/views.py` and `hr/serializers.py` to expose `Branch` APIs and include branch details in `Location` responses.
- [x] 7.4 Update frontend `AssetManagementPage.jsx` to fetch Branches.
- [x] 7.5 Update frontend UI in Space Inventory to group/filter Locations by Branch (e.g., adding a "Branch" dropdown or tabs).
- [x] 7.6 Assign existing locations to "Kochi Office" by default.

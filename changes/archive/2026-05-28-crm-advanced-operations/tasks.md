## 1. Database & Models

- [x] 1.1 Create `Branch` model and add `ForeignKey` to `Trainer` and `Student`.
- [x] 1.2 Create `ExamResult` model linking `Student`, `AcademicBatch`, `exam_type` (Model vs Final), and `score`.
- [x] 1.3 Create `WebhookLog` model to store incoming payloads from Voxbay and Meta Ads for debugging and retry mechanisms.
- [x] 1.4 Generate and apply Django migrations.

## 2. Integrations (Webhooks)

- [x] 2.1 Implement `/api/webhooks/meta/` endpoint with signature validation.
- [x] 2.2 Implement Meta webhook logic to map payload data and create `Lead` records automatically.
- [x] 2.3 Implement `/api/webhooks/voxbay/` endpoint.
- [x] 2.4 Implement Voxbay webhook logic to auto-schedule a follow-up task when a call log is received for an existing Lead.

## 3. API Updates

- [x] 3.1 Update `Student` and `Trainer` endpoints to accept and expose `branch`.
- [x] 3.2 Update list endpoints (Students, Trainers, Attendance) to accept a `branch_id` query parameter for filtering.
- [x] 3.3 Create endpoints for creating, updating, and fetching `ExamResult` objects per Academic Batch.
- [x] 3.4 Add an endpoint to convert a Voxbay call log record into a new `Lead`.

## 4. Frontend: Branch & Academic UI

- [x] 4.1 Update `AddTrainer` and `AddStudent` forms with a `Branch` dropdown.
- [x] 4.2 Update Students and Attendance pages to include a global Branch filter dropdown.
- [x] 4.3 Update `AcademicBatchesPage` UI to support adding and viewing "Marks Achieved" via `ExamResult` API.
- [x] 4.4 Add tabbed interface to `StudentsPage` (Active, Paused, Dropped, Completed) and `StaffPage` (Active, Inactive).

## 5. Frontend: Advanced Filtering & Exports

- [x] 5.1 Update Tasks (Kanban) to support multi-select date filtering (Today, Yesterday, Specific Date).
- [x] 5.2 Implement CSV download functionality for active table/grid views on the frontend.
- [x] 5.3 Implement PDF download functionality for active table/grid views using `jspdf` and `html2pdf`.
- [x] 5.4 Update Reports list to visually flag rows (e.g. red background or tag) if Morning Agenda > 10:30 AM or Evening Report > 6:00 PM.

## 1. Database & Schema Updates

- [x] 1.1 Add `personal_phone` and `office_phone` fields to the Staff model/schema.
- [x] 1.2 Update the Academic Batch schema to reference an `academic_year` and include `admission_date`, `model_exam_date`, and `final_exam_date`.
- [x] 1.3 Add `report_type` (Morning/Evening), `submission_time`, and `next_day_agenda` fields to the Reports schema.

## 2. API Backend Adjustments

- [x] 2.1 Update Staff creation/editing endpoints to accept and validate the new phone fields.
- [x] 2.2 Update Academic endpoints to support nested batch queries (Academic Year -> Grade) and date saving.
- [x] 2.3 Enhance the Attendance API to support batch updating statuses, advanced filtering (trainer, location), and querying non-dropout students.
- [x] 2.4 Create a Reports endpoint that auto-timestamps submissions and fetches previous evening's `next_day_agenda` for new Morning reports.

## 3. Task Management (Kanban)

- [x] 3.1 Install a drag-and-drop library (e.g., `react-beautiful-dnd` or `dnd-kit`).
- [x] 3.2 Refactor the Tasks page to map tasks into dynamic columns based on status.
- [x] 3.3 Implement drag-and-drop handlers to trigger backend status update APIs upon card movement.

## 4. Attendance Page Enhancements

- [x] 4.1 Update `StudentAttendanceRecordsPage` or related components to expose trainer and location filters.
- [x] 4.2 Support bulk selection/action for marking attendance (passing array of `{student_id, status}` to the updated API).
- [x] 4.3 Add a "Mark All Present" toggle and tie it to the batch update API.

## 5. Daily Reporting Flow

- [x] 5.1 Implement a report type selector (`MORNING` vs `EVENING`).
- [x] 5.2 Fetch and display `next_day_agenda` when opening a new MORNING report.
- [x] 5.3 Ensure submission records `submission_time` for late-entry tracking.
- [x] 5.4 Display submission lateness flags based on the automatically recorded server timestamp.

## 6. Academic Section UI

- [x] 6.1 Update the Students/Academics pages to display grouped structure (`Academic Year -> Grade -> Batch/Students`).
- [x] 6.2 Bind the new Academic Batch creation endpoint to the UI (capturing name, year, and dates).
- [x] 6.3 Update the frontend models/components for creating a student to attach an `academic_batch` instead of a plain text string.

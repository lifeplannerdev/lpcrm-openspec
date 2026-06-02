## Context

The current CRM lacks certain usability features (like drag-and-drop task management) and has incomplete tracking mechanisms for academic scheduling, advanced attendance filtering, and daily staff reporting. We need to upgrade these systems without breaking the existing core functionality.

## Goals / Non-Goals

**Goals:**
- Add personal/office phone number tracking to staff data.
- Integrate a drag-and-drop Kanban view into the Tasks page, keeping all existing task functionality.
- Structure academic batches by Academic Year -> General/Grade hierarchy and track model/final exam dates.
- Add advanced filtering to the Attendance page, toggle-based full-list attendance, and exclude dropout students.
- Support new "Morning Agenda" and "Evening Report" types with timestamps to flag late submissions. Add carry-over logic for "Next Day's Agenda".

**Non-Goals:**
- Completely rewriting the underlying Task management engine or Attendance database (just extending them).
- Modifying UI components outside of the specified pages.

## Decisions

- **Task Kanban:** We will use a standard frontend drag-and-drop library (e.g., `react-beautiful-dnd` or `dnd-kit` depending on the framework) to render the Kanban view on top of the existing task data schema.
- **Reporting Timestamps:** The backend will automatically timestamp Morning and Evening reports upon creation to enforce lateness checks server-side (preventing client-side tampering).
- **Academic Hierarchy:** Update the Batch schema to include references for Academic Year, enabling nested querying. Admission and Exam dates will be stored as ISO-8601 strings or proper Date objects.
- **Toggle Attendance:** A single "Mark All" toggle will update state on the frontend for visible, non-dropout students before batch submitting to the backend API.

## Risks / Trade-offs

- [Risk] Performance issues on the Kanban board with a massive amount of tasks. → Mitigation: Implement lazy loading or pagination within the Kanban columns.
- [Risk] Data inconsistencies when modifying batch hierarchies. → Mitigation: Perform careful database migrations ensuring existing flat batches are assigned to default academic years.

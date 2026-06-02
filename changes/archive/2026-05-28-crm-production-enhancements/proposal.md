## Why

The CRM needs enhancements to improve usability, better manage academic data, and improve the daily tracking and reporting for staff and students. This includes a more intuitive Kanban-style task management, robust academic tracking and scheduling, streamlined toggle-based attendance, and better daily reporting with late entry tracking and agenda carry-over.

## What Changes

- **Staff Management:** Add distinct fields for "Personal Phone Number" and "Office Phone Number".
- **Task Management:** Convert the task page to a Kanban-style interface with drag-and-drop support while retaining existing functionality.
- **Academic Management:** Revamp the section to support batches based on Academic Year and then General/Grade. Add tracking for Admission Date, Model Exams Date, and Final Exams Date.
- **Attendance:** Introduce comprehensive filtering (by trainer, location, etc.), handle student status to exclude dropouts, and implement a toggle-based attendance system for all students on the page.
- **Reports:** Expand report options to include "Morning Agenda" and "Evening Report" (currently only "Add Report" exists). Both must capture timestamp to flag late entries. Add an optional "Next Day's Agenda" field that automatically populates the following morning's agenda.

## Capabilities

### New Capabilities
- `task-kanban`: Implement drag-and-drop Kanban interface for task management.
- `advanced-attendance`: Implement toggle-based attendance with advanced filtering and student status exclusion (e.g. dropouts).
- `daily-reporting`: Morning/Evening agenda and report tracking with automatic late flags and next-day agenda carry-over.

### Modified Capabilities
- `staff-management`: Adding new phone number fields.
- `academic-management`: Batch hierarchy (academic year -> grade) and exam date tracking.

## Impact

- Database schema updates for staff (phone numbers), academics (dates, batch structure), attendance, and reports.
- Frontend UI revamps on the Task Page (Kanban integration), Attendance Page, Academic Section, and Reports Page.
- Backend API adjustments to support new report types, agenda carry-over, and attendance filtering.

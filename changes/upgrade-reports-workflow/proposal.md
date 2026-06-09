## Why

The current daily reports system is rigid, relying on a single submission timestamp and offering no granular insight into an employee's compliance with daily planning. Because "Tomorrow's Agenda" is treated as optional text appended to today's report, there is no way to strictly enforce and track when employees plan their next day versus when they report on their current day. This change introduces a policy-driven, continuous workflow where the admin can define strict, individualized deadlines for both the Agenda and the Report, and the UI visually gamifies completion into clear progress steps.

## What Changes

- **BREAKING**: Replaced single `heading` field on `DailyReport` with `report_heading` and `agenda_heading`.
- **BREAKING**: Replaced single `submission_time` with independent `report_submitted_at` and `agenda_submitted_at` timestamps to accurately calculate lateness per action.
- Added `ReportTimingSettings` model to allow admins to assign custom report policies (`EVENING_BEFORE` or `MORNING_OF`) and strict time deadlines per employee.
- Overhauled the "Add Report" frontend modal to reflect a continuous loop (Morning Agenda -> Evening Report) with a 50%/100% completion progress bar.
- Implemented smart pre-filling: If an employee submitted "Next Day's Agenda" yesterday, today's "Morning Agenda" is automatically marked as complete.
- Added new visual filter flags (e.g., "Late Agenda", "Late Report", "Incomplete", "On-Time") to both the Employee and Admin Reports pages for immediate compliance tracking.

## Capabilities

### New Capabilities
None.

### Modified Capabilities
- `reports-and-exports`: Transforms the basic daily reporting flow into a multi-step, policy-enforced compliance workflow with admin-configurable deadlines.

## Impact

- **Backend Models**: Requires database migration to update `DailyReport` fields (`report_heading`, `agenda_heading`, `report_submitted_at`, `agenda_submitted_at`, `completion_percentage`) and a new `ReportTimingSettings` model.
- **Backend API Views**: `DailyReportCreateView` and `MyDailyReportUpdateView` must handle progressive saving (submitting report and agenda at different times).
- **Frontend Components**: `MyReportsPage.jsx` modal and display logic will be significantly overhauled. `ReportsPage.jsx` requires updates for new flags and data structures.
- **Admin**: New configuration screen for `ReportTimingSettings` to assign policies.

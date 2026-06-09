## 1. Backend Models & Migrations

- [x] 1.1 Create `ReportTimingSettings` model in `reports/models.py`.
- [x] 1.2 Update `DailyReport` model: rename `heading` to `report_heading`, add `agenda_heading`, add `report_submitted_at` and `agenda_submitted_at`.
- [x] 1.3 Add properties to `DailyReport` to calculate completion percentage and lateness flags.
- [x] 1.4 Generate and run Django migrations.

## 2. Backend Views & Logic

- [x] 2.1 Update `DailyReportCreateView` and `MyDailyReportUpdateView` to handle saving report vs agenda text and timestamping them accurately.
- [x] 2.2 Implement auto-carryover logic: when creating a report, check yesterday's `next_day_agenda` and pre-fill `agenda_heading` and `next_day_agenda`.
- [x] 2.3 Create admin API endpoints for fetching, updating, and assigning `ReportTimingSettings`.
- [x] 2.4 Update `AllDailyReportsView` and `MyDailyReportsView` to support filtering by new lateness flags.

## 3. Frontend: My Reports Modal

- [x] 3.1 Update `FormFields` in `MyReportsPage.jsx` to make the Name and Date/Time read-only.
- [x] 3.2 Update `MyReportsPage.jsx` modal to show the 3-step progress bar (0%, 50%, 100%).
- [x] 3.3 Update the input fields to handle `report_heading`, `report_text`, `agenda_heading`, and `next_day_agenda`.

## 4. Frontend: Admin Timings UI & Filtering

- [x] 4.1 Update `ReportsPage.jsx` (admin list) to include filter buttons/dropdowns for "Late Agenda", "Late Report", "Incomplete", and "On Time".
- [x] 4.2 Create a new config UI for admins to define the `ReportTimingSettings` for employees (or globally). Create `ReportTimingSettingsPage.jsx` or add it as a tab in Admin settings.jsx` to include new filter dropdowns for Lateness Flags (`Late Agenda`, `Late Report`, `On-Time`, `Incomplete`).
- [ ] 4.3 Update `ReportRow` and badging logic to display the new flags visually.

## 5. Verification

- [x] 5.1 Test submitting a Morning Agenda only.
- [x] 5.2 Test submitting an Evening Report only.
- [x] 5.3 Test the auto-carryover from Monday evening to Tuesday morning.

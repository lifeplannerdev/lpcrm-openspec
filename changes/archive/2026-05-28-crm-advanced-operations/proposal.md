## Why

The CRM needs to transition from a manual data-entry system to an automated, intelligent operational platform. Integrating with Voxbay and Meta Ads will automate lead ingestion and task scheduling, significantly reducing manual effort and response times. Adding branch-level visibility and advanced multi-filters with export capabilities will give management the data insights needed for scale, while new UI components (tabs, timeout flags, marks achieved) will streamline daily workflows.

## What Changes

- **Voxbay Integration**: Auto-ingest call logs, allow 1-click lead conversion, and automatically queue follow-up tasks when calls happen.
- **Meta Ads Integration**: Connect Facebook/IG Lead Ads via webhooks to auto-create leads instantly in the CRM.
- **Branch Management**: Introduce a "Branch" entity (e.g., Kottayam, Kochi) assigned to Trainers and Students, with branch-wise filtering across the system.
- **Advanced Filtering & Exports**: Add multi-date filters (Today, Yesterday, Custom) to Tasks and Reports, along with PDF/Excel export functionalities for filtered views.
- **Reporting Timeouts**: Flag morning agendas submitted after 10:30 AM and evening reports missing by 6:00 PM for easy auditing.
- **Academic Updates**: Add "Marks Achieved" tracking for model and final exams, and introduce tabbed views to cleanly separate Active/Inactive/Dropped students and staff.

## Capabilities

### New Capabilities
- `voxbay-integration`: Auto-ingest call logs, 1-click lead conversion, and automated follow-up task generation.
- `meta-ads-integration`: Webhook endpoints to directly ingest Facebook and Instagram Lead Ads into the CRM.
- `branch-management`: Core location/branch entity allowing trainers and students to be segmented by branch (e.g., Kochi, Kottayam).
- `data-exports`: System-wide capabilities for advanced multi-filtering and exporting grid/table data to PDF and Excel formats.

### Modified Capabilities
- `academic-management`: Add "Marks Achieved" (Exam Results) tracking and UI tabs for separating active/dropped students.
- `staff-management`: Add UI tabs for separating active/inactive staff.
- `daily-reporting`: Add logic to flag submissions that violate timeout constraints (Morning > 10:30 AM, Evening > 6:00 PM).
- `task-kanban`: Add multi-date filtering (Today, Yesterday, Specific Date) to the task board view.

## Impact

- **Database**: New models for `Branch`, `ExamResult` (Marks), and webhooks logging. Updates to `Student`, `Trainer`, `Lead` models to link branches and ingestion sources.
- **Backend API**: New webhook ingestion endpoints for Voxbay and Meta. Export generation APIs (if generating Excel/PDF server-side). Complex filter queries.
- **Frontend UI**: Sweeping UI changes across multiple pages to add tabs, branch dropdowns, date filters, and export buttons.
- **Infrastructure**: Exposing a public webhook URL (via ngrok for local dev, or standard HTTPS for production) for Voxbay and Meta Ads to hit.

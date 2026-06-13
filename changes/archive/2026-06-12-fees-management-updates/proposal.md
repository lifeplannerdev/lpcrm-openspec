## Why

The current fees management system lacks critical missing UI components and backend automations defined in the specification. Specifically, there's no UI for aggregated fee summary reports, scheduled fee reminders are not running because of a missing Celery configuration, and accounting is not notified when students are enrolled without a fee plan. Implementing these features brings the codebase into compliance with the `fees-management` specification.

## What Changes

- Add a Fee Summary Dashboard to the top of `FeesManagementPage.jsx` to aggregate total due, total paid, and overdue amounts across students.
- Introduce Celery Beat for scheduled tasks to handle daily cron tasks (Specifically, fee payment reminders).
- Update `StudentSerializer.create` to explicitly notify finance users when a student is created without an assigned `fee_template_id`.

## Capabilities

### New Capabilities
- None

### Modified Capabilities
- `fees-management`: Updated to explicitly rely on `celery-beat` for scheduled reminders and defining the location of the fee summary UI in the main Fees page.

## Impact

- `lpcrmbackend-main`: Adding celery beat configurations, a new celery task for fee reminders, and updates to the `StudentSerializer.create` logic.
- `lpcrm-frontend-main`: Updates to `FeesManagementPage.jsx` to fetch from `FeeSummaryAPIView` and aggregate/display data.

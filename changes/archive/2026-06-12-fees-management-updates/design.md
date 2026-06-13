## Context

The fee management system requires a summary dashboard and scheduled notifications to keep track of missing/overdue payments. Currently, `FeesManagementPage.jsx` lacks aggregated visualizations. There is no automated schedule to remind users of due fees, and accounting is not proactively notified when students are enrolled without fee plans.

## Goals / Non-Goals

**Goals:**
- Add an aggregated Fee Summary UI to the top of `FeesManagementPage.jsx`.
- Implement Celery Beat for daily scheduled tasks, specifically for fee reminders.
- Ensure the backend (`StudentSerializer`) sends notifications to finance users for missing fee plans upon enrollment.

**Non-Goals:**
- Completely redesigning the table in `FeesManagementPage.jsx`.
- Adding new notification channels (e.g. SMS/WhatsApp) beyond the existing system for fee reminders.

## Decisions

- **UI Location**: We will place the summary dashboard at the top of `FeesManagementPage.jsx` rather than a separate report page. This keeps operations and reporting close for fee management.
- **Aggregation**: The frontend will fetch the flat summary list from `FeeSummaryAPIView` and aggregate the data (`total_due`, `total_paid`, `overdue_amount`, `balance_due`) using standard JavaScript array reduction methods. This avoids complex backend grouping changes for now.
- **Scheduling Tool**: We will leverage `celery-beat` (already available alongside Celery) to run a daily task. This aligns with standard Django/Celery architectures.
- **Notification Logic**: We will add a simple `else` branch in `StudentSerializer.create` when a `fee_template_id` is missing. We will use the existing `Notification.objects.create` helper to send alerts to the Finance role.

## Risks / Trade-offs

- **Risk**: Frontend aggregation could be slow if the number of fee accounts is extremely high.
  - **Mitigation**: The API restricts to active students, usually keeping numbers manageable per batch/company. Long-term, if performance degrades, we can shift aggregation to the database via Django `Sum` annotations.
- **Risk**: Celery Beat adds another daemon to the infrastructure.
  - **Mitigation**: Standardize deployment scripts to ensure the celery beat worker is started alongside the main celery worker.

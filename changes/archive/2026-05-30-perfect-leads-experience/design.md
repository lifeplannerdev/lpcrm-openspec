## Context

The current Leads Management System has a monolithic view architecture and a standard page-based UI. To handle increasing load and provide a premium "wow" user experience, we need to optimize data loading, implement a visual drag-and-drop Kanban pipeline, a split-pane Command Center, and modularize the backend. The Pusher notification system will remain for assignments, but scheduled background follow-up reminders are explicitly out of scope due to serverless constraints.

## Goals / Non-Goals

**Goals:**
- Implement a split-pane "Command Center" for the main Leads page.
- Implement a Kanban board for leads visualization.
- Refactor `leads/views.py` into multiple focused modules.
- Optimize the bulk upload API endpoint using `bulk_create` for performance.
- Improve form aesthetics and UX using Headless UI / Radix primitives.

**Non-Goals:**
- Moving away from the current Vercel deployment model.
- Implementing scheduled background cron jobs/Celery for Pusher reminders (explicitly excluded).
- Changing the underlying authentication mechanism.

## Decisions

- **Modular Backend Views**: Split `leads/views.py` into `leads.py`, `assignments.py`, `followups.py`, and `uploads.py`.
  - *Rationale*: Maintains code readability and follows SRP (Single Responsibility Principle). The current 1000+ line file is difficult to maintain.
- **Bulk Upload Optimization**: Utilize Django's `bulk_create` and pre-fetch phone numbers for O(1) in-memory duplicate checking.
  - *Rationale*: A `for` loop executing a DB transaction for every row in a 5,000 row Excel file risks timing out on serverless environments.
- **UI Architecture**: Adopt a split-pane layout component for desktop, where the list is on the left and detail view slides in on the right.
  - *Rationale*: Minimizes context switching.
- **Kanban Implementation**: Use `dnd-kit` or similar modern React drag-and-drop library.
  - *Rationale*: Provides fluid animations and accessible drag-and-drop mechanics.

## Risks / Trade-offs

- [Risk] Changing `BulkLeadUploadView` to `bulk_create` skips the `save()` method on individual models. → Mitigation: Ensure any signal-like logic (like Pusher notifications and ActivityLogs) is explicitly handled in bulk operations.
- [Risk] Splitting `views.py` causes circular imports if models/serializers are overly intertwined. → Mitigation: Define clear boundaries and only import models/serializers at the top level of each new view file.

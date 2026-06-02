## Why

The current Leads module is functional but operates like a static data-entry CRM. To scale and empower the sales team, we are upgrading the Lead Detail page into a proactive "Lead Command Center." This establishes a clean, unified, and highly optimized foundation that easily supports advanced future integrations like Voxbay and Meta webhooks, while removing technical debt and outdated code.

## What Changes

- **Lead Command Center UI**: Redesign the lead detail page to feature a Unified Activity Feed and Customer Journey Visualization.
- **Unified Activity Feed API**: A new backend API that merges `ProcessingUpdate`, `RemarkHistory`, `FollowUpHistory`, and `WebhookLog` into a single chronological timeline.
- **Customer Journey Visualization**: A frontend component visually tracking the lead from creation (e.g., Meta Ad) to conversion.
- **Follow-up Enhancements**: Introduce a Calendar View (Day/Week/Month) for follow-ups and implement an escalation system for overdue follow-ups (notifications after 24h, reassignment after 72h).
- **Collaboration Features**: Add file attachments to leads and enable `@mentions` in notes to trigger notifications.
- **Code Cleanup**: Remove unwanted legacy code, optimize existing React components in `src/Components/leads`, and ensure the codebase is structured for scalable additions like advanced Voxbay hooks.

## Capabilities

### New Capabilities
- `unified-timeline`: Aggregates all lead-related events into a single chronological feed API.
- `follow-up-escalation`: Automated background jobs for overdue follow-up notifications and reassignment.
- `lead-collaboration`: File attachments and @mentions within lead remarks.

### Modified Capabilities
- `lead-management`: Upgrade of the lead detail UI to a Command Center and inclusion of Customer Journey tracking.

## Impact

- **Frontend**: Major refactor of `LeadDetailPage.jsx` and `UnifiedTimeline.jsx`. Introduction of calendar components in `AllFollowUpsPage.jsx`.
- **Backend**: New APIs for timeline aggregation and file uploads. Celery/Cron tasks required for escalation. Modification of `RemarkHistory` logic for `@mention` parsing.
- **Database**: New `LeadDocument` model for attachments.

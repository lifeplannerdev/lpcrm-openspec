## ADDED Requirements

### Requirement: Unified Activity Feed API
The system SHALL provide an API endpoint that aggregates all historical events related to a lead into a single chronologically sorted feed.

#### Scenario: Fetching the unified timeline
- **WHEN** the client requests the timeline for a lead
- **THEN** the system returns a combined list of Remarks, Status Updates, Follow-up changes, and Webhook logs sorted from newest to oldest.

### Requirement: Timeline Pagination
The unified timeline SHALL support pagination to ensure performance on leads with extensive histories.

#### Scenario: Paginating the timeline
- **WHEN** the timeline has more than 20 events
- **THEN** the API returns the first 20 and a cursor/link for the next page.

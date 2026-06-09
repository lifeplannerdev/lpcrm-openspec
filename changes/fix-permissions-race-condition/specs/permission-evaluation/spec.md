## ADDED Requirements

### Requirement: Synchronous Permission Resolution
The permissions resolution context SHALL immediately provide valid permissions based on the authenticated user without asynchronous delay upon initial load.

#### Scenario: Page Refresh on Protected Route
- **WHEN** user refreshes a page protected by permissions
- **THEN** the router receives the correct permissions instantly and stays on the requested route instead of falling back to the dashboard

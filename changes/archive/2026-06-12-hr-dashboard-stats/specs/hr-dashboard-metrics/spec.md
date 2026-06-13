## ADDED Requirements

### Requirement: HR Dashboard Metrics Retrieval
The system SHALL provide HR-specific metrics for users with HR viewing permissions, including Active Staff, Staff on Leave, Pending Candidates, and Available Assets.

#### Scenario: HR user accesses dashboard
- **WHEN** a user with `staff:read_tenant` (or similar HR permission) views the dashboard
- **THEN** the system returns statistics counting active staff, staff on leave, candidates in 'applied' status, and assets in 'AVAILABLE' status

### Requirement: Conditional Metric Display
The frontend dashboard SHALL only render metric cards that have explicit values returned by the backend.

#### Scenario: Backend returns sparse metrics
- **WHEN** the backend returns HR stats but excludes Leads or Students
- **THEN** the frontend `AdminStatsGrid` renders cards for HR stats and completely omits cards for Leads or Students instead of displaying them as "0"

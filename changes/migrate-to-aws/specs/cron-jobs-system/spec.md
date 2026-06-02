## ADDED Requirements

### Requirement: Celery Background Workers
The system SHALL utilize Celery and Redis running on the EC2 instance to execute background tasks independently of the main web API.

#### Scenario: Execution failure handling
- **WHEN** a background task fails during execution
- **THEN** the error is logged to standard output, captured by `systemd` journal logs, and an alert is sent if configured

### Requirement: Scheduled Tasks
The system SHALL utilize Celery Beat to trigger scheduled tasks at defined intervals.

#### Scenario: Nightly data cleanup
- **WHEN** the scheduled time occurs
- **THEN** Celery Beat queues the cleanup task for execution by the Celery worker

## ADDED Requirements

### Requirement: Centralized Task Registration
The system SHALL enforce a standardized convention where all asynchronous tasks and scheduled automations are defined in `tasks.py` modules within their respective Django apps.

#### Scenario: Adding a new background task
- **WHEN** a developer creates a new automation for the `leads` app
- **THEN** the task is defined in `leads/tasks.py` using the `@shared_task` decorator

### Requirement: Asynchronous Execution Priority
The system SHALL process critical webhooks (like incoming Leads) asynchronously to immediately return a 200 OK response to the caller, preventing timeouts.

#### Scenario: Processing an external webhook
- **WHEN** a Meta Lead Ad webhook is received
- **THEN** the system pushes the payload to the Celery broker, returns 200 OK, and processes the lead creation asynchronously

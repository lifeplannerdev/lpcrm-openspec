## ADDED Requirements

### Requirement: EC2 Bare-Metal Setup
The system SHALL provide a single AWS EC2 instance (e.g., Ubuntu) running Nginx, PostgreSQL, Redis, and Python to host the backend API and background workers.

#### Scenario: Network access
- **WHEN** a user attempts to access the API from the internet
- **THEN** traffic is allowed on ports 80 and 443, and all other ports (except SSH) are restricted

### Requirement: S3 Storage Setup
The system SHALL provide an Amazon S3 bucket for storing user documents and database backups.

#### Scenario: Backend access to S3
- **WHEN** the backend attempts to upload a file to S3
- **THEN** it succeeds using securely provisioned IAM credentials

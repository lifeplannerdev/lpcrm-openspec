## Purpose
Unified specification for infrastructure-and-devops.

## Requirements

**Subdomain:** aws-infrastructure

### Requirement: EC2 Bare-Metal Setup
The system SHALL provide a single AWS EC2 instance (e.g., Ubuntu) running Nginx, PostgreSQL, Redis, and Python to host the backend API and background workers. The system SHALL NOT contain any configuration files, routing structures, or dependencies specific to the legacy Vercel serverless environment.

#### Scenario: Network access
- **WHEN** a user attempts to access the API from the internet
- **THEN** traffic is allowed on ports 80 and 443, and all other ports (except SSH) are restricted

#### Scenario: Vercel cleanup
- **WHEN** the application is deployed to EC2
- **THEN** it boots successfully without relying on any Vercel environment variables or QStash webhooks


**Subdomain:** ci-cd-pipeline

### Requirement: Automated Backend Deployment
The CI/CD pipeline SHALL automatically deploy the Python backend upon merging code to the main branch.

#### Scenario: Successful backend deployment
- **WHEN** a pull request is merged into the `main` branch of the backend repository
- **THEN** GitHub Actions securely SSHs into the EC2 instance, pulls the latest code, and restarts the `systemd` services

### Requirement: Automated Frontend Deployment
The CI/CD pipeline SHALL automatically build and deploy the React frontend via AWS Amplify upon code changes.

#### Scenario: Successful frontend commit
- **WHEN** new code is pushed to the tracked branch for the frontend
- **THEN** AWS Amplify automatically triggers a build and updates the live site


**Subdomain:** cron-jobs-system

### Requirement: Celery Background Workers
The system SHALL utilize Celery and Redis running on the EC2 instance to execute background tasks independently of the main web API.

#### Scenario: Execution failure handling
- **WHEN** a background task fails during execution
- **THEN** the error is logged to standard output, captured by `systemd` journal logs, and an alert is sent if configured

### Requirement: Scheduled Tasks
The system SHALL utilize Celery Beat to trigger scheduled tasks at defined intervals natively within the VPC, entirely replacing any external triggers, dummy cron scripts, or Vercel cron endpoints.

#### Scenario: Nightly data cleanup
- **WHEN** the scheduled time occurs
- **THEN** Celery Beat queues the cleanup task for execution by the Celery worker


**Subdomain:** database-migration

### Requirement: Database Parity
The new local EC2 PostgreSQL database SHALL contain all schemas, tables, and data exactly as they exist in the current Neon database post-migration.

#### Scenario: Successful data import
- **WHEN** the `pg_restore` command completes
- **THEN** querying the new database yields the identical record count as the old database





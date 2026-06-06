## Purpose
Defines the capabilities and requirements for this domain.

## Requirements

### Requirement: EC2 Bare-Metal Setup
The system SHALL provide a single AWS EC2 instance (e.g., Ubuntu) running Nginx, PostgreSQL, Redis, and Python to host the backend API and background workers. The system SHALL NOT contain any configuration files, routing structures, or dependencies specific to the legacy Vercel serverless environment.

#### Scenario: Network access
- **WHEN** a user attempts to access the API from the internet
- **THEN** traffic is allowed on ports 80 and 443, and all other ports (except SSH) are restricted

#### Scenario: Vercel cleanup
- **WHEN** the application is deployed to EC2
- **THEN** it boots successfully without relying on any Vercel environment variables or QStash webhooks

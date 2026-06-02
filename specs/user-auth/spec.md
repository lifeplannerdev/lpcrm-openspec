## ADDED Requirements

### Requirement: Prevent Inactive User Login
The system SHALL NOT permit authentication for staff members who are marked as inactive (soft deleted).

#### Scenario: Inactive user attempts login
- **WHEN** an inactive user submits their credentials
- **THEN** the system rejects the login attempt and returns a 401 Unauthorized or a descriptive error message indicating the account is inactive

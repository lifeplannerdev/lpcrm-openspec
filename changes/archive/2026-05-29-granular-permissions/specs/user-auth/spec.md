## ADDED Requirements

### Requirement: Permissions included in Auth Payload
The system SHALL return the user's granular permissions upon successful authentication.

#### Scenario: User logs in
- **WHEN** a user successfully authenticates
- **THEN** the login response payload includes a `permissions` array alongside standard user data

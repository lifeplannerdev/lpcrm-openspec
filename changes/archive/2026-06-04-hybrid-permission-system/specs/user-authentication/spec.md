## MODIFIED Requirements

### Requirement: Login Response Payload
The system SHALL return authentication credentials along with a comprehensive permissions dictionary when a user successfully authenticates.

#### Scenario: Successful authentication
- **WHEN** user provides valid credentials
- **THEN** system returns an auth token, user details, AND a `permissions` JSON object outlining their allowed actions per resource

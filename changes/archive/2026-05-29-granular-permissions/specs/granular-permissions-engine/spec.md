## ADDED Requirements

### Requirement: Granular Permission Storage
The system SHALL store individual user permissions as a flat JSON array on the User record.

#### Scenario: User creation with template
- **WHEN** a new user is created with a specific role
- **THEN** the system populates the user's permissions array based on the role's predefined template

### Requirement: Granular API Authorization
The system SHALL authorize API requests based on granular permissions rather than role checks.

#### Scenario: Authorized API access
- **WHEN** a user requests an API endpoint requiring `edit_tasks`
- **THEN** the system grants access if `edit_tasks` is present in the user's permissions array

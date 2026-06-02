## Purpose
Defines the granular permissions engine for assigning and checking discrete user permissions.
## Requirements
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

### Requirement: Company Access Permissions
The permission system SHALL support new granular permissions for company-level access control.

#### Scenario: System checks for cross-company access
- **WHEN** validating a user's permissions array
- **THEN** the system recognizes `access_flag` as a valid permission string for cross-company access

#### Scenario: Default Role Templates include company access
- **WHEN** creating or migrating roles based on `permission_templates.py`
- **THEN** executive roles (ADMIN, CEO, HR, CM) are seeded with `access_flag` so they can manage the sister company


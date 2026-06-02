## ADDED Requirements

### Requirement: Company Access Permissions
The permission system SHALL support new granular permissions for company-level access control.

#### Scenario: System checks for cross-company access
- **WHEN** validating a user's permissions array
- **THEN** the system recognizes `access_flag` as a valid permission string for cross-company access

#### Scenario: Default Role Templates include company access
- **WHEN** creating or migrating roles based on `permission_templates.py`
- **THEN** executive roles (ADMIN, CEO, HR, CM) are seeded with `access_flag` so they can manage the sister company

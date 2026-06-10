## ADDED Requirements

### Requirement: RBAC Permission Evaluation
The system SHALL evaluate API access permissions dynamically using the database-backed Role and AppPermission relationships rather than a static JSON field on the User model.

#### Scenario: User requests a protected resource
- **WHEN** an authenticated user accesses an endpoint requiring specific resource and action permissions (e.g., `leads:read_tenant`)
- **THEN** the system checks if the user's assigned `db_roles` include an `AppPermission` matching that exact resource and action
- **THEN** access is granted if a match is found, otherwise 403 Forbidden is returned

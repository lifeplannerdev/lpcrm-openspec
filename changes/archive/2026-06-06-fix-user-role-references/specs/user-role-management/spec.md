## ADDED Requirements

### Requirement: Many-to-Many Role Validation
The system MUST validate user access and assign metadata based on the `db_roles` relationship rather than a flat `role` string field on the User object.

#### Scenario: User performs an action restricted to specific roles
- **WHEN** a user attempts to access an endpoint or perform an action restricted to `FULL_ACCESS_ROLES`
- **THEN** the system MUST check if any of the user's `db_roles` intersect with `FULL_ACCESS_ROLES` using a `.filter(name__in=...)` query

#### Scenario: User activity is logged
- **WHEN** the system logs user activity (e.g. Staff Creation, Updates)
- **THEN** the system MUST derive the role name(s) from the `db_roles` relationship to include in the log metadata, avoiding `AttributeError` from `.role`.

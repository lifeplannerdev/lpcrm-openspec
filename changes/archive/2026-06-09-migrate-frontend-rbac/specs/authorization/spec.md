## MODIFIED Requirements

### Requirement: Hybrid Permission Storage and Payload Generation
The system SHALL support role-based access control exclusively via a many-to-many `db_roles` relationship to a `Role` model, and user-specific custom permissions via a `permissions` JSON field. The legacy `role` field SHALL NOT be used.
The backend SHALL calculate a consolidated permission payload for a user based on their assigned DB roles and directly assigned JSON permissions, returning a structured dictionary mapping resources to allowed actions (e.g., `{"leads": ["read", "create"]}`).

#### Scenario: User performs an action restricted to specific roles
- **WHEN** a user attempts to access an endpoint or perform an action restricted to `FULL_ACCESS_ROLES`
- **THEN** the system MUST check if any of the user's `db_roles` intersect with `FULL_ACCESS_ROLES`

#### Scenario: User activity is logged
- **WHEN** the system logs user activity (e.g., Staff Creation, Updates)
- **THEN** the system MUST derive the role name(s) from the `db_roles` relationship to include in the log metadata.

#### Scenario: User logs in
- **WHEN** user with valid DB roles logs in
- **THEN** system generates a hybrid payload with access strictly defined by the union of their DB role permissions and user-specific permissions.

## REMOVED Requirements

### Requirement: Single Role Assignment
**Reason**: Replaced by multiple DB roles assignment (`db_roles`) to allow finer granularity and multiple role inheritance per staff member.
**Migration**: Update frontend Staff creation/editing forms to utilize the `db_roles` array parameter instead of sending a single `role` string. Remove `role` from all components and API interactions.

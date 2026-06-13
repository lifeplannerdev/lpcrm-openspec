## ADDED Requirements

### Requirement: Permission-based Dashboard Statistics
The dashboard stats API endpoint SHALL evaluate individual permissions dynamically to determine which statistics to expose, rather than demanding an absolute `ADMIN` role.

#### Scenario: User without ADMIN role but with read permissions queries stats
- **WHEN** an authenticated user without the `ADMIN` role but possessing specific read permissions queries `/stats/`
- **THEN** the endpoint returns a valid response containing only the statistical totals they are authorized to view

#### Scenario: User queries stats without any read permissions
- **WHEN** an authenticated user without any relevant read permissions queries `/stats/`
- **THEN** the endpoint returns a 403 Permission Denied response indicating insufficient privileges

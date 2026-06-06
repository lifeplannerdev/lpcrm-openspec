# dynamic-rbac Specification

## Purpose
TBD - created by archiving change migrate-user-role-to-db-roles. Update Purpose after archive.
## Requirements
### Requirement: Dynamic Roles
The system MUST support assigning multiple dynamic roles (`db_roles`) to users instead of a single static `role`.

#### Scenario: Creating a staff member
- **WHEN** an admin creates a new staff member and provides a list of `db_roles`
- **THEN** the system successfully saves the user and associates them with the selected roles, without requiring a static `role` string.

### Requirement: Permission-based Access
The system MUST evaluate user access based on `db_roles` and `permissions` rather than static role strings.

#### Scenario: Admin accessing dashboard stats
- **WHEN** a user requests the dashboard stats endpoint
- **THEN** the system checks if the user has the 'General Manager' or equivalent admin dynamic role, and grants or denies access accordingly.

#### Scenario: Assigning a branch to a Trainer
- **WHEN** a staff member is created or updated with the 'TRAINER' role in `db_roles`
- **THEN** the system automatically updates the associated `trainer_profile.branch_id`.


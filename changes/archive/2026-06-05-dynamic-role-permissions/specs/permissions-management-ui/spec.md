## MODIFIED Requirements

### Requirement: Permission Grouping and Role Presets
The system SHALL present student, attendance, and finance permissions in clear groups and shall support applying DB-backed Roles as default templates for users.

#### Scenario: Admin applies a DB-backed Role
- **WHEN** an Admin selects a predefined Role from the database (e.g., trainer or accounting) for a user
- **THEN** the system applies the associated DB permissions for that Role to the user without affecting unrelated custom permissions

## ADDED Requirements

### Requirement: Role Management Interface
The system SHALL provide an interface to manage dynamic roles independently of users.

#### Scenario: Admin configures a new role
- **WHEN** an Admin accesses the Role Management section
- **THEN** they can create a new role, assign it a name, and select which granular permissions it should contain

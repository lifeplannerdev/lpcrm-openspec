## ADDED Requirements

### Requirement: Role CRUD APIs
The backend SHALL expose endpoints to Create, Read, Update, and Delete roles. It SHALL also allow attaching granular permissions to these roles.

#### Scenario: Admin creates a custom role
- **WHEN** an administrator sends a POST request with a role name and a list of permission IDs
- **THEN** the backend persists the new role and its relationship with the provided permissions

### Requirement: Role Assignment API
The backend SHALL expose endpoints to assign roles to specific users, overriding or supplementing their existing roles.

#### Scenario: Admin assigns a role to a user
- **WHEN** an administrator sends a POST request linking a User ID to a Role ID
- **THEN** the user gains all permissions associated with that role on their next login or session refresh

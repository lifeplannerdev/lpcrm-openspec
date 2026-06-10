## MODIFIED Requirements

### Requirement: Granular API Authorization
The system SHALL authorize API requests using method-aware, granular `resource:action` permissions (e.g., `staff:read_any`, `penalties:edit_tenant`, `credentials:manage`) rather than legacy role checks or flat string matching (e.g. `request.user.permissions`).

#### Scenario: Authorized API access
- **WHEN** a user requests a `POST` API endpoint for penalties requiring `penalties:create`
- **THEN** the system grants access if `penalties:create` is present in the user's evaluated `db_roles` payload via `has_dynamic_permission`

#### Scenario: Unauthorized API access
- **WHEN** a trainer without `penalties:edit_any` requests a `PUT` endpoint for penalties
- **THEN** the system rejects the request even if the trainer has `penalties:read_any` to view the page

#### Scenario: Credentials write access via dynamic permissions
- **WHEN** a user attempts to create or delete a credential
- **THEN** the system grants access ONLY if `credentials:manage` is present in the user's evaluated `db_roles` payload via `has_dynamic_permission` (or if they are the creator of that specific credential where applicable)

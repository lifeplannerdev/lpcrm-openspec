## ADDED Requirements

### Requirement: RBAC Scoped Permissions Conversion
The system SHALL strictly enforce the `<resource>:<action>` format for all permissions across both the database seed (`seed_roles.py` and `permission_templates.py`) and frontend routing configurations. Legacy strings (e.g., `view_staff_reports`) MUST be automatically migrated to new formats (e.g., `reports:read_all`) in existing installations.

#### Scenario: Existing Role Evaluation
- **WHEN** the backend processes `get_user_permissions` for a user assigned an older `manage_asset` permission
- **THEN** the system returns `assets:manage` instead because the underlying database row was migrated, successfully passing the colon filter

### Requirement: Frontend Route Validation
The frontend `roles.js` and `PermissionRoute` components SHALL validate strictly against `<resource>` base names matching the new conventions.

#### Scenario: Navigating to Reports Menu
- **WHEN** an admin with the newly scoped `reports:read_all` permission navigates to the app
- **THEN** the frontend `hasAnyPermission('reports')` evaluates to true, and the "Staff Reports" menu appears correctly

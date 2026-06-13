## Purpose
Unified specification for core-systems-and-auth.

## Requirements

**Subdomain:** authorization

### Requirement: Prevent Inactive User Login
The system SHALL NOT permit authentication for staff members who are marked as inactive (soft deleted).

#### Scenario: Inactive user attempts login
- **WHEN** an inactive user submits their credentials
- **THEN** the system rejects the login attempt and returns a 401 Unauthorized or a descriptive error message indicating the account is inactive

### Requirement: Login Response Payload
The system SHALL return authentication credentials along with a comprehensive permissions dictionary when a user successfully authenticates.

#### Scenario: Successful authentication
- **WHEN** user provides valid credentials
- **THEN** system returns an auth token, user details, AND a `permissions` JSON object outlining their allowed actions per resource

### Requirement: Global Permissions Store
The frontend SHALL provide a React Context or global store that holds the `permissions` payload received from the backend upon login or session refresh.

#### Scenario: User logs in successfully
- **WHEN** backend responds with authentication token and `permissions` payload
- **THEN** frontend saves the payload to the global permissions store

### Requirement: Generic Authorization Wrapper
The frontend SHALL provide a generic wrapper component `<Can>` that conditionally renders its children based on the presence of a specific permission in the global store.

#### Scenario: User has required permission
- **WHEN** `<Can perform="leads:edit">` is rendered and the store contains `edit` under the `leads` key
- **THEN** the children of `<Can>` are rendered

#### Scenario: User lacks required permission
- **WHEN** `<Can perform="leads:edit">` is rendered and the store lacks `edit` under the `leads` key
- **THEN** the children of `<Can>` are NOT rendered

### Requirement: Hybrid Permission Storage and Payload Generation
The system SHALL support both role-based access control via a many-to-many `db_roles` relationship to a `Role` model, and user-specific custom permissions via a `permissions` JSON field. The legacy string-based `role` field on the `User` model is deprecated and completely removed; it MUST NOT be used for access control, serialization, or frontend display logic. The frontend MUST rely on `role_names` (array of strings) or `db_roles` (array of IDs).
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

### Requirement: Synchronous Permission Resolution
The permissions resolution context in the frontend SHALL immediately provide valid permissions based on the authenticated user without asynchronous delay upon initial load.

#### Scenario: Page Refresh on Protected Route
- **WHEN** user refreshes a page protected by permissions
- **THEN** the router receives the correct permissions instantly via the Auth Context and stays on the requested route.

### Requirement: Granular API Authorization
The system SHALL authorize API requests using method-aware, granular `resource:action` permissions (e.g., `staff:read_any`, `penalties:edit_tenant`) rather than legacy role checks or flat string matching.

#### Scenario: Authorized API access
- **WHEN** a user requests a `POST` API endpoint for penalties requiring `penalties:create`
- **THEN** the system grants access if `penalties:create` is present in the user's evaluated `db_roles` payload via `has_dynamic_permission`

#### Scenario: Unauthorized API access
- **WHEN** a trainer without `penalties:edit_any` requests a `PUT` endpoint for penalties
- **THEN** the system rejects the request even if the trainer has `penalties:read_any` to view the page

#### Scenario: Credentials write access via dynamic permissions
- **WHEN** a user attempts to create or delete a credential
- **THEN** the system grants access ONLY if `credentials:manage` is present in the user's evaluated `db_roles` payload via `has_dynamic_permission` (or if they are the creator of that specific credential where applicable)

### Requirement: Company and Domain Access Permissions
The permission system SHALL support company-level access control and domain-specific access for students, attendance, and fees.

#### Scenario: System checks for cross-company access
- **WHEN** validating a user's permissions array
- **THEN** the system recognizes `access_flag` as a valid permission string for cross-company access

#### Scenario: Default Role Templates include student and fee access
- **WHEN** creating or migrating roles based on `permission_templates.py`
- **THEN** accounting roles are seeded with fee-management permissions, trainers are seeded with attendance and read-only fee permissions, and admin-style roles retain cross-company access

### Requirement: Dynamic Permission Vocabulary
The system SHALL recognize standard `resource:action` permission strings used by both the CRM UI and the backend dynamic permission classes (e.g., `HasPenaltyPermission`, `HasStaffPermission`).

#### Scenario: Read permissions are evaluated
- **WHEN** the system evaluates a `GET` request requiring `staff:read_any`, `attendance:read_any`, or `candidates:read_any`
- **THEN** the permission engine accepts those strings as valid read permissions

#### Scenario: Write/Manage permissions are evaluated
- **WHEN** the system evaluates a `POST`, `PUT`, or `DELETE` request requiring `penalties:edit_any`, `attendance:create_any`, or `candidates:delete_any`
- **THEN** the permission engine strictly enforces write access based on those specific action strings


**Subdomain:** permission-evaluation
### Requirement: RBAC Permission Evaluation
The system SHALL evaluate API access permissions dynamically using the database-backed Role and AppPermission relationships rather than a static JSON field on the User model.

#### Scenario: User requests a protected resource
- **WHEN** an authenticated user accesses an endpoint requiring specific resource and action permissions (e.g., `leads:read_tenant`)
- **THEN** the system checks if the user's assigned `db_roles` include an `AppPermission` matching that exact resource and action
- **THEN** access is granted if a match is found, otherwise 403 Forbidden is returned


**Subdomain:** legacy-permissions-migration
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


**Subdomain:** multi-tenant-company-segregation
### Requirement: Backend API Company Filtering
The system SHALL filter all core resource queries (Tasks, Leads, Staff, Penalties, Candidates, Students, Reports) by the requested company.

#### Scenario: User queries their own native company
- **WHEN** user makes a GET request for their own company (e.g., `user.company == 'LP'` querying `?company=LP`)
- **THEN** system returns records where `company='LP'`

#### Scenario: User queries other company with access_flag permission
- **WHEN** an LP user makes a GET request with `?company=FLAG` and possesses the `access_flag` permission
- **THEN** system returns records where `company='FLAG'`

#### Scenario: User queries other company without permission
- **WHEN** user makes a GET request for a company they do not belong to and lacks the `access_flag` permission
- **THEN** system returns a 403 Forbidden response

#### Scenario: User queries without specifying company
- **WHEN** user makes a GET request without a `company` parameter
- **THEN** system defaults to returning records for the user's native `company`

### Requirement: Per-Page Company Switcher Component
The UI SHALL provide a standalone Company Switcher tab component that can be rendered at the top of individual pages (Tasks, Staff, Leads) rather than in the global Navbar.

#### Scenario: User has cross-company access
- **WHEN** an LP user with the `access_flag` permission views a supported page
- **THEN** they see the Company Switcher tabs (`LP | FLAG`) at the top of the page content

#### Scenario: User changes company on a specific page
- **WHEN** user clicks `FLAG` on the Tasks page switcher
- **THEN** the Tasks page fetches and displays FLAG tasks, and the URL updates (e.g., `?view_company=FLAG`), but other open browser tabs (e.g., Staff page showing LP) remain unaffected

#### Scenario: User only has native access
- **WHEN** user lacks the `access_flag` permission
- **THEN** the Company Switcher component is hidden and the page always shows their native company's data




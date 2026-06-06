## Purpose
Defines the authorization layer, granular permission engine, API access control, frontend permission state, and user authentication rules for the CRM.

## Requirements

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

### Requirement: Granular Permission Storage
The system SHALL store individual user permissions as a flat JSON array on the User record.

#### Scenario: User creation with template
- **WHEN** a new user is created with a specific role
- **THEN** the system populates the user's permissions array based on the role's predefined template

### Requirement: Granular API Authorization
The system SHALL authorize API requests based on granular permissions rather than role checks.

#### Scenario: Authorized API access
- **WHEN** a user requests an API endpoint requiring `manage_fees`
- **THEN** the system grants access if `manage_fees` is present in the user's permissions array

#### Scenario: Unauthorized API access
- **WHEN** a trainer without `manage_fees` requests a fee update endpoint
- **THEN** the system rejects the request even if the trainer can view the page in read-only mode

### Requirement: Company and Domain Access Permissions
The permission system SHALL support company-level access control and domain-specific access for students, attendance, and fees.

#### Scenario: System checks for cross-company access
- **WHEN** validating a user's permissions array
- **THEN** the system recognizes `access_flag` as a valid permission string for cross-company access

#### Scenario: Default Role Templates include student and fee access
- **WHEN** creating or migrating roles based on `permission_templates.py`
- **THEN** accounting roles are seeded with fee-management permissions, trainers are seeded with attendance and read-only fee permissions, and admin-style roles retain cross-company access

### Requirement: Student, Finance, and Credentials Permission Vocabulary
The system SHALL recognize student, attendance, finance, and credentials permission strings used by the CRM UI and backend authorization layer.

#### Scenario: New permission string is validated
- **WHEN** the system evaluates `view_students`, `mark_attendance`, `view_fees`, `manage_fees`, `view_credentials`, or `manage_credentials`
- **THEN** the permission engine accepts those strings as valid permissions

#### Scenario: Expanded finance permissions are evaluated
- **WHEN** the system evaluates `restructure_fees`, `record_partial_payment`, `issue_fee_notice`, or `view_fee_reports`
- **THEN** the permission engine accepts those strings as valid permissions

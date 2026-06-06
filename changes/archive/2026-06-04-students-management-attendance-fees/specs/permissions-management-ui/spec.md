## MODIFIED Requirements

### Requirement: Permissions Management Interface
The system SHALL provide an interface for Admins to view and edit individual user permissions, including student, attendance, and finance permissions.

#### Scenario: Admin views user permissions
- **WHEN** an Admin selects a user in the Staff Management section
- **THEN** the system displays a checklist of all available system permissions grouped by domain, with the user's current permissions checked

#### Scenario: Admin updates user permissions
- **WHEN** an Admin checks or unchecks a permission and saves
- **THEN** the system updates the user's permissions array in the database

### Requirement: Permission Grouping and Role Presets
The system SHALL present student, attendance, and finance permissions in clear groups and shall support role-based default templates for common CRM roles.

#### Scenario: Admin reviews finance permissions
- **WHEN** an Admin opens the permissions editor for an accounting user
- **THEN** the system shows the fee-related permissions together so the admin can quickly confirm write access versus trainer read-only access

#### Scenario: Admin resets a role template
- **WHEN** an Admin applies the default template for a trainer or accounting role
- **THEN** the system restores the expected permission set for that role without affecting unrelated custom permissions

### Requirement: Finance Permission Coverage
The system SHALL expose finance permissions such as fee viewing, fee management, partial payment handling, fee restructuring, fee notices, and fee reporting in the permissions editor.

#### Scenario: Admin configures accounting access
- **WHEN** an Admin opens the permissions editor for an accounting user
- **THEN** the system shows the finance permission group with the fee-related actions required for accounting work

#### Scenario: Admin configures trainer read-only access
- **WHEN** an Admin opens the permissions editor for a trainer
- **THEN** the system shows only the read-only fee permissions and does not preselect fee edit or restructuring permissions

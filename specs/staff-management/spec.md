## ADDED Requirements

### Requirement: Staff Soft Deletion Only
The system SHALL NOT permit the hard deletion of staff records under any circumstances from the user interface. Staff records can only be soft-deleted by toggling their `is_active` status to false.

#### Scenario: User attempts to delete a staff member
- **WHEN** a user looks for a delete option on a staff member's record
- **THEN** no delete button is available in the UI
- **AND** the user can only deactivate the staff member using the "Active Status" toggle

### Requirement: Premium Staff Management UI
The Staff Management UI SHALL employ premium visual design standards, including dynamic hover states, soft rounded corners, glassmorphism accents, and highly structured, clean forms.

#### Scenario: Viewing the staff grid
- **WHEN** a user visits the Staff Management page
- **THEN** the grid displays highly optimized, visually premium cards with clear status indicators and action buttons

### Requirement: Display Attached Assets on Staff Profile
The system SHALL display all assets currently assigned to a staff member on their individual Staff Details page, providing a clear list of what company property they currently hold.

#### Scenario: Viewing a staff profile with assigned assets
- **WHEN** an admin views the detailed profile of a staff member who holds a laptop
- **THEN** the profile shows an "Attached Assets" section listing the laptop and its details.

### Requirement: Asset Permission Assignment
The Staff Permission Assign Screen SHALL list the new Asset Management permissions (`view_asset`, `manage_asset`) allowing admins to grant specific staff access to the Asset Management feature.

#### Scenario: Granting asset management permissions
- **WHEN** an admin edits the permissions of an IT staff member
- **THEN** they can select the "Manage Assets" permission flag, saving the setting successfully.

## MODIFIED Requirements

### Requirement: Tabbed Status Filtering for Staff
The system SHALL present staff members in a tabbed UI to clearly separate them by status (All Staff, Active, Inactive, On Leave), ensuring soft-deleted (inactive) users remain accessible for data integrity.

#### Scenario: User views inactive staff
- **WHEN** the user switches to the "Inactive" tab on the Staff page
- **THEN** the grid only displays staff members whose status is Inactive

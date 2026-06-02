## ADDED Requirements

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

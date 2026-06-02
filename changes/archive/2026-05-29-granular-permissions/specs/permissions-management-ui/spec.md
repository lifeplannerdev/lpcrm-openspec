## ADDED Requirements

### Requirement: Permissions Management Interface
The system SHALL provide an interface for Admins to view and edit individual user permissions.

#### Scenario: Admin views user permissions
- **WHEN** an Admin selects a user in the Staff Management section
- **THEN** the system displays a checklist of all available system permissions, with the user's current permissions checked

#### Scenario: Admin updates user permissions
- **WHEN** an Admin checks or unchecks a permission and saves
- **THEN** the system updates the user's permissions array in the database

## ADDED Requirements

### Requirement: Asset Tracking Model
The system SHALL track physical and digital assets with details including name, type, serial number, status, company affiliation, assignment to a user, and a photo/invoice attachment.

#### Scenario: Creating a new asset
- **WHEN** an admin creates a new asset record
- **THEN** the system stores the asset details and associates it with the specified company and optionally a staff member.

### Requirement: Multi-Tenant Asset Filtering
The Asset Management UI SHALL display assets segregated by company (LP vs FLAG) using tabbed views or optimized filtering to ensure strict data separation based on the viewing admin's access.

#### Scenario: Viewing assets for LP company
- **WHEN** an admin clicks the "LP" tab on the Asset Management page
- **THEN** the system fetches and displays only assets where `company == 'LP'`.

### Requirement: Asset Assignment and Status
The system SHALL allow updating the status of an asset (Available, Assigned, Maintenance, Retired) and tracking its current assignee.

#### Scenario: Assigning an asset to a staff member
- **WHEN** an admin assigns an available laptop to "John Doe"
- **THEN** the system sets the asset's assigned_to field to John Doe and its status to 'Assigned'.

### Requirement: Premium Asset UI
The Asset Management page SHALL follow the premium UI guidelines, offering a dynamic, visually appealing grid or table with glassmorphism elements, micro-animations, and clear status indicators.

#### Scenario: Navigating the asset inventory
- **WHEN** the user browses the asset inventory
- **THEN** they see an engaging, responsive interface with hover effects and clear typography.

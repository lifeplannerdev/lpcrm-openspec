## ADDED Requirements

### Requirement: Attach Asset to Parent Asset
The system SHALL allow an asset (such as a SIM card) to be attached to a parent asset (such as a Mobile phone).

#### Scenario: Attaching a SIM to a Mobile
- **WHEN** a user creates or edits an asset of type "SIM" and selects a "Mobile" from the Parent Asset dropdown
- **THEN** the SIM is saved with the Mobile as its `parent_asset`

### Requirement: Inherit Assigned User from Parent
The system SHALL enforce that any asset attached to a parent asset inherits the `assigned_to` property of its parent.

#### Scenario: Syncing Assignment on Attachment
- **WHEN** an unassigned SIM is attached to a Mobile assigned to User A
- **THEN** the SIM's `assigned_to` field is automatically set to User A

#### Scenario: Syncing Assignment on Parent Update
- **WHEN** a Mobile with an attached SIM is reassigned from User A to User B
- **THEN** the attached SIM's `assigned_to` field is automatically updated to User B

### Requirement: Display Attached Assets
The system SHALL display attached assets grouped under their parent asset in the UI (e.g., Staff Profile page).

#### Scenario: Viewing Staff Assigned Devices
- **WHEN** a user views a staff member's profile
- **THEN** any attached assets (SIMs) are displayed visually indented beneath their respective parent device (Mobiles)

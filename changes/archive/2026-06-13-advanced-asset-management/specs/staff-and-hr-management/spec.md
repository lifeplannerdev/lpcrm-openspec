## MODIFIED Requirements

### Requirement: Asset Tracking Model
The system SHALL track physical and digital assets with details including name, category, serial number/IMEI, status, company affiliation, assignment to a User OR a Location, and a photo/invoice attachment.

#### Scenario: Creating a new asset
- **WHEN** an admin creates a new asset record
- **THEN** the system stores the asset details and associates it with the specified company and optionally a staff member or a physical location.

## REMOVED Requirements

### Requirement: Structured Asset Types
**Reason**: Replaced by the dynamic AssetCategory model which allows administrators to define custom types like AC, Teapoy, etc.
**Migration**: Use the new dynamic categories endpoint and UI.

## ADDED Requirements

### Requirement: Location Management
The system SHALL support the creation and management of physical Locations (e.g., "Reception 1", "Cabin 3", "MD Cabin") to which assets can be assigned.

#### Scenario: Creating a new location
- **WHEN** an admin navigates to Space Management and creates a new Location named "Cabin 1"
- **THEN** the location is saved and becomes available as an assignment target for assets

### Requirement: Asset Assignment to Location
The system SHALL allow an asset to be assigned directly to a Location, indicating it is an office fixture (e.g., AC, Fan, Sofa) rather than a personal assignment.

#### Scenario: Assigning AC to Cabin 3
- **WHEN** an admin edits an AC asset and selects "Cabin 3" as the location
- **THEN** the asset's assigned_location is updated and assigned_to (User) is cleared

### Requirement: Space Inventory Dashboard (Macro View)
The system SHALL provide a Space Inventory Dashboard that visualizes the office spatially, showing a card for each Location, summarizing the occupant and the assets within it.

#### Scenario: Viewing the Macro Dashboard
- **WHEN** an admin visits the Space Inventory page
- **THEN** they see cards for "Reception", "Cabin 1", etc., with summarized icons for Desktop Systems, Chairs, and ACs present in each location

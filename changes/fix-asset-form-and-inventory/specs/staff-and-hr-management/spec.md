## MODIFIED Requirements

### Requirement: Location Assignment for Assets
The system SHALL allow an asset to be assigned to both a Location and a User simultaneously. This indicates that an asset is physically located in a specific space but is the personal responsibility of a specific user. If assigned only to a Location without a User, it is considered a general room fixture.

#### Scenario: Assigning an asset to a Location and User
- **WHEN** an admin edits an asset and selects both "Cabin 3" as the location and "John Doe" as the assigned user
- **THEN** the asset's `assigned_location` is updated to Cabin 3 and `assigned_to` is updated to John Doe simultaneously

### Requirement: Space Inventory Dashboard
The system SHALL provide a Space Inventory Dashboard that visualizes the office spatially, showing a card for each Location, summarizing the occupants and the assets within it based on the physical location of the assets.

#### Scenario: Viewing occupants in a Location
- **WHEN** an admin visits the Space Inventory page and clicks on "Cabin 1"
- **THEN** the system displays all assets where `assigned_location` is "Cabin 1", grouping personal assets under the respective users they are `assigned_to`, regardless of those users' HR profile location settings

## ADDED Requirements

### Requirement: Dependent Branch-Location Form Logic
The asset creation and editing form SHALL enforce a strict hierarchy between Branch and Location assignments to prevent invalid location selections.

#### Scenario: Location dropdown visibility and filtering
- **WHEN** a user opens the asset form
- **THEN** the Location dropdown is only visible or enabled if a Branch is selected
- **AND** the Location dropdown only displays locations that belong to the selected Branch

### Requirement: Complete Asset Form Submission
The asset creation and editing form SHALL submit all fields, including the Branch assignment, to ensure data integrity across the hierarchy.

#### Scenario: Saving branch assignment
- **WHEN** an admin selects a Branch and saves the asset
- **THEN** the `branch` ID is included in the form payload and correctly saved to the database

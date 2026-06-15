## ADDED Requirements

### Requirement: Branch Data Model
The system SHALL support organizational Branches.
- A `Branch` model MUST have a `name` (e.g., "Kochi Office", "Kottayam HO").
- A `Branch` MUST belong to a company.

#### Scenario: Creating a branch
- **WHEN** an admin creates a new branch
- **THEN** it is saved in the database

### Requirement: Location to Branch Mapping
The system SHALL map `Location` entities to a specific `Branch`.
- A `Location` MUST have a foreign key to `Branch` (nullable initially for migration purposes).

#### Scenario: Assigning a location to a branch
- **WHEN** an admin creates or edits a location
- **THEN** they can select which branch the location belongs to

### Requirement: Branch Filtering in Space Inventory
The frontend Space Inventory SHALL group or filter locations by their respective Branch.

#### Scenario: Viewing the Space Inventory
- **WHEN** a user visits the Asset Management page and clicks "Space Inventory"
- **THEN** they see an option to filter or view locations strictly by Branch (e.g., viewing only Kochi Office locations).

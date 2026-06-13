## ADDED Requirements

### Requirement: Dynamic Asset Categories
The system SHALL support a dynamic AssetCategory model, allowing administrators to add, edit, or remove asset categories (e.g., 'Teapoy', 'Waste Bin', 'AC') without code changes.

#### Scenario: Creating a new category
- **WHEN** an admin adds "Teapoy" to the Asset Categories
- **THEN** "Teapoy" immediately becomes available in the Category dropdown when creating a new asset

### Requirement: Flat Mobile Phone Details
The system SHALL support storing primary and secondary phone numbers directly on Mobile assets to flatten data entry.

#### Scenario: Creating a Mobile Asset
- **WHEN** a user creates an asset with a category of 'Mobiles'
- **THEN** the form dynamically shows `Primary Phone Number` and `Secondary Phone Number` fields, which are saved directly to the asset record

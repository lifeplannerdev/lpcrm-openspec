## ADDED Requirements

### Requirement: Structured Asset Types
The system SHALL restrict the creation and editing of assets to a predefined set of types: Mobiles, Monitors, PC, Keyboard, Mouse, Laptops, SIM.

#### Scenario: Creating a New Asset
- **WHEN** a user fills out the Add Asset form
- **THEN** the Asset Type field is a dropdown containing only the approved predefined types

### Requirement: Dynamic IMEI Labeling
The system SHALL dynamically change the UI label for the hardware identifier field based on the selected asset type.

#### Scenario: Selecting Mobile Asset Type
- **WHEN** a user selects "Mobiles" from the Asset Type dropdown
- **THEN** the label for the hardware identifier field changes from "Serial Number" to "IMEI Number"

#### Scenario: Selecting Non-Mobile Asset Type
- **WHEN** a user selects "Laptops" from the Asset Type dropdown
- **THEN** the label for the hardware identifier field remains "Serial Number"

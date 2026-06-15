## MODIFIED Requirements

### Requirement: Display Attached Assets on Staff Profile
The system SHALL display all assets and locations currently assigned to a staff member on their individual Staff Details page, grouped logically by category. The system SHALL group assets into "Mobile Phones" (displaying their primary/secondary SIM details and provider), "Standalone SIMs" (SIMs not attached to a phone), and "Responsible Areas" (locations managed by the staff). The system SHALL NOT rely on legacy `asset_type` fields, instead using `category_details.name` or the presence of specific SIM/provider fields to determine the type.

#### Scenario: Viewing a staff profile with assigned assets
- **WHEN** an admin views the detailed profile of a staff member who holds a laptop, a mobile phone with a SIM, and manages a location
- **THEN** the profile shows a categorized list, separating the Mobile Phone (with its SIM details) from the general assets, and displaying the managed location under "Responsible Areas".

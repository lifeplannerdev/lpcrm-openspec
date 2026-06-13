## ADDED Requirements

### Requirement: Academic Batch Default Fee Template
The system SHALL allow administrators to configure a default fee template for each Academic Batch. 

#### Scenario: Configuring a Default Fee Template
- **WHEN** an admin creates or edits an Academic Batch in the UI
- **THEN** they are presented with a dropdown of active fee templates to select as the default

#### Scenario: Auto-suggesting Fee Template during Enrollment
- **WHEN** an admin selects an Academic Batch during student enrollment
- **THEN** the system automatically pre-selects the corresponding default fee template in the fee plan dropdown

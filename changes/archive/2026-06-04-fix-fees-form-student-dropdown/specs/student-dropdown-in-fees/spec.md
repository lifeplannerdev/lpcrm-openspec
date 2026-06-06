## ADDED Requirements

### Requirement: Searchable Student Dropdown in Fee Form
The system SHALL display a searchable dropdown for selecting a student in the Create Fee Account form instead of a manual text input.

#### Scenario: Successful student selection
- **WHEN** user opens the Create Fee Account form and interacts with the Student input
- **THEN** system displays a list of active students fetched from the backend and allows the user to select one, storing their ID in the form state.

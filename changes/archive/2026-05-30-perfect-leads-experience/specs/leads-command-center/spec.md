## ADDED Requirements

### Requirement: Split-Pane Master-Detail View
The Leads List page SHALL optionally render as a split-pane interface on desktop screens, displaying the list of leads on the left and a detailed preview panel on the right.

#### Scenario: Selecting a lead
- **WHEN** user clicks on a lead row in the main table
- **THEN** a side panel slides in from the right containing the lead's core details and quick actions
- **AND** the URL updates without forcing a full page reload

#### Scenario: Closing the preview
- **WHEN** user clicks the 'X' button or presses Escape while the side panel is open
- **THEN** the side panel collapses and returns focus to the main list

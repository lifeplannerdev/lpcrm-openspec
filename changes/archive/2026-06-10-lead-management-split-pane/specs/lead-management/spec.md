## MODIFIED Requirements

### Requirement: Split-Pane Master-Detail View
The Leads List page SHALL optionally render as a split-pane interface on desktop screens, displaying the list of leads on the left and a detailed preview panel on the right. On mobile screens (under 1024px), it SHALL render as a full-screen slide-over drawer to preserve context without compromising usability. The system SHALL use nested routing to maintain state across reloads.

#### Scenario: Selecting a lead on desktop
- **WHEN** user clicks on a lead row in the main table on a desktop device
- **THEN** the route updates to `/leads/:leadId` using nested routing
- **AND** a side panel slides in from the right containing the lead's core details and quick actions, while the table width compresses to accommodate it

#### Scenario: Selecting a lead on mobile
- **WHEN** user clicks on a lead row in the main table on a mobile device
- **THEN** the route updates to `/leads/:leadId` using nested routing
- **AND** a full-screen slide-over drawer covers the view, retaining the list's scroll position underneath

#### Scenario: Closing the preview
- **WHEN** user clicks the 'X' button, the backdrop, or presses Escape
- **THEN** the route updates to `/leads`
- **AND** the side panel collapses and returns focus to the main list

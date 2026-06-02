## ADDED Requirements

### Requirement: Unified Story Timeline
The lead details page SHALL display a single vertical timeline combining Follow-ups, Assignment History, and Processing Updates.

#### Scenario: Viewing a lead's history
- **WHEN** user navigates to a lead detail page
- **THEN** they see a chronological timeline of all events (creation, assignments, calls made, status changes) in one scrollable view

### Requirement: Inline Timeline Actions
The timeline SHALL allow users to directly schedule follow-ups or add notes without leaving the timeline view.

#### Scenario: Adding a note to the timeline
- **WHEN** user clicks "Add Note" within the timeline header
- **THEN** an inline form appears allowing immediate submission of a new remark or follow-up

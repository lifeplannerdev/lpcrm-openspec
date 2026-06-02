## ADDED Requirements

### Requirement: Advanced Multi-Date Filtering for Tasks
The system SHALL support filtering tasks by multiple dynamic date ranges simultaneously (e.g. Today, Yesterday, Specific Date).

#### Scenario: User filters by Today
- **WHEN** a user clicks the "Today" filter on the Kanban board
- **THEN** the board only displays tasks due today

#### Scenario: User filters by Specific Date
- **WHEN** a user selects a specific date from a date picker on the Kanban board
- **THEN** the board only displays tasks due on that specific date

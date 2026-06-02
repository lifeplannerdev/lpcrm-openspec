## MODIFIED Requirements

### Requirement: Tasks Module Navigation
The system SHALL support deep navigation within the Tasks tab.

#### Scenario: Navigating to Task Details
- **WHEN** the user is on the main Tasks screen
- **THEN** they see a list of tasks
- **WHEN** they tap a specific task
- **THEN** the app pushes the `TaskDetailsScreen` onto the navigation stack, preserving the bottom tab bar.

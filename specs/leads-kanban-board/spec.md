## ADDED Requirements

### Requirement: Kanban View for Leads
The system SHALL provide an alternate "Kanban" view for the Leads page, categorizing leads by their current status (e.g., Enquiry, Contacted, Qualified, Converted).

#### Scenario: Dragging a lead to a new status
- **WHEN** user drags a lead card from the "Enquiry" column and drops it into the "Contacted" column
- **THEN** the lead's status is instantly updated via an API call
- **AND** a success toast notification is displayed

#### Scenario: Accessing the Kanban board
- **WHEN** user clicks the "Kanban View" toggle on the Leads list page
- **THEN** the table view is hidden and the drag-and-drop board is displayed

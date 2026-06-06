## Purpose
Defines the capabilities and requirements for this domain.

## Requirements

### Requirement: Missing Action Warning
The system SHALL visually flag leads in active states (ENQUIRY, CONTACTED) that do not have a future scheduled follow-up.

#### Scenario: Lead missing a follow-up
- **WHEN** an active lead has no pending follow-ups scheduled
- **THEN** a warning icon and highlight are displayed next to the lead in the main list and Kanban view

### Requirement: Follow-up Cascading Prompt
When a lead is reassigned, the system SHALL prompt the user to reassign any pending follow-ups to the new owner.

#### Scenario: Reassigning a lead with pending follow-ups
- **WHEN** user reassigns a lead that has pending follow-ups
- **THEN** a prompt asks "Do you want to reassign the pending follow-ups to [New User]?"
- **AND** confirming updates the `assigned_to` field of the pending follow-ups

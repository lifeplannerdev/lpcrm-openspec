## ADDED Requirements

### Requirement: Meta Lead Auto-Assignment
The system SHALL automatically assign incoming Meta Leads to a designated counselor or manager.

#### Scenario: Assigning based on campaign rules
- **WHEN** a Meta Lead is created and the `campaign_name` matches a predefined assignment rule
- **THEN** the system assigns the lead to the specified user
- **THEN** the system schedules a standard FollowUp task for that assignee

#### Scenario: Fallback assignment
- **WHEN** a Meta Lead is created but no specific campaign rule matches
- **THEN** the system assigns the lead to a default fallback user (e.g. an Admin)

## MODIFIED Requirements

### Requirement: Role-Based Navigation System
The system SHALL dynamically filter the mobile MainTabNavigator based on the logged-in user's permissions array. It MUST support up to 13 distinct CRM screens.

#### Scenario: User has permissions for all 13 screens
- **WHEN** user logs in with an Admin role
- **THEN** the Tab Bar renders the first 4 screens (e.g. Dashboard, Leads, Tasks, Chat)
- **THEN** the Tab Bar renders a 5th 'Menu' tab
- **THEN** clicking 'Menu' opens a grid containing the remaining 9 screens (Staff, Students, Penalties, Candidates, Reports, etc.)

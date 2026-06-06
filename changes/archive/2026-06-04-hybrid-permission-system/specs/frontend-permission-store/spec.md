## ADDED Requirements

### Requirement: Global Permissions Store
The frontend SHALL provide a React Context or global store that holds the `permissions` payload received from the backend upon login or session refresh.

#### Scenario: User logs in successfully
- **WHEN** backend responds with authentication token and `permissions` payload
- **THEN** frontend saves the payload to the global permissions store

### Requirement: Generic Authorization Wrapper
The frontend SHALL provide a generic wrapper component `<Can>` that conditionally renders its children based on the presence of a specific permission in the global store.

#### Scenario: User has required permission
- **WHEN** `<Can perform="leads:edit">` is rendered and the store contains `edit` under the `leads` key
- **THEN** the children of `<Can>` are rendered

#### Scenario: User lacks required permission
- **WHEN** `<Can perform="leads:edit">` is rendered and the store lacks `edit` under the `leads` key
- **THEN** the children of `<Can>` are NOT rendered

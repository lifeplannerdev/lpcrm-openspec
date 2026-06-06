## Purpose
Defines the backend authorization logic and hybrid payload generation mechanism for permissions.
## Requirements
### Requirement: Generate Hybrid Permission Payload
The backend SHALL calculate a consolidated permission payload for a user based on their assigned DB roles and directly assigned DB permissions, returning a dictionary mapping resources to allowed actions.

#### Scenario: User logs in
- **WHEN** user with valid DB roles logs in
- **THEN** system generates payload with access strictly defined by their DB role/permission mappings


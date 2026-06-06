## MODIFIED Requirements

### Requirement: Generate Hybrid Permission Payload
The backend SHALL calculate a consolidated permission payload for a user based on their assigned DB roles and directly assigned DB permissions, returning a dictionary mapping resources to allowed actions.

#### Scenario: User logs in
- **WHEN** user with valid DB roles logs in
- **THEN** system generates payload with access strictly defined by their DB role/permission mappings

## REMOVED Requirements

### Requirement: Fallback Evaluation
**Reason**: All permissions and roles are now entirely DB-driven and dynamically manageable. Fallback logic is obsolete and dangerous.
**Migration**: Run the database migration and seeder to populate all existing hardcoded roles into the DB before removing this fallback logic.

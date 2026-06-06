## ADDED Requirements

### Requirement: Generate Hybrid Permission Payload
The backend SHALL calculate a consolidated permission payload for a user based on their legacy role and company, returning a dictionary mapping resources to allowed actions.

#### Scenario: User is an LP Admin
- **WHEN** user with role 'admin' logs in
- **THEN** system generates payload with full access across all resources (e.g., `{"leads": ["read", "create", "update", "delete"]}`)

#### Scenario: User is an LP Manager
- **WHEN** user with role 'manager' and company 'LP' logs in
- **THEN** system generates payload allowing read/write on LP resources only

### Requirement: Fallback Evaluation
The backend SHALL support a grace period where if an explicit DB permission does not exist, it falls back to a hardcoded mapping of legacy roles to the new permission schema.

#### Scenario: No DB permissions defined
- **WHEN** backend generates payload for user without explicit DB mappings
- **THEN** backend uses the hardcoded fallback dictionary mapping their role/company to actions

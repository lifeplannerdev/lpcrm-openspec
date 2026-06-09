## MODIFIED Requirements

### Requirement: Granular Credential Sharing
The system SHALL allow users to share a specific credential with individual users or entire roles.
Visibility of a credential SHALL be strictly controlled by object-level sharing and query filtering, allowing any authenticated user to access the Vault and see only what is explicitly shared with them, without requiring global API permissions.

#### Scenario: Credential shared with a role
- **WHEN** a user creates a credential and selects the "Manager" role in the "Share With" dropdown
- **THEN** any user with the Manager role can access the vault, view, and decrypt the credential
- **AND** other users cannot see or decrypt the credential

#### Scenario: Credential kept private
- **WHEN** a user creates a credential without selecting any users or roles to share with
- **THEN** only the creator (and super admins) can view or decrypt it

## MODIFIED Requirements

### Requirement: Premium Vault Interface
The system SHALL display the credentials in a secure, glassmorphic UI where passwords are masked by default.
The UI SHALL provide action buttons for users to interact with credentials based on their permissions.

#### Scenario: Editing a credential
- **WHEN** the authorized user (creator or admin) clicks the "Edit" button on a credential card
- **THEN** the system opens the Edit Modal populated with the credential's existing data, including shared users and roles
- **AND** saving the modal updates the credential directly

#### Scenario: Deleting a credential
- **WHEN** the authorized user (creator or admin) clicks the "Delete" button on a credential card
- **THEN** the system prompts for confirmation, and upon approval, permanently removes the credential

#### Scenario: Sharing a credential
- **WHEN** a user is creating or editing a credential in the modal
- **THEN** they can select specific users and/or roles from a dropdown
- **AND** upon saving, the backend grants those selected users/roles access to view the credential

## ADDED Requirements

### Requirement: Centralized Credentials Storage
The system SHALL provide a centralized "Credentials Vault" to securely store account details such as username, email, encrypted password, platform name, and notes.

#### Scenario: User saves a new credential
- **WHEN** an authorized user submits the "Add Credential" form
- **THEN** the system encrypts the password and stores the credential record

### Requirement: Granular Credential Sharing
The system SHALL allow users to share a specific credential with individual users or entire roles.

#### Scenario: Credential shared with a role
- **WHEN** a user creates a credential and selects the "Manager" role in the "Share With" dropdown
- **THEN** any user with the Manager role can view and decrypt the credential
- **AND** other users cannot see or decrypt the credential

#### Scenario: Credential kept private
- **WHEN** a user creates a credential without selecting any users or roles to share with
- **THEN** only the creator (and super admins) can view or decrypt it

### Requirement: Premium Vault Interface
The system SHALL display the credentials in a secure, glassmorphic UI where passwords are masked by default.

#### Scenario: Viewing the credentials list
- **WHEN** an authorized user opens the Credentials Vault
- **THEN** they see a visually appealing grid or list of credentials they have access to, with passwords masked (e.g., `••••••••`)

#### Scenario: Copying a password
- **WHEN** a user clicks the "Copy" or "Unmask" button on a credential
- **THEN** the system fetches the decrypted password from the API and allows the user to copy it to their clipboard

### Requirement: Password Timeline
The system SHALL maintain a history of all previous passwords for a credential, and users with access MUST be able to view and decrypt historical passwords.

#### Scenario: Viewing a previous password
- **WHEN** an authorized user opens the Timeline for a credential
- **THEN** they see a list of past updates (date, updater)
- **AND** they can unmask/copy the old password just like the current one

### Requirement: Update Request Workflow
Shared users SHALL NOT overwrite a credential directly; instead, they MUST submit an update request which requires manual approval from the credential owner or an admin.

#### Scenario: Submitting an update request
- **WHEN** a shared user (without global manage permissions) changes the password and clicks Save
- **THEN** the system creates a Pending Update Request instead of updating the credential immediately

#### Scenario: Approving an update request
- **WHEN** the credential owner approves the pending request
- **THEN** the system saves the old password to the Password Timeline
- **AND** updates the credential with the newly requested password

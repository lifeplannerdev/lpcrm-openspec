## Purpose
Defines the Centralized Credentials Vault for securely storing and sharing organizational account details.

## Requirements

### Requirement: Centralized Credentials Storage
The system SHALL provide a centralized "Credentials Vault" to securely store account details such as username, email, encrypted password, platform name, and notes.
Credentials SHALL optionally be linked to a dynamic "Credential Category" for organization.

#### Scenario: User saves a new credential with a dynamic category
- **WHEN** an authorized user submits the "Add Credential" form and selects a credential category from the dynamically fetched dropdown
- **THEN** the system encrypts the password and stores the credential record linked to that category via a foreign key

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

### Requirement: Premium Vault Interface
The system SHALL display the credentials in a secure, glassmorphic UI where passwords are masked by default.
The UI SHALL support filtering and grouping of credentials by their dynamic categories.
The UI SHALL provide action buttons for users to interact with credentials based on their permissions.

#### Scenario: Viewing the credentials list
- **WHEN** an authorized user opens the Credentials Vault
- **THEN** they see a visually appealing grid or list of credentials they have access to, with passwords masked (e.g., `••••••••`)

#### Scenario: Filtering credentials
- **WHEN** a user selects a category from the filter dropdown
- **THEN** the UI updates to display only credentials matching the selected category

#### Scenario: Grouping credentials
- **WHEN** a user toggles "Group by Category"
- **THEN** the UI displays credentials clustered visually under their respective category headers

#### Scenario: Category Badges
- **WHEN** viewing the credentials list
- **THEN** each credential visually displays its category using the category's assigned custom color and a matching `lucide-react` icon

#### Scenario: Copying a password
- **WHEN** a user clicks the "Copy" or "Unmask" button on a credential
- **THEN** the system fetches the decrypted password from the API and allows the user to copy it to their clipboard

#### Scenario: Editing a credential
- **WHEN** the authorized user (creator or admin) clicks the "Edit" button on a credential card
- **THEN** the system opens the Edit Modal populated with the credential's existing data, including shared users and roles
- **AND** saving the modal updates the credential directly

#### Scenario: Editing a credential without changing the password
- **WHEN** the user leaves the password field blank during an edit to indicate they want to keep it unchanged
- **THEN** the backend serializer strictly allows the empty string (`allow_blank=True`) to pass validation and safely preserves the existing password in the database

#### Scenario: Deleting a credential
- **WHEN** the authorized user (creator or admin) clicks the "Delete" button on a credential card
- **THEN** the system prompts for confirmation, and upon approval, permanently removes the credential

#### Scenario: Sharing a credential
- **WHEN** a user is creating or editing a credential in the modal
- **THEN** they can select specific users and/or roles from a dropdown
- **AND** upon saving, the backend grants those selected users/roles access to view the credential

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

### Requirement: Dynamic Credential Categories
The system SHALL allow authorized admins to define, edit, and delete dynamic credential categories (which include a name, color code, and icon name).

#### Scenario: Admin creates a new category
- **WHEN** a user with `credentials:manage` permission submits the "Add Category" form
- **THEN** the system saves the new category, making it immediately available in the dropdowns for all users

#### Scenario: Admin deletes a category
- **WHEN** a user with `credentials:manage` permission deletes a category
- **THEN** the system removes the category and safely unlinks (sets to null) any credentials that were attached to it, rather than deleting the credentials themselves

## MODIFIED Requirements

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

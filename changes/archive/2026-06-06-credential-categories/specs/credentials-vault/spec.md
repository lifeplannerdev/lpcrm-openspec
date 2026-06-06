## MODIFIED Requirements

### Requirement: Centralized Credentials Storage
The system SHALL provide a centralized "Credentials Vault" to securely store account details such as username, email, encrypted password, platform name, and notes.
Credentials SHALL optionally be linked to a dynamic "Credential Category" for organization.

#### Scenario: User saves a new credential with a dynamic category
- **WHEN** an authorized user submits the "Add Credential" form and selects a credential category from the dynamically fetched dropdown
- **THEN** the system stores the credential record linked to that category via a foreign key

### Requirement: Premium Vault Interface
The system SHALL display the credentials in a secure, glassmorphic UI where passwords are masked by default.
The UI SHALL support filtering and grouping of credentials by their dynamic categories.

#### Scenario: Filtering credentials
- **WHEN** a user selects a category from the filter dropdown
- **THEN** the UI updates to display only credentials matching the selected category

#### Scenario: Grouping credentials
- **WHEN** a user toggles "Group by Category"
- **THEN** the UI displays credentials clustered visually under their respective category headers

#### Scenario: Category Badges
- **WHEN** viewing the credentials list
- **THEN** each credential visually displays its category using the category's assigned custom color and a matching `lucide-react` icon

## ADDED Requirements

### Requirement: Dynamic Credential Categories
The system SHALL allow authorized admins to define, edit, and delete dynamic credential categories (which include a name, color code, and icon name).

#### Scenario: Admin creates a new category
- **WHEN** a user with `credentials:manage` permission submits the "Add Category" form
- **THEN** the system saves the new category, making it immediately available in the dropdowns for all users

#### Scenario: Admin deletes a category
- **WHEN** a user with `credentials:manage` permission deletes a category
- **THEN** the system removes the category and safely unlinks (sets to null) any credentials that were attached to it, rather than deleting the credentials themselves

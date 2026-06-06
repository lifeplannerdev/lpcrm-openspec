## Why

The current Credentials Vault allows users to store account details, but all credentials look the same. As the number of credentials grows, users need a way to categorize, filter, and group them. By introducing fully dynamic "Credential Categories", admins can define custom categories (with distinct colors and icons) to organize credentials efficiently. 

## What Changes

- Add a new dynamic `CredentialCategory` model to the backend (name, color, icon_name).
- Update the `Credential` model to have a foreign key to `CredentialCategory`.
- Build a "Manage Categories" UI accessible only to admins (via existing central permissions).
- Update the "Add Credential" and "Update Request" forms on the frontend to dynamically fetch categories for a dropdown.
- Update the Credentials Vault grid/list to display the category badge with Lucide React icons.
- Add filtering and grouping controls to the Credentials Vault UI so users can easily sort and find credentials by category.

## Capabilities

### New Capabilities
- None. This is an extension of the existing Credentials Vault.

### Modified Capabilities
- `credentials-vault`: The "Centralized Credentials Storage" and "Premium Vault Interface" requirements are changing to include dynamic categorization, filtering, and grouping of credentials.

## Impact

- **Backend Models**: `CredentialCategory` model created, `Credential` model updated with a foreign key (migration required).
- **Backend API**: New `CredentialCategoryViewSet`. Updates to `CredentialSerializer`.
- **Frontend UI**: `CredentialsVault.jsx` requires a new filter/grouping bar. A new "Manage Categories" modal for admins. Updates to existing forms.

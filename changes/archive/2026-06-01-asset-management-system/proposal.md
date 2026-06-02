## Why

The company currently lacks a centralized, efficient way to track physical and digital assets and their assignments to staff members. This change introduces an Asset Management module to improve accountability, streamline asset allocation, and provide clear visibility into which assets are held by which employees directly from their staff profiles.

## What Changes

- Create a new `Asset` model in the backend (likely in the `hr` app) to store asset details (`name`, `type`, `serial_number`, `status`, `company`, etc.) and a foreign key linking it to the specific staff member (`User` model).
- Implement an Asset Management UI (a "wow" page) that lists all assets, supports filtering/searching, allows adding/editing assets, and includes a company separation tab (e.g., LP vs. FLAG) optimized using SQL operations similar to the Leads module.
- Update the Staff Details page to display a new section showing all assets currently attached/assigned to that specific staff member.
- Introduce specific permissions for Asset Management (e.g., `view_asset`, `manage_asset`) and ensure this new screen access feature is listed and configurable in the Staff Permission Assignment screen.
- Develop the necessary API endpoints to handle asset CRUD operations, assignments, and retrieving assets by staff ID.

## Capabilities

### New Capabilities
- `asset-management`: Core capabilities for creating, viewing, updating, and deleting company assets, including tracking their status and assignment to staff members with company-based data segregation.

### Modified Capabilities
- `staff-management`: Updated requirements to display assigned assets on the individual staff details page and to include the new asset management access controls in the staff permissions assignment screen.

## Impact

- **Database**: Introduction of the new `Asset` model.
- **Backend APIs**: New endpoints in the CRM backend for asset management. Modification of the staff details endpoint to include attached assets.
- **Frontend UI**: A brand new Asset Management page and updates to the existing Staff Details and Permissions Assignment screens.
- **Permissions System**: Addition of new permission flags specifically for accessing and managing the asset inventory.

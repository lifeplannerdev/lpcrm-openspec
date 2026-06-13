## Why

The current Asset Management system uses a rigid, purely generic parent-child model (Mobile + SIM) with no concept of physical locations (Cabins, Reception) or dynamic asset categories. This creates a highly tedious data-entry process and prevents admins from generating flat, matrix-style inventory views that match their real-world mental models (e.g., grouping a complete "Desktop Setup" and assigning it to "Cabin 3" alongside an AC, while assigning a Mobile to "Jithin").

## What Changes

- Introduce a `Location` model to represent physical spaces (e.g., Cabins, Reception) where assets can be placed.
- Update the `Asset` model to support assigning an asset to either a `User`, a `Location`, or attaching it to a `parent_asset`.
- Replace the hardcoded `ASSET_TYPE_CHOICES` with a dynamic `AssetCategory` model to support an arbitrary number of asset types (e.g., Fans, ACs, Teapoys, Waste Bins).
- Add `primary_phone_number` and `secondary_phone_number` directly to the `Asset` model (or as specialized metadata) to flatten SIM tracking for Mobiles.
- Introduce a visual macro-dashboard (Space Inventory) and micro-dashboard (Cabin/Person details) in the frontend for powerful viewing and management.

## Capabilities

### New Capabilities
- `space-management`: Defines requirements for tracking physical locations and assigning assets to them instead of just users.
- `dynamic-asset-categories`: Defines requirements for managing an extensible list of asset categories.

### Modified Capabilities
- `staff-and-hr-management`: Modifies existing asset assignment constraints to support location assignments, removes hardcoded asset types, and updates the UI requirements to include Macro/Micro dashboards.

## Impact

- **Models**: `Asset` (hr app), New `Location` model, New `AssetCategory` model.
- **Frontend**: Major overhaul of `AssetManagementPage.jsx` to support macro/micro views, location selection, and bundled grouping.
- **APIs**: Asset CRUD endpoints need to support `location_id`, dynamic `category_id`, and updated filtering logic.

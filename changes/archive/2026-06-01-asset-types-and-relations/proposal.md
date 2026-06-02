## Why

The current asset management system relies on simple flat lists with free-text fields. This change introduces strict typings (dropdowns) to maintain clean data, adds specific hardware tracking (IMEI for Mobiles), and introduces relational asset tracking (attaching SIM cards to Mobiles) to accurately model real-world asset distributions where accessories or components follow a primary device.

## What Changes

- Change `asset_type` to a strict dropdown selection (Mobiles, Monitors, PC, Keyboard, Mouse, Laptops, SIM).
- Dynamically update the frontend "Serial Number" label to "IMEI Number" when "Mobiles" is selected.
- Add an `attached_to` (or `parent_asset`) self-referential foreign key to the `Asset` model to allow assets (like SIMs) to be linked to other assets (like Mobiles).
- Enforce logic where an attached asset (e.g., SIM) inherently inherits the assignee (`assigned_to`) of its parent asset (e.g., Mobile).
- Update the Staff view UI to nest attached assets under their parent devices for clear visual hierarchy.

## Capabilities

### New Capabilities
- `asset-relations`: Introducing the ability to link assets hierarchically (e.g., linking a SIM card to a Mobile phone) and inherit assignments.

### Modified Capabilities
- `asset-management-system`: Enhancing the existing asset creation/editing forms to support type dropdowns, dynamic labels (IMEI), and parent asset selection.

## Impact

- **Database**: The `hr_asset` table will require a new migration to add a self-referential ForeignKey (`parent_asset`).
- **Backend APIs**: The Asset serializers and views will need to handle hierarchical nesting and parent assignment logic.
- **Frontend UI**: The `AssetManagementPage` form will be updated heavily, and the `AssignedAssetsSection` component on the Staff page will be refactored to support rendering nested assets.

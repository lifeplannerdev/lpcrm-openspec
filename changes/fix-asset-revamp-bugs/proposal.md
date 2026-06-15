## Why

Recent changes including `asset-management-revamp` and `global-modal-redesign` introduced a few critical bugs. A build error is currently blocking deployment due to duplicated variable declarations in `AssetManagementPage.jsx`. Furthermore, the Space Inventory UI incorrectly lists personal assets as room fixtures, and the Staff Details page was never fully upgraded to the new asset data structure, causing missing data (due to referencing the deleted `asset_type` field) and lack of proper asset grouping.

## What Changes

- Fix the build error in `AssetManagementPage.jsx` by removing the duplicate declarations of `hasPermission` and `canManageAssets`.
- Update the Space Inventory modal in `AssetManagementPage.jsx` to filter out personal assets from the "Room Fixtures" list.
- Upgrade `StaffDetailsPage.jsx` to properly group assets into "Mobiles" (with nested SIM details), "Standalone SIMs", and "Responsible Areas".
- Fix `StaffDetailsPage.jsx` to use `category_details.name` instead of the deprecated `asset_type` field.

## Capabilities

### New Capabilities
None

### Modified Capabilities
- `staff-and-hr-management`: Updating the Staff Details page requirements to properly categorize and display the new asset structure.

## Impact

- `AssetManagementPage.jsx`
- `StaffDetailsPage.jsx`

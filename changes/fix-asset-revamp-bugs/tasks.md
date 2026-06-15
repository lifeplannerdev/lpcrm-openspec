## 1. Fix Asset Management Bugs

- [x] 1.1 In `AssetManagementPage.jsx`, delete the duplicated lines declaring `hasPermission` and `canManageAssets` (lines 71-72) to resolve the build error.
- [x] 1.2 In `AssetManagementPage.jsx`, within the `LocationDetailsView` component, update the filter for "Room Fixtures & General Assets" to include `!a.assigned_to` so personal assets assigned to users are excluded.

## 2. Upgrade Staff Details Profile

- [x] 2.1 In `StaffDetailsPage.jsx`, remove references to the deleted `asset.asset_type` property.
- [x] 2.2 Update `StaffDetailsPage.jsx` to parse and group the staff member's assets into "Mobile Phones" (showing primary/secondary SIM details and provider) and "Standalone SIMs" using `asset.category_details?.name` or presence of `provider`.
- [x] 2.3 Update the UI in `StaffDetailsPage.jsx` to render the grouped assets cleanly.
- [x] 2.4 Verify that "Responsible Areas" (locations) are correctly rendering in the `StaffDetailsPage.jsx`.

## Why

The current Asset Management system has a few critical bugs preventing accurate data entry and inventory tracking:
1. The `branch` assignment is not being saved when adding or editing an asset due to missing fields in the form submission.
2. Space Inventory does not show personal assets assigned to a cabin if the assigned user's HR profile location differs from that cabin.
3. The Location dropdown in the asset form shows all locations regardless of branch, leading to incorrect assignments.

These bugs must be fixed immediately to ensure accurate asset tracking.

## What Changes

- Add `branch` to the `FormData` object appended in `handleSubmit` in `AssetManagementPage.jsx`.
- Update the Space Inventory logic so it iterates through assets physically assigned to the selected location and groups them by their assigned users, rather than iterating through the location's `assigned_staff` (which relies purely on HR profiles).
- Update the Add/Edit Asset modal to hide the Location dropdown until a Branch is selected.
- Filter the Location dropdown options to only include locations where `loc.branch === selectedBranchId`.

## Capabilities

### New Capabilities

### Modified Capabilities
- `staff-and-hr-management`: Updating the asset form logic to properly save branch data and enforce dependent dropdowns for branch-location hierarchy. Additionally, modifying space inventory logic to accurately render personal assets regardless of the user's HR profile.

## Impact

- `lpcrm-frontend-main/src/Pages/AssetManagementPage.jsx`
- This is a pure frontend fix; backend models and serializers remain unaffected as they already support these relationships correctly.

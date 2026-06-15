## 1. Asset Form Logic

- [x] 1.1 In `AssetManagementPage.jsx` `handleSubmit`, add `if (formData.branch) formDataObj.append('branch', formData.branch);` to ensure the branch is saved to the database.
- [x] 1.2 In `AssetManagementPage.jsx` form render, update the "Assigned To (Location)" dropdown to only render or be enabled if `formData.branch` has a value.
- [x] 1.3 Update the mapping for the Location dropdown to filter locations by the selected branch (`locations.filter(loc => loc.branch === parseInt(formData.branch))`).

## 2. Space Inventory Rendering

- [x] 2.1 In `AssetManagementPage.jsx` Space Inventory view, update the "Assigned People & Personal Assets" section. Instead of iterating `locations.assigned_staff`, dynamically compute the occupants by finding all assets where `assigned_location === selectedLocationId` and `assigned_to` is not null.
- [x] 2.2 Group these assets by `assigned_to` and render a card for each user containing their respective assets.

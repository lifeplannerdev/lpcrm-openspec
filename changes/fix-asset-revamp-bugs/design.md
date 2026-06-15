## Context

The recent `asset-management-revamp` introduced primary/secondary SIMs to mobile phones and removed legacy statuses and parent-child asset relationships. However, a git merge issue led to duplicate variable declarations (`hasPermission` and `canManageAssets`) in `AssetManagementPage.jsx`, breaking the frontend build. Additionally, some UI components were not fully updated to reflect the new data model, leading to display bugs in the Space Inventory and Staff Details views.

## Goals / Non-Goals

**Goals:**
- Fix the build error by removing duplicated lines in `AssetManagementPage.jsx`.
- Fix the Space Inventory UI to correctly exclude personal assets from "Room Fixtures" (by checking `assigned_to` instead of just `assigned_location`).
- Update `StaffDetailsPage.jsx` to properly categorize and render the new asset structures.

**Non-Goals:**
- Refactoring the entire `AssetManagementPage.jsx` component.
- Modifying backend models or serializers.

## Decisions

- **Build Fix**: Simply delete the duplicate lines 71-72 in `AssetManagementPage.jsx`.
- **Space Inventory Fix**: The `Room Fixtures & General Assets` logic in `AssetManagementPage.jsx` will be updated from `a.assigned_location == location.id && !a.branch` to `a.assigned_location == location.id && !a.assigned_to`. This ensures that assets assigned to a person (even if they also have a location) only show up under the person.
- **Staff Details Fix**: In `StaffDetailsPage.jsx`, we will iterate through the user's assigned assets and correctly group them. We will stop using `asset.asset_type` (which was removed) and instead rely on `asset.category_details.name` or presence of `provider` and `primary_sim_details`.

## Risks / Trade-offs

- **Risk**: Other components might still be relying on `asset.asset_type`. 
  - **Mitigation**: A quick search of the frontend codebase ensures we catch any lingering uses of `asset_type` and replace them with `category_details.name`.

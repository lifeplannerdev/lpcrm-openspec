## Context

The `AssetManagementPage.jsx` component manages the creation and updating of assets. It communicates with the backend Django API. Recent updates to asset assignment logic introduced dependencies between branch and location, and un-linked people from location to asset, causing data loss during form submission and rendering issues in the Space Inventory view.

## Goals / Non-Goals

**Goals:**
- Fix the form submission so that the `branch` value is correctly preserved and sent to the backend.
- Correctly calculate personal assets for a physical space by scanning all assets that share the physical location and grouping by their assigned user.
- Enforce UI logic where a Location can only be selected after a Branch is selected, filtering the options to belong to the selected branch.

**Non-Goals:**
- Backend API modifications (the APIs already support these fields and relations properly).
- Changes to other modules like HR or Staff Profile.

## Decisions

- **Space Inventory Grouping**: We will iterate through all assets where `assigned_location === selectedLocationId` and `assigned_to` is not null. We will group these assets by `assigned_to` (the user ID) and display them under the assigned people section, ignoring `emp.location` from the HR profile. This is the source of truth for physical asset location.
- **Form Data Append**: We will simply add `if (formData.branch) formDataObj.append('branch', formData.branch);` to `handleSubmit` in `AssetManagementPage.jsx`.
- **Dependent Dropdown**: The `assigned_location` dropdown will be rendered conditionally or disabled until `formData.branch` is truthy. The options will be filtered using `locations.filter(loc => loc.branch === parseInt(formData.branch))`.

## Risks / Trade-offs

- **Risk**: Performance impact of grouping assets on the frontend.
  **Mitigation**: The number of assets per location is typically small, so an `O(N)` grouping operation in the render function is perfectly acceptable and imperceptible to users.

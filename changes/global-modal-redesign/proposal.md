## Why

Currently, all the large forms inside modals (like Asset Edit, Add Lead, Permissions, etc.) are built inside a structure that causes the entire dark backdrop to scroll. On smaller screens, this causes form fields at the very top (like Asset Name) to scroll upwards and hide underneath the sticky semi-transparent header, making them completely inaccessible or invisible to users. This creates a confusing user experience. We need to redesign the modals to ensure only the form body scrolls while the header and footer remain fixed, enforcing a strict maximum height.

## What Changes

- Redesign the underlying HTML/Tailwind structure of all major popups/modals across the system.
- Impose a strict maximum height (e.g., `max-h-[90vh]`) on the modal container so it never overflows the window.
- Make the header containing the title and close button fully fixed (`shrink-0`).
- Make the modal body scrollable (`overflow-y-auto`) with a customized internal scrollbar.
- Add a fixed footer for the "Save" and "Cancel" action buttons so users don't have to scroll all the way to the bottom just to save.
- Tidy up input field padding to make forms slightly more compact for a better popup experience.
- **BREAKING**: Introduce the concept of a `Branch` (e.g. Kochi Office, Kottayam Office, Kottayam HO) to the Asset Management module.
- Modify the `Location` model to belong to a specific `Branch` so that assets can be correctly filtered by office location.

## Capabilities

### New Capabilities

- `branch-management`: The ability to manage and assign physical office branches to spaces and assets.

### Modified Capabilities

- `frontend-and-ui`: Redesign the layout structure of frontend modals to prevent field overlap.

## Impact

This will touch several frontend pages including:
- `AssetManagementPage.jsx`
- `CandidateDetailPage.jsx`
- `FeesManagementPage.jsx`
- `LeadsPage.jsx`
- `RoleManagementPage.jsx`
- `TaskViewPage.jsx`
- Any other page using the `fixed inset-0 overflow-y-auto` full-screen modal pattern.

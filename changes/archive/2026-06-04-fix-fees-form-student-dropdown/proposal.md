## Why

The "Create Fee Account" form currently accepts a manually typed Student ID as a raw text input, which is a poor user experience. Users cannot be expected to memorize student IDs. We need a searchable dropdown to select a student, ensuring better usability and accurate data entry.

## What Changes

- Replace the raw text `<input>` for Student ID with a searchable dropdown (e.g., `<select>` or autocomplete component).
- Fetch the list of active students from the backend API to populate the dropdown.
- Ensure the selected student's ID is properly wired into the `createForm` state for submission.

## Capabilities

### New Capabilities
- `student-dropdown-in-fees`: Fetching and rendering a searchable list of students for creating fee accounts.

### Modified Capabilities


## Impact

- Frontend: `src/Pages/FeesManagementPage.jsx` will be updated to fetch and render student data.
- Backend API: Relies on existing students endpoint.

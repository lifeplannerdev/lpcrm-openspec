## Why

The navigation bar includes a "My Tasks" link pointing to `/mytasks`, but there is currently no page implemented for this route, resulting in a 404 Not Found error when users click it. This change introduces the missing page so users can view and manage their personal tasks.

## What Changes

- Create a new `MyTasksPage.jsx` component to serve as the user-facing task view.
- Update frontend routing (likely in `App.jsx` or similar) to map the `/mytasks` route to the new `MyTasksPage` component.
- The page will fetch and display tasks assigned to the currently logged-in user.

## Capabilities

### New Capabilities
- `my-tasks-view`: A capability allowing users to view and interact with their personal tasks on a dedicated page.

### Modified Capabilities
None

## Impact

- Frontend Routing: Adds a new route `/mytasks`.
- Frontend UI: Introduces a new page component in the `src/Pages/` directory.
- Backend API Interaction: The new page will consume existing task-related backend endpoints to fetch tasks for the current user.

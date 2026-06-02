## Context

The CRM application currently has a top navigation bar with a "My Tasks" link pointing to `/mytasks`. However, no matching route or component exists in the React frontend, leading to a 404 page. Users need a dedicated page to view tasks assigned specifically to them.

## Goals / Non-Goals

**Goals:**
- Implement the `MyTasksPage.jsx` component.
- Register the `/mytasks` route in the main frontend routing system.
- Fetch and display only the tasks assigned to the currently authenticated user.

**Non-Goals:**
- Creating new backend API endpoints (we will reuse the existing tasks API endpoint, applying query parameters or utilizing the endpoint's built-in user filtering if available).
- Modifying the existing admin-focused `TasksPage.jsx` logic.

## Decisions

- **Component Location:** The new component will be placed in `src/Pages/MyTasksPage.jsx`.
- **API Strategy:** The page will call the existing `GET /admin/tasks/` or `GET /tasks/` endpoint (depending on the backend setup). It will pass the current user's ID as a filter parameter (e.g., `?user=<user_id>`) to retrieve only the relevant tasks. If a dedicated `GET /my-tasks/` endpoint already exists in the backend, it will be used instead.
- **UI Consistency:** The page design will mirror the existing `TasksPage` or `ReportsPage`, using the same layout wrappers (e.g., `<Navbar />`), data tables, and card structures.

## Risks / Trade-offs

- **Backend Endpoint Support:** If the existing tasks endpoint does not support filtering by user ID, the backend will need to be updated. Mitigation: Verify the endpoint parameters before or during implementation. If an update is needed, it will be added to the tasks.

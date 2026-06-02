## Why

Currently, the mobile application's Tasks module acts as a read-only list. Users can view their pending tasks but cannot create new ones, edit existing details, or update a task's status. The Web Frontend has a robust CRUD interface for tasks (Create, Edit, Details, Kanban Status Updates). To make the mobile app truly useful for users on the go, we must bridge this gap and introduce Interactive Tasks to the mobile client.

## What Changes

- **Task Details Screen**: A dedicated screen (`TaskDetailsScreen`) to view the full description, assigned staff, deadlines, and current status of a specific task.
- **Create/Edit Task Forms**: Reusable forms to allow authorized users (users with `edit_tasks` permission) to create new tasks or modify existing ones directly from their phone.
- **Status Updates**: The ability to quickly update a task's status (e.g. from PENDING to COMPLETED) directly from the list or details view.
- **Floating Action Button (FAB)**: A global action button on the Tasks screen to quickly trigger the "Create Task" flow.

## Capabilities

### New Capabilities
- `mobile-tasks-crud`: Adds interactive forms and API mutations to Create, Read, Update, and manage Tasks in the mobile application.

### Modified Capabilities
- `mobile-app-navigation`: Updates the navigation stack to include modal screens for Task Creation and deep linking into Task Details.

## Impact

- **Mobile Frontend (`lpcrm-mobile`)**: Significant additions to `src/screens` (creating `TaskDetailsScreen.tsx`, `TaskFormScreen.tsx`). Addition of `@react-native-picker/picker` and `@react-native-community/datetimepicker` for form inputs. Updates to API client hooks to support mutations.
- **Backend API**: No changes required. The endpoints (`POST /tasks/`, `PUT /tasks/:id`, `PATCH /tasks/:id`) are already fully operational for the web app.

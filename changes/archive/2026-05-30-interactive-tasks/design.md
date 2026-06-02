## Context

The mobile app currently utilizes TanStack Query (`react-query`) in custom hooks like `useTasks.ts` to fetch data. However, there are no mutation hooks implemented for Tasks. The UI also needs form components for creating/editing tasks, which requires handling dates and dropdowns (e.g., assigning to staff).

## Goals / Non-Goals

**Goals:**
- Implement `useMutation` hooks for creating, updating, and deleting tasks.
- Create `TaskDetailsScreen`, `TaskFormScreen`.
- Integrate `@react-native-picker/picker` for dropdowns (priority, status, assigned_to).
- Integrate `@react-native-community/datetimepicker` for deadline selection.

**Non-Goals:**
- We are not implementing the Kanban drag-and-drop board on mobile. List view with a status dropdown is sufficient for touch interfaces.
- We will not implement task assignment to *multiple* users if the backend only supports single assignment.

## Decisions

- **Navigation**: `TaskFormScreen` will be presented as a standard pushed screen. We will add a Native Stack Navigator inside the Tasks tab to handle nested navigation for `/tasks/:id` and `/tasks/new`.
- **Form State**: We will use standard React `useState` for the form instead of complex libraries like `react-hook-form`, keeping it lightweight.
- **Role Permissions**: The "Create Task" FAB will only render if `user.permissions.includes('edit_tasks')` or if the user meets the backend `TASK_ASSIGNER` roles, matching the web app's security logic.
- **Aesthetics**: The new screens will strictly utilize the new Glassmorphism design system (`AnimatedGlassCard`, `ScreenWrapper` with gradient) created in the previous change.

## Why

The current permission system hardcodes role and company logic (e.g., `user.role === 'manager' && user.company === 'LP'`) directly into frontend components. This causes a "role explosion," makes the UI rigid, and creates security risks because business rules leak into the presentation layer. We need to centralize all permission evaluation in the backend as the "single source of truth," allowing the frontend to simply react to a dynamic JSON payload of allowed actions.

## What Changes

- **BREAKING**: Remove all role-based `if` statements and custom permission checks from frontend components (e.g., `StaffPermissionsModal.jsx`).
- Implement a Hybrid RBAC + ABAC engine in the Django backend.
- Update the login/session endpoint to return a consolidated `permissions` JSON payload containing allowed actions per resource (e.g., `leads: ["read", "create", "edit_own"]`).
- Update the React frontend context/store to manage this generic permissions payload.
- Create generic frontend wrapper components (e.g., `<Can perform="leads:edit">`) to simplify UI rendering based on permissions.

## Capabilities

### New Capabilities
- `backend-hybrid-permissions`: The core Django engine evaluating Roles and Attributes to generate the JSON permission payload.
- `frontend-permission-store`: The React context/provider and generic components that consume the backend payload and control UI visibility.

### Modified Capabilities
- `user-authentication`: The login response will now include the comprehensive permissions payload.

## Impact

- **Frontend**: Almost all UI components that conditionally render based on user roles will be updated to use the new permission store.
- **Backend APIs**: The login and `/api/user/me` endpoints will change their response schema to include `permissions`.
- **Backend Models**: New models for Roles, Permissions, and potentially Resource Policies will be introduced to support ABAC.

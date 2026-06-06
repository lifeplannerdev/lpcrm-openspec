## Context

Currently, the CRM handles permissions by checking user roles and companies directly in the frontend (e.g., `user.role === 'admin'`). This leads to a brittle frontend, role explosion, and potential security holes. The goal is to move the CRM to a Hybrid RBAC/ABAC model where the backend is the single source of truth for authorization, sending a unified `permissions` payload upon login.

## Goals / Non-Goals

**Goals:**
- Centralize all permission evaluation in the Django backend.
- Define a generic JSON schema for the permission payload.
- Update frontend context to consume the payload generically.
- Ensure backwards compatibility during the migration phase by supporting both legacy roles and the new permission array until full cutover.

**Non-Goals:**
- Completely rewriting the user authentication token logic (we just add permissions to the existing token/login payload).
- Implementing a dynamic UI builder for admins to edit permissions in Phase 1 (we will hardcode the Hybrid mapping in the backend first to prove the architecture, then build UI for it later).

## Decisions

**1. JSON Payload Structure**
*Decision*: The backend will send a mapping of resources to allowed actions.
*Example*:
```json
{
  "permissions": {
    "leads": ["read", "create", "edit_own", "delete_own"],
    "staff": ["read"],
    "attendance": ["read_tenant", "create"]
  }
}
```
*Rationale*: This is flat, easy for the frontend to parse, and allows simple checks like `permissions.leads.includes('edit_own')`.

**2. Backend Evaluation Engine**
*Decision*: We will implement a Permission Service in Django that hooks into the existing `user` and `company` fields on the `User` model.
*Rationale*: Instead of building a complex database schema immediately, we can map existing `Role` + `Company` logic to this new JSON payload in code. This makes the migration safer.

**3. Frontend Consumption**
*Decision*: Create a `usePermissions` React hook and a generic `<Can perform="resource:action">` component.
*Rationale*: Replaces `if (role === 'admin')` with declarative wrapper components that don't need to know *why* a user has permission.

## Risks / Trade-offs

- **Risk**: Missed permission check during migration leading to unauthorized access or broken UI.
  - *Mitigation*: Run both systems in parallel. Have the frontend check the new payload, but fallback to the old role logic if the new payload is missing or undefined during the transition.
- **Risk**: Payload size growth. If we have 100s of resources, the permissions JSON could get large.
  - *Mitigation*: The payload should only contain permissions the user actually has. If they have none for a resource, omit the resource key.

## Context

The current LPCrm application relies on Role-Based Access Control (RBAC) where roles like `ADMIN`, `CEO`, `HR` are hardcoded in the frontend navigation (`roles.js`) and backend API permission checks (`user.role in TOP_MANAGEMENT`). This rigid structure makes it impossible to grant exception permissions to specific users without creating entirely new roles. 

## Goals / Non-Goals

**Goals:**
- Implement granular, string-based permissions (e.g., `view_leads`, `edit_tasks`).
- Introduce Role Templates where assigning a role populates a default list of permissions.
- Make the frontend navigation and UI rendering completely driven by the `user.permissions` array.
- Create a management UI for Admins to customize individual user permissions.

**Non-Goals:**
- Completely remove the concept of Roles. Roles will remain as useful templates when creating/updating users.
- Implement complex Attribute-Based Access Control (ABAC) or row-level permissions at this stage.

## Decisions

**1. Storing Permissions as a JSONField on the User Model**
Instead of using Django's built-in `ContentType` based `auth.Permission` and `auth.Group` models, we will use a `JSONField` named `permissions` directly on the custom `User` model.
*Rationale:* Django's built-in permissions are tightly coupled to database models and require complex queries. Since the frontend UI (like rendering the "Reports" tab) requires arbitrary string permissions that don't always map to a database model, a flat JSON array `['view_reports', 'edit_tasks']` is significantly faster to query, simpler to send to the frontend, and easier to build a UI around.

**2. The Template Approach (Option A)**
When a user is created or their role is changed, the backend will look up the `ROLE_TEMPLATES` config and copy the array of permissions into the user's `permissions` JSONField. From that point on, the user's permissions are detached from the role and can be individually edited.
*Rationale:* It's the simplest approach to allow exceptions for specific users without building a complex engine for "negative/revoked" permissions.

## Risks / Trade-offs

- [Risk] Missing permissions after migration.
  - *Mitigation:* We will write a data migration script that loops through all existing users, checks their current `role`, and populates their `permissions` JSONField based on the new templates before deploying the frontend changes.
- [Risk] Desync between Role template updates and existing users. If we decide all `HR` roles should get a new `view_voxbay` permission, existing `HR` users won't get it automatically.
  - *Mitigation:* We will provide a "Reset to Default Role Permissions" button in the management UI, or run a backend script when global role changes are needed.

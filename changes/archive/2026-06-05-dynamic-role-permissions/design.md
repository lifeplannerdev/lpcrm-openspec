## Context

The current system relies on hardcoded role presets and legacy mapping for permissions. To provide fine-grained, manageable control to administrators, we need a DB-backed roles and permissions system. This will involve defining tables for roles, permissions, and their relations, and exposing endpoints for the frontend to manage them.

## Goals / Non-Goals

**Goals:**
- Provide DB schemas for `roles`, `permissions`, `role_permissions`, and `user_roles`.
- Implement CRUD APIs for roles and permissions management.
- Build a frontend UI to allow administrators to manage roles and their associated permissions.
- Remove hardcoded permission fallback logic from the backend.
- Ensure all existing permission checks seamlessly utilize the DB-backed permission data.

**Non-Goals:**
- Completely rewriting the frontend global permission store. We will keep the global store but enforce its usage exhaustively across the entire application.
- Overhauling authentication; we are only changing authorization (roles/permissions).

## Decisions

- **Database Structure:** We will use `roles`, `permissions`, `role_permissions` (join table for roles to permissions), and `user_roles` (join table for users to roles) to allow maximum flexibility.
- **Permission Granularity & Scoping:** Permissions will be granular and encode data scope (e.g., `leads:read_all`, `leads:read_tenant`, `leads:read_own`) so that backend `get_queryset` methods no longer rely on hardcoded roles like `FULL_ACCESS_ROLES`.
- **Exhaustive Frontend Enforcement:** Every single button, tab, and screen (all 25+ screens) MUST be wrapped with the `<Can>` component or equivalent route guards. The DB is the singular source of truth.
- **API Endpoints:**
  - `GET /api/roles`, `POST /api/roles`, `PUT /api/roles/:id`, `DELETE /api/roles/:id`
  - `GET /api/permissions`
  - `GET /api/roles/:id/permissions`, `PUT /api/roles/:id/permissions`
- **Fallback Removal & Initial Seeding:** The hardcoded mappings will be deleted. The database seeder will:
  - Create one single superuser `admin` with password `admin`.
  - Strip `is_superuser=True` and hardcoded admin bypasses from all other users.
  - Map all other existing users cleanly to their dynamic DB roles (MD, CEO, HR, etc.) without any hidden bypasses.

## Risks / Trade-offs

- **Risk: Breaking Access on Deployment** -> Mitigation: We must provide a database seed script that runs upon deployment to populate the DB with the existing hardcoded roles and their exact permission mappings so nobody loses access.
- **Risk: Frontend Caching Stale Permissions** -> Mitigation: Ensure that when an admin changes permissions for a role, the affected users have their session permissions refreshed or force them to re-fetch on next navigation, or at minimum document that changes take effect on next login.

## Context

The Credentials Vault currently stores all credentials generically. To improve user experience and organization, we are adding dynamic "Credential Categories". This will require updating the backend database schema to include a new model, adding API endpoints for admins to manage these categories, and updating the React frontend to fetch these dynamically and provide filtering and grouping features.

## Goals / Non-Goals

**Goals:**
- Add a new dynamic `CredentialCategory` model (name, color, icon_name).
- Add a `category` foreign key to the `Credential` model.
- Provide a "Manage Categories" UI on the frontend, accessible only if the user has `credentials:manage` permissions.
- Update frontend forms to fetch categories dynamically from the API.
- Add filtering and grouping controls to the Credentials Vault list view.
- Use `lucide-react` for category icons.

**Non-Goals:**
- Auto-categorizing existing credentials (migration will just leave them uncategorized or null initially).
- Complex custom icon uploads (we will stick to mapping a string name to a Lucide icon component).

## Decisions

- **Database Structure**: A new `CredentialCategory` table with `name`, `color` (hex string), and `icon_name` (string matching a Lucide icon). `Credential` gets a `category` ForeignKey allowing nulls (for uncategorized existing data).
- **Admin Access**: Since we don't set granular permissions per file, we will rely on the existing `credentials:manage` central permission. Only users with this permission can see the "Manage Categories" button and hit the `POST/PUT/DELETE` endpoints for categories.
- **Filtering UI**: A dropdown at the top of the page will let users filter by category. We will also add a "Group by Category" toggle that groups the map output into sections.

## Risks / Trade-offs

- **Risk**: Existing credentials will not have a category (ForeignKey will be null).
  - **Mitigation**: The UI must gracefully handle `null` categories (e.g., displaying an "Uncategorized" section or a default gray folder icon).
- **Risk**: A deleted category could break credentials attached to it.
  - **Mitigation**: Use `on_delete=models.SET_NULL` for the `category` foreign key in Django, so deleting a category safely uncategorizes its credentials instead of deleting them.

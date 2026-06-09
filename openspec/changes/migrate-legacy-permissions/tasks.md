## 1. Backend Seed Configuration Updates

- [x] 1.1 Update `accounts/permission_templates.py` to replace all legacy permission strings with the new `<resource>:<action>` equivalents for every role.
- [x] 1.2 Update `accounts/management/commands/seed_roles.py` to ensure it only assigns properly scoped strings (including updating the `HR` role explicit dictionary).
- [x] 1.3 Run the seed command to verify the output matches expectations without crashing.

## 2. Backend Data Migration

- [x] 2.1 Generate an empty Django migration file for the `accounts` app.
- [x] 2.2 Write a `RunPython` script in the migration to dynamically rename existing `AppPermission` records (e.g., `AppPermission.objects.filter(name='manage_asset').update(name='assets:manage')`).
- [x] 2.3 Run the migration against the local database to verify successful conversion.

## 3. Backend Code Updates

- [x] 3.1 Use `git grep` to find any hardcoded references to legacy permissions in the backend (e.g., `view_all_tasks`) and replace them with the scoped strings.

## 4. Frontend Code Updates

- [x] 4.1 Update `src/config/roles.js` to ensure the required resources match the new base resource names (e.g., `"dashboard"`, `"reports"`, `"staff"`).
- [x] 4.2 Use `git grep` across the frontend repository to find `hasPermission` or `hasAnyPermission` checks that use the legacy strings, replacing them with the new `<resource>:<action>` format.
- [x] 4.3 Verify that `PermissionsContext.jsx` accurately checks the new structures.
- [x] 4.4 Run a frontend build to ensure there are no breaking syntax errors.

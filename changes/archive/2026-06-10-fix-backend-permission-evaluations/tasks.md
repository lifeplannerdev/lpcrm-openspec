## 1. Automated Replacements

- [x] 1.1 Use a script or search-and-replace to update all occurrences of `in request.user.permissions` to use `has_dynamic_permission(request.user, '<perm>')` across all backend modules (e.g., `tasks`, `leads`, `trainers`, `fees`, `reports`).
- [x] 1.2 Update occurrences of `in (user.permissions or [])` to use `has_dynamic_permission(user, '<perm>')`.

## 2. Refactoring Helper Functions

- [x] 2.1 Identify custom helper functions like `_has_perm(user, perm)` and `_perm_list(user)`.
- [x] 2.2 Refactor `_has_perm` to internally call `has_dynamic_permission(user, perm)` to maintain localized logic while correctly evaluating RBAC rules.
- [x] 2.3 Ensure that `accounts/permissions.py` (which exports `has_dynamic_permission`) is imported wherever these replacements happen.

## 3. Verification

- [x] 3.1 Run Django checks (`python manage.py check`) to ensure no syntax errors were introduced during the replacements.
- [x] 3.2 Ensure there are no outstanding `request.user.permissions` checks in the backend codebase by running a final `git grep`.

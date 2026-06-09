## 1. Permission Class Updates

- [x] 1.1 Update `CredentialPermission.has_permission` in `lpcrmbackend-main/credentials/views.py` to allow `list`, `retrieve`, `history`, `requests`, and `propose_update` for all authenticated users without checking `request.user.permissions`.
- [x] 1.2 Update `CredentialPermission.has_permission` to use `has_dynamic_permission(request.user, 'credentials:manage')` for write actions (`create`, `update`, `partial_update`, `destroy`, `approve_request`, `reject_request`) instead of `request.user.permissions`.
- [x] 1.3 Update `CredentialPermission.has_object_permission` to use `has_dynamic_permission(request.user, 'credentials:manage')` instead of `request.user.permissions`.
- [x] 1.4 Update `CredentialCategoryPermission.has_permission` in `lpcrmbackend-main/credentials/views.py` to use `has_dynamic_permission(request.user, 'credentials:manage')` instead of checking `request.user.permissions`.

## 2. QuerySet Updates

- [x] 2.1 Update `CredentialViewSet.get_queryset` and `CredentialUpdateRequestViewSet.get_queryset` to use `has_dynamic_permission(request.user, 'credentials:manage')` instead of `request.user.permissions`.

## 3. Verification

- [x] 3.1 Verify no syntax errors in the backend with `python manage.py check`.

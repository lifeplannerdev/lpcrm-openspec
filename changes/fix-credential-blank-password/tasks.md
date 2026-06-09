## 1. Backend Serializer Fix

- [x] 1.1 Update `CredentialSerializer` password field in `lpcrmbackend-main/credentials/serializers.py` to allow blank values (`allow_blank=True`, `required=False`).
- [x] 1.2 Add a `validate` method to `CredentialSerializer` to strictly enforce that the password field is provided when creating a new credential (i.e. when `self.instance` is None).

## 2. Verification

- [x] 2.1 Verify no syntax errors in the backend with `python manage.py check`.

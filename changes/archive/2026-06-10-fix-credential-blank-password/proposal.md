## Why

When editing an existing credential in the UI, users are prompted to "Leave blank to keep unchanged" for the password field. When they submit the form, a blank password string (`""`) is sent to the backend. Because the `password` field on `CredentialSerializer` is strictly required and does not allow blank values, Django REST Framework immediately rejects the payload with a `400 Bad Request` ("This field may not be blank."), preventing users from assigning or updating the credential. This fix resolves the issue by allowing empty password strings during the serialization phase, which the update logic safely ignores.

## What Changes

- Modify `password` field in `CredentialSerializer` to allow blank values (`allow_blank=True`) and make it optional (`required=False`).
- Ensure the `update` method safely ignores empty string values when assigning the password to the credential instance.

## Capabilities

### New Capabilities
None.

### Modified Capabilities
- `credentials-vault`: Minor bug fix; the core requirements for managing credentials remain unchanged, but the validation logic for updating passwords will correctly support the intended blank-state behavior.

## Impact

- **Affected Code**: `lpcrmbackend-main/credentials/serializers.py` -> `CredentialSerializer`
- **APIs**: `PATCH /api/credentials/<id>/` (Updates)
- **Systems**: Credentials Vault frontend behavior (specifically sharing with users/roles or editing notes)

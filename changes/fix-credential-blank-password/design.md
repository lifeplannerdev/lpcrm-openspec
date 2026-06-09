## Context

The Credentials Vault frontend interface sends a blank password string (`""`) during a `PATCH` request when a user leaves the password field empty (indicating "keep unchanged"). Because the backend `CredentialSerializer` defines `password` as a `CharField(write_only=True)` without `allow_blank=True`, Django REST Framework defaults to strictly rejecting empty strings.

## Goals / Non-Goals

**Goals:**
- Prevent the `400 Bad Request` validation error when updating credentials with an empty password string.
- Safely ignore empty password strings in the `update` block so the existing password remains unchanged in the database.

**Non-Goals:**
- We are not changing how new passwords are encrypted or stored.
- We are not rewriting the frontend logic to omit the password key.

## Decisions

- **Modify Serializer Field Args**: We will add `required=False` and `allow_blank=True` to the `password` field definition in `CredentialSerializer`.
  *Rationale*: This is the idiomatic DRF way to allow a client to submit an empty string for a field that should conditionally be ignored without raising a validation error. 
  *Alternative*: We could update the React frontend to strip the `password` key entirely from the JSON payload if it's empty. However, fixing the backend validator is more robust and prevents future API consumers from hitting the same issue if they submit an empty string.

## Risks / Trade-offs

- **Risk**: Allowing a blank password might let users accidentally set their password to blank.
  **Mitigation**: The `update` method explicitly checks `if password:` (which evaluates `""` as False) before calling `set_password()`. Thus, an empty string will be ignored, and the password will remain unchanged. If a user actually wants a blank password, they can't set it via this mechanism, which is standard security practice for credentials anyway.

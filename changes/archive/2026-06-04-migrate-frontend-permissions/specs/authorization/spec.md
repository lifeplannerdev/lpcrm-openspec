## MODIFIED Requirements

### Requirement: Granular Authorization Checking
The frontend UI SHALL evaluate user access privileges using the dynamic `PermissionsContext` (`hasPermission`, `hasAnyPermission`) exclusively, evaluating the resource/action JSON map provided by the backend.

#### Scenario: User attempts to perform privileged action
- **WHEN** a user navigates to a restricted route or attempts to click an action button (e.g. Edit Lead)
- **THEN** the system SHALL consult `hasPermission('resource:action')` instead of interrogating raw array sets or computing string combinations based on `user.role`.

#### Scenario: Fallback behavior
- **WHEN** a user lacks explicit action permission
- **THEN** the component SHALL hide the restricted element or redirect the user away from restricted pages gracefully.

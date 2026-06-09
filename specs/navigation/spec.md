## Purpose
Defines the capabilities and requirements for this domain.

## Requirements

### Requirement: Role-Based Navigation Rendering
The navigation menu SHALL render items based on the user's granular permissions evaluated via the `hasPermission` hook, matching against resources and actions rather than legacy flat string matching.

#### Scenario: Admin views dashboard
- **WHEN** user logs in with a role granting `{"*": ["*"]}` or explicit resource access (e.g., `{"leads": ["read", "create"]}`)
- **THEN** the navigation bar SHALL display all menu items for which the user has matching read permissions via the `PermissionsContext`.

#### Scenario: Restricted user views dashboard
- **WHEN** user logs in with a role lacking `leads` read access
- **THEN** the Leads menu item SHALL NOT be rendered in the navigation bar.

### Requirement: SPA Routing Fallback
The server configuration SHALL route any unmatched request to the main `index.html` file to enable client-side routing.

#### Scenario: Direct navigation to a valid route
- **WHEN** user directly navigates to or refreshes a route that only exists in the SPA (e.g. `/leads`)
- **THEN** Vercel servers return the `index.html` file with a 200 OK status, instead of a 404.

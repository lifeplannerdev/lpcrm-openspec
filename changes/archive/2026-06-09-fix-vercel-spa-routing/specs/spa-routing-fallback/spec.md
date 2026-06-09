## ADDED Requirements

### Requirement: SPA Routing Fallback
The server configuration SHALL route any unmatched request to the main `index.html` file to enable client-side routing.

#### Scenario: Direct navigation to a valid route
- **WHEN** user directly navigates to or refreshes a route that only exists in the SPA (e.g. `/leads`)
- **THEN** Vercel servers return the `index.html` file with a 200 OK status, instead of a 404

## ADDED Requirements

### Requirement: Vercel Backend Integration
The mobile application SHALL communicate with the existing Node.js/Express backend hosted on Vercel.

#### Scenario: Fetching Data from Backend
- **WHEN** the app requests a list of tasks
- **THEN** it successfully connects to the Vercel API, parses the JSON response, and updates the local state

### Requirement: Network Error Handling
The application SHALL gracefully handle network errors, timeouts, and offline states since mobile connections can be unstable.

#### Scenario: API Timeout
- **WHEN** an API request times out due to poor connectivity
- **THEN** the application displays a user-friendly error message and offers a retry option

# multi-tenant-company-segregation Specification

## Purpose
TBD - created by archiving change multi-company-segregation. Update Purpose after archive.
## Requirements
### Requirement: Backend API Company Filtering
The system SHALL filter all core resource queries (Tasks, Leads, Staff, Penalties, Candidates, Students, Reports) by the requested company.

#### Scenario: User queries their own native company
- **WHEN** user makes a GET request for their own company (e.g., `user.company == 'LP'` querying `?company=LP`)
- **THEN** system returns records where `company='LP'`

#### Scenario: User queries other company with access_flag permission
- **WHEN** an LP user makes a GET request with `?company=FLAG` and possesses the `access_flag` permission
- **THEN** system returns records where `company='FLAG'`

#### Scenario: User queries other company without permission
- **WHEN** user makes a GET request for a company they do not belong to and lacks the `access_flag` permission
- **THEN** system returns a 403 Forbidden response

#### Scenario: User queries without specifying company
- **WHEN** user makes a GET request without a `company` parameter
- **THEN** system defaults to returning records for the user's native `company`

### Requirement: Per-Page Company Switcher Component
The UI SHALL provide a standalone Company Switcher tab component that can be rendered at the top of individual pages (Tasks, Staff, Leads) rather than in the global Navbar.

#### Scenario: User has cross-company access
- **WHEN** an LP user with the `access_flag` permission views a supported page
- **THEN** they see the Company Switcher tabs (`LP | FLAG`) at the top of the page content

#### Scenario: User changes company on a specific page
- **WHEN** user clicks `FLAG` on the Tasks page switcher
- **THEN** the Tasks page fetches and displays FLAG tasks, and the URL updates (e.g., `?view_company=FLAG`), but other open browser tabs (e.g., Staff page showing LP) remain unaffected

#### Scenario: User only has native access
- **WHEN** user lacks the `access_flag` permission
- **THEN** the Company Switcher component is hidden and the page always shows their native company's data


## MODIFIED Requirements

### Requirement: Bulk Lead Upload Processing
The system SHALL process bulk lead uploads efficiently using bulk database operations.

#### Scenario: Uploading a large Excel file
- **WHEN** user uploads a file with 5,000 leads
- **THEN** the system validates and inserts the leads within standard HTTP timeout limits (under 30 seconds)
- **AND** duplicate checks are performed optimally without O(N) database queries

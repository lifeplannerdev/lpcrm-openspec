## ADDED Requirements

### Requirement: Advanced Filtering by Marketing Fields
The system SHALL allow users to filter the leads list by `campaign_name`, `adset_name`, and `ad_name`.

#### Scenario: Filtering by Campaign
- **WHEN** the user selects a specific Meta Campaign from the filter UI
- **THEN** the list displays only leads associated with that campaign

### Requirement: Date-based Filtering (Today)
The system MUST provide a quick filter to view leads created "Today".

#### Scenario: Filtering for today's leads
- **WHEN** the user clicks the "Today" filter
- **THEN** the list displays only leads where `created_at` is the current day

### Requirement: Excel Export with Filters
The system SHALL allow users to export their current filtered view of leads to an Excel spreadsheet.

#### Scenario: Exporting a filtered list
- **WHEN** the user applies filters (e.g., Campaign="UK 2026", Date="Today") and clicks "Export"
- **THEN** the system generates and downloads an `.xlsx` file containing exactly the leads matching those filters

## Purpose
Defines the capabilities for capturing, filtering, processing, and viewing CRM leads, including advanced interfaces like Kanban and Split-Pane views.
## Requirements
### Requirement: Extend Lead Model for Marketing
The system SHALL extend the existing CRM Lead model to include marketing data fields.

#### Scenario: Storing marketing properties
- **WHEN** a lead is created from an Ad source
- **THEN** the system must store `campaign_name`, `adset_name`, `ad_name`, `meta_lead_id`, and `raw_form_data` correctly

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

### Requirement: Bulk Lead Upload Processing
The system SHALL process bulk lead uploads efficiently using bulk database operations.

#### Scenario: Uploading a large Excel file
- **WHEN** user uploads a file with 5,000 leads
- **THEN** the system validates and inserts the leads within standard HTTP timeout limits (under 30 seconds)
- **AND** duplicate checks are performed optimally without O(N) database queries

### Requirement: Split-Pane Master-Detail View
The Leads List page SHALL optionally render as a split-pane interface on desktop screens, displaying the list of leads on the left and a detailed preview panel on the right. On mobile screens (under 1024px), it SHALL render as a full-screen slide-over drawer to preserve context without compromising usability. The system SHALL use nested routing to maintain state across reloads.

#### Scenario: Selecting a lead on desktop
- **WHEN** user clicks on a lead row in the main table on a desktop device
- **THEN** the route updates to `/leads/:leadId` using nested routing
- **AND** a side panel slides in from the right containing the lead's core details and quick actions, while the table width compresses to accommodate it

#### Scenario: Selecting a lead on mobile
- **WHEN** user clicks on a lead row in the main table on a mobile device
- **THEN** the route updates to `/leads/:leadId` using nested routing
- **AND** a full-screen slide-over drawer covers the view, retaining the list's scroll position underneath

#### Scenario: Closing the preview
- **WHEN** user clicks the 'X' button, the backdrop, or presses Escape
- **THEN** the route updates to `/leads`
- **AND** the side panel collapses and returns focus to the main list

### Requirement: Kanban View for Leads
The system SHALL provide an alternate "Kanban" view for the Leads page, categorizing leads by their current status (e.g., Enquiry, Contacted, Qualified, Converted).

#### Scenario: Dragging a lead to a new status
- **WHEN** user drags a lead card from the "Enquiry" column and drops it into the "Contacted" column
- **THEN** the lead's status is instantly updated via an API call
- **AND** a success toast notification is displayed

#### Scenario: Accessing the Kanban board
- **WHEN** user clicks the "Kanban View" toggle on the Leads list page
- **THEN** the table view is hidden and the drag-and-drop board is displayed

### Requirement: Unified Story Timeline
The lead details page SHALL display a single vertical timeline combining Follow-ups, Assignment History, and Processing Updates.

#### Scenario: Viewing a lead's history
- **WHEN** user navigates to a lead detail page
- **THEN** they see a chronological timeline of all events (creation, assignments, calls made, status changes) in one scrollable view

### Requirement: Inline Timeline Actions
The timeline SHALL allow users to directly schedule follow-ups or add notes without leaving the timeline view.

#### Scenario: Adding a note to the timeline
- **WHEN** user clicks "Add Note" within the timeline header
- **THEN** an inline form appears allowing immediate submission of a new remark or follow-up


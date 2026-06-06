## Purpose
Defines the capabilities and requirements for this domain.

## Requirements

### Requirement: Student Management Workspace
The system SHALL provide a student workspace with list, detail, create, and edit surfaces that support search, pagination, status filters, branch filters, and batch filters.

#### Scenario: User opens the students list
- **WHEN** an authorized user opens the students section
- **THEN** the system displays a paginated student list with search and filter controls that match the CRM theme

#### Scenario: User filters students
- **WHEN** the user applies a status, batch, or branch filter
- **THEN** the system returns only students matching the selected criteria

### Requirement: Student Lifecycle Management
The system SHALL support the full student lifecycle including active, paused, completed, and dropped states.

#### Scenario: Admin updates a student status
- **WHEN** an authorized user updates a student from Active to Paused or Completed
- **THEN** the system saves the new lifecycle state and reflects it in the student list and detail view

### Requirement: Student Detail Tabs
The system SHALL present student details in a tabbed layout that includes profile data, attendance history, and fee summary entry points.

#### Scenario: User opens a student profile
- **WHEN** the user opens a student detail page
- **THEN** the system shows the student's profile, attendance context, and fee summary tabs within a single CRM-styled layout

### Requirement: Student Access Scoping
The system SHALL restrict student editing to users with the appropriate student permissions while allowing trainers to view only the students assigned to them.

#### Scenario: Trainer opens the students list
- **WHEN** a trainer opens the students workspace
- **THEN** the system shows only the trainer's assigned students and hides create or edit controls unless explicit write permission is granted

### Requirement: CRM Theme Consistency
The system SHALL render all student screens using the established CRM visual language, including the same spacing, gradients, card treatment, and navigation patterns used elsewhere in the app.

#### Scenario: User navigates between CRM modules
- **WHEN** the user switches from leads or reports to students
- **THEN** the student screens remain visually consistent with the rest of the CRM

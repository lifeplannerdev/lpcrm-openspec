## ADDED Requirements

### Requirement: Advanced Attendance Filtering
The system SHALL provide filters by trainer, location, and dynamically exclude dropout students from the attendance view.

#### Scenario: Filtering active students for a trainer
- **WHEN** user selects a trainer and location
- **THEN** system lists all active students (excluding dropouts) matching the criteria

### Requirement: Toggle-based Attendance
The system SHALL allow users to mark all listed students present or absent with a single toggle action.

#### Scenario: Toggling all present
- **WHEN** user clicks "Mark All Present" toggle
- **THEN** system updates the status of all visible students to present

# academic-management Specification

## Purpose
TBD - created by archiving change crm-production-enhancements. Update Purpose after archive.
## Requirements
### Requirement: Hierarchical Academic Batches
The system SHALL structure academic batches based on an Academic Year -> General/Grade hierarchy.

#### Scenario: Viewing batches
- **WHEN** user views the academic section
- **THEN** system organizes batches under their respective academic years

### Requirement: Academic Date Tracking
The system SHALL track Admission Date, Model Exams Date, and Final Exams Date for student batches.

#### Scenario: Scheduling exams
- **WHEN** admin inputs model and final exam dates for a batch
- **THEN** system stores and displays these dates correctly within the academic view

### Requirement: Marks Achieved Tracking
The system SHALL support tracking the "Marks Achieved" for students in their Model Exams and Final Exams.

#### Scenario: Trainer enters exam marks
- **WHEN** a trainer inputs the model exam score for a student in a batch
- **THEN** the system saves the `ExamResult` linking the student to the score

### Requirement: Tabbed Status Filtering for Students
The system SHALL present students in a tabbed UI to clearly separate them by status (Active, Paused, Dropped, Completed).

#### Scenario: User clicks "Dropped" tab
- **WHEN** the user switches to the "Dropped" tab on the Students page
- **THEN** the grid only displays students whose status is Dropped


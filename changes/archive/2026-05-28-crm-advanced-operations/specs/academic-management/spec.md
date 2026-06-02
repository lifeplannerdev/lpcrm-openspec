## ADDED Requirements

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

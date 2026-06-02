## ADDED Requirements

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

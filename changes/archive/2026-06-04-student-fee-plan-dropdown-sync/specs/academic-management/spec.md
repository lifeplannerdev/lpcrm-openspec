## ADDED Requirements

### Requirement: Fee-Aware Academic Enrollment Views
The system MUST show linked fee-plan status in academic management views so staff can see whether a student is fully set up for the active academic batch.

#### Scenario: Batch roster shows fee state
- **WHEN** an authorized user opens a batch or student roster in academic management
- **THEN** the system SHALL display whether each student has no fee plan, a pending fee setup, an active fee plan, or an overdue fee account

#### Scenario: Academic lifecycle reflects fee linkage
- **WHEN** a student is moved between batches or enrollment states
- **THEN** the system SHALL preserve the linked fee account and keep the academic record aligned with the current fee state

### Requirement: Default Fee Template Awareness
The system MUST allow academic enrollment flows to understand the default fee template context for a batch or program when one is configured.

#### Scenario: Batch has a default fee template
- **WHEN** an admin configures a default fee template for an academic batch
- **THEN** the system SHALL surface that template as the suggested fee plan during student enrollment

#### Scenario: No batch default exists
- **WHEN** a batch has no default fee template
- **THEN** the system SHALL require the fee plan to be chosen explicitly from the fee template catalog during accounting setup

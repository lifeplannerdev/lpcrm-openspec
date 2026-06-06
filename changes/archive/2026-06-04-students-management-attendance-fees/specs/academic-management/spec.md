## ADDED Requirements

### Requirement: Academic Fee Plan Linking
The system SHALL allow academic batches and course levels to map to default fee plans and payment structures.

#### Scenario: Batch uses a default fee plan
- **WHEN** an administrator configures an academic batch
- **THEN** the system allows the batch to reference a default fee plan such as one-time, installment, or monthly pricing

### Requirement: Academic and Fee Policy Integration
The system SHALL allow academic records to surface fee status context so operations can see how collections and attendance relate to the student lifecycle.

#### Scenario: Staff reviews a batch
- **WHEN** a user opens an academic batch
- **THEN** the system can show linked fee plan and attendance policy context for that batch

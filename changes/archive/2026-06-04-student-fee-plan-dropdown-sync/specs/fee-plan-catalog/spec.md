## ADDED Requirements

### Requirement: Managed Fee Plan Templates
The system MUST provide a company-scoped fee plan catalog containing the standard fee templates used for student enrollment and fee account creation.

#### Scenario: Accounting views available fee templates
- **WHEN** an authorized accounting user opens the fee setup screen for a company
- **THEN** the system SHALL display the active fee templates for that company as selectable options

#### Scenario: Standard plans are represented in the catalog
- **WHEN** the catalog is loaded for FLAG
- **THEN** the system SHALL include templates for the known standard plans such as one-time package, installment package, monthly plan, and level-based plans

### Requirement: Template-Driven Fee Account Autofill
The system MUST populate fee account fields from the selected fee template so staff do not manually type standard plan names or pricing.

#### Scenario: Template selection fills the form
- **WHEN** the user selects a fee template from the dropdown
- **THEN** the system SHALL populate plan name, plan code, plan type, total due, registration amount, due day, and any template defaults into the fee account form

#### Scenario: Template snapshot is preserved
- **WHEN** a fee account is created from a selected template
- **THEN** the system SHALL store a snapshot of the template data on the fee account so future catalog edits do not change historical student contracts

### Requirement: Controlled Custom Overrides
The system MUST allow accounting users to override template-derived values only through explicit fee restructuring or controlled override fields.

#### Scenario: Exceptional plan changes are recorded
- **WHEN** an accounting user changes the plan after creation due to a special case
- **THEN** the system SHALL record the override as a fee adjustment or restructure event instead of silently replacing the original template selection

#### Scenario: Non-accounting users cannot override plans
- **WHEN** a trainer or other read-only user views a fee account
- **THEN** the system SHALL not allow manual edits to the template-derived fee plan fields

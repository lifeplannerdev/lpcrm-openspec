## Purpose
Defines the capabilities for managing student fees, creating fee catalogs and templates, tracking installments, recording payments, and synchronizing fee states with student enrollment records.

## Requirements

### Requirement: Fee Catalog and Plan Templates
The system SHALL maintain reusable fee catalog templates for level-based fees, package-based fees, one-time payment offers, installment plans, and monthly payment plans.

#### Scenario: Accounting views available fee templates
- **WHEN** an authorized accounting user opens the fee setup screen for a company
- **THEN** the system SHALL display the active fee templates for that company as selectable options

#### Scenario: System seeds fees from the workbook
- **WHEN** the existing spreadsheet data is imported
- **THEN** the system maps the workbook rows into reusable fee templates and structured student-level payment records

### Requirement: Authorized users can create fee plan templates
The frontend SHALL provide a user interface to create new fee plan templates.

#### Scenario: Successful creation of a new fee template
- **WHEN** an authorized user opens the "Create Template" modal, fills in the required fields, and submits
- **THEN** the template is created in the backend and the frontend refreshes the list

#### Scenario: Dynamic fields based on plan type
- **WHEN** the user selects `MONTHLY` or `INSTALLMENT` as the plan type
- **THEN** the form SHALL reveal additional relevant inputs

### Requirement: Template-Driven Fee Account Autofill
The system MUST populate fee account fields from the selected fee template so staff do not manually type standard plan names or pricing.

#### Scenario: Template selection fills the form
- **WHEN** the user selects a fee template from the dropdown
- **THEN** the system SHALL populate plan name, plan type, total due, and template defaults into the fee account form

### Requirement: Searchable Student Dropdown in Fee Form
The system SHALL display a searchable dropdown for selecting a student in the Create Fee Account form instead of a manual text input.

#### Scenario: Successful student selection
- **WHEN** user opens the Create Fee Account form and interacts with the Student input
- **THEN** system displays a list of active students fetched from the backend and allows selection

### Requirement: Controlled Custom Overrides
The system MUST allow accounting users to override template-derived values only through explicit fee restructuring or controlled override fields.

#### Scenario: Exceptional plan changes are recorded
- **WHEN** an accounting user changes the plan after creation due to a special case
- **THEN** the system SHALL record the override as a fee adjustment or restructure event instead of silently replacing the original template selection

### Requirement: Fee Account Management
The system SHALL provide an accounting-owned fee management workspace for defining student fee structures, dues, and payment status.

#### Scenario: Accounting user opens fees
- **WHEN** an accounting user opens the fees section
- **THEN** the system displays fee accounts, due balances, and payment status controls for the relevant students

### Requirement: Fee Plan and Installment Tracking
The system SHALL support fee plans with installments, due dates, discounts, payment milestones, and plan versioning.

#### Scenario: Accounting user creates a fee plan
- **WHEN** the accounting user enters fee amounts and installment dates for a student or batch
- **THEN** the system stores the fee structure and exposes the outstanding balance in subsequent views

### Requirement: Fee Payment Recording
The system SHALL allow authorized finance users to record payments, partial payments, adjustments, refunds, and receipt references.

#### Scenario: Accounting user records a payment
- **WHEN** the accounting user posts a payment against a student's fee account
- **THEN** the system updates the paid amount, outstanding balance, and payment history

#### Scenario: Installment receives a partial payment
- **WHEN** a student pays less than the scheduled installment amount
- **THEN** the system records the installment as partially paid, carries forward the remainder, and keeps the account open

### Requirement: Trainer Read-Only Fee Access
The system SHALL allow trainers to view fee status for their assigned students without permitting fee edits, receipt posting, or balance adjustments.

#### Scenario: Trainer opens a fee summary
- **WHEN** a trainer views a student fee screen
- **THEN** the system displays fee status and balance information in read-only mode and hides all write actions

### Requirement: Fee Audit Trail
The system SHALL record fee changes with actor, timestamp, and change type so accounting actions can be audited later.

#### Scenario: Accounting user updates a fee record
- **WHEN** a fee amount, receipt, or adjustment changes
- **THEN** the system stores the change in an audit trail showing who changed it and when

### Requirement: Fee Summary Reporting
The system SHALL provide fee summary views that show total due, total paid, overdue amounts, collection status, and fee plan type by student, batch, branch, or company.

#### Scenario: Manager reviews fee performance
- **WHEN** an authorized manager opens the fee summary report
- **THEN** the system shows aggregated collections and outstanding balances using the current student set

### Requirement: Fee Overdue and Restructure Handling
The system SHALL flag overdue fee accounts, support plan restructuring, and preserve the prior contract history whenever a student changes payment mode.

#### Scenario: A fee plan becomes overdue
- **WHEN** a scheduled due date passes without full payment
- **THEN** the system marks the account overdue and exposes the overdue amount in the student and accounting views

### Requirement: Student Enrollment and Fee Linkage
The system MUST keep the academic student record and the linked fee account synchronized so both sides reflect the same enrollment state.

#### Scenario: New student enrollment awaits fee setup
- **WHEN** a student is created without an assigned fee plan
- **THEN** the system SHALL mark the student as pending fee setup and expose that state in both academic and accounting views

### Requirement: Shared Fee State Across Views
The system MUST present the same fee status, balance, and plan summary in the student workspace, trainer view, and accounting workspace.

#### Scenario: Student detail shows the current fee summary
- **WHEN** an authorized user opens a student detail page
- **THEN** the system SHALL display the current fee plan, total due, paid amount, balance due, and overdue amount from the backend source of truth

### Requirement: Fee Event Notifications
The system SHALL generate fee-related notifications for required personnel when a payment is due, overdue, partially paid, or restructured.

#### Scenario: Payment reminder is due soon
- **WHEN** a fee installment is approaching its due date
- **THEN** the system sends a reminder to the configured accounting and management recipients

#### Scenario: Accounting receives enrollment notification
- **WHEN** a student enrollment is created and the fee plan is still pending
- **THEN** the system SHALL notify accounting that a fee plan must be assigned

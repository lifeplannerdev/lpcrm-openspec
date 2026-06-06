## ADDED Requirements

### Requirement: Fee Catalog and Plan Templates
The system SHALL maintain reusable fee catalog templates for level-based fees, package-based fees, one-time payment offers, installment plans, and monthly payment plans.

#### Scenario: Accounting user views standard plans
- **WHEN** an accounting user opens the fee catalog
- **THEN** the system shows the standard plans such as level-based fees, full-package pricing, installment plans, and monthly plans

#### Scenario: System seeds fees from the workbook
- **WHEN** the existing spreadsheet data is imported
- **THEN** the system maps the workbook rows into reusable fee templates and structured student-level payment records

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

#### Scenario: Student changes from one-time payment to installments
- **WHEN** a student who originally chose a one-time payment can no longer pay in full
- **THEN** the system allows an authorized user to convert the student to an installment plan and retains the original contract history

#### Scenario: Special monthly structure is selected
- **WHEN** the accounting user selects the monthly payment structure from the fee catalog
- **THEN** the system stores the registration amount, monthly amount, term length, and due schedule as a structured plan

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

#### Scenario: An authorized user restructures a plan
- **WHEN** accounting changes a student's plan from one-time to installments or from installments to another approved structure
- **THEN** the system creates a new plan version and keeps the original plan for audit purposes

### Requirement: Fee Notifications
The system SHALL generate fee-related notifications for required personnel when a payment is due, overdue, partially paid, or restructured.

#### Scenario: Payment reminder is due soon
- **WHEN** a fee installment is approaching its due date
- **THEN** the system sends a reminder to the configured accounting and management recipients

#### Scenario: Overdue alert is created
- **WHEN** a student becomes overdue
- **THEN** the system notifies the required personnel and shows the alert in the fee workspace

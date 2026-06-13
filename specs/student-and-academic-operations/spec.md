## Purpose
Unified specification for student-and-academic-operations.

## Requirements

**Subdomain:** student-management

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


**Subdomain:** academic-management

### Requirement: Fee-Aware Academic Enrollment Views
The system MUST show linked fee-plan status in academic management views so staff can see whether a student is fully set up for the active academic batch.

#### Scenario: Batch roster shows fee state
- **WHEN** an authorized user opens a batch or student roster in academic management
- **THEN** the system SHALL display whether each student has no fee plan, a pending fee setup, an active fee plan, or an overdue fee account

#### Scenario: Academic lifecycle reflects fee linkage
- **WHEN** a student is moved between batches or enrollment states
- **THEN** the system SHALL preserve the linked fee account and keep the academic record aligned with the current fee state

### Requirement: Academic Batch Default Fee Template
The system MUST allow administrators to configure a default fee template for each Academic Batch, and the enrollment flows MUST understand this context.

#### Scenario: Configuring a Default Fee Template
- **WHEN** an admin creates or edits an Academic Batch in the UI
- **THEN** they are presented with a dropdown of active fee templates to select as the default

#### Scenario: Auto-suggesting Fee Template during Enrollment
- **WHEN** an admin selects an Academic Batch during student enrollment
- **THEN** the system automatically pre-selects the corresponding default fee template in the fee plan dropdown

#### Scenario: No batch default exists
- **WHEN** a batch has no default fee template
- **THEN** the system SHALL require the fee plan to be chosen explicitly from the fee template catalog during accounting setup



**Subdomain:** advanced-attendance

### Requirement: Advanced Attendance Filtering
The system SHALL provide filters by trainer, location, student status, and permission scope, and it SHALL exclude dropped or completed students from the attendance marking view.

#### Scenario: Filtering active students for a trainer
- **WHEN** user selects a trainer and location
- **THEN** system lists only the active students that match the criteria and that the user is allowed to see

#### Scenario: Excluding inactive students
- **WHEN** a trainer opens the attendance workspace
- **THEN** the system omits students whose status is Dropped or Completed from the marking list



### Requirement: Toggle-based Attendance
The system SHALL allow authorized users to mark all listed students present or absent with a single toggle action, and trainers SHALL only mark attendance for their assigned students.

#### Scenario: Toggling all present
- **WHEN** user clicks "Mark All Present" toggle
- **THEN** system updates the status of all visible students to present

#### Scenario: Trainer marks a student not assigned to them
- **WHEN** a trainer attempts to mark attendance for a student outside their assignment
- **THEN** the system rejects the change and keeps the record unchanged

### Requirement: Permission-Based Attendance Editing
The system SHALL hide attendance edit actions from users who only have read-only attendance access.

#### Scenario: Read-only user opens attendance
- **WHEN** a user with view-only attendance access opens the attendance page
- **THEN** the system shows attendance history but disables or hides marking controls




**Subdomain:** fees-management

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
The system SHALL provide fee summary dashboard components within the primary fee management workspace that show total due, total paid, overdue amounts, and collection status.

#### Scenario: Manager reviews fee performance
- **WHEN** an authorized manager opens the fees management workspace
- **THEN** the system shows aggregated collections and outstanding balances as a dashboard using the current student set

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
The system SHALL generate fee-related notifications for required personnel using Celery Beat for scheduled tasks when a payment is due, overdue, partially paid, or restructured, and MUST instantly notify accounting upon enrollment anomalies.

#### Scenario: Payment reminder is due soon
- **WHEN** a scheduled daily Celery Beat task identifies a fee installment approaching its due date
- **THEN** the system sends a reminder to the configured accounting and management recipients

#### Scenario: Accounting receives enrollment notification
- **WHEN** a student enrollment is created and the fee plan is still pending (no template provided)
- **THEN** the system SHALL immediately notify accounting that a fee plan must be assigned


**Subdomain:** branch-management
### Requirement: Branch Entity Creation
The system SHALL support managing multiple Branches (e.g., Kochi, Kottayam) via a dedicated database model.

#### Scenario: Admin creates branch
- **WHEN** an admin creates a new Branch
- **THEN** it becomes available in dropdown menus across the system

### Requirement: Branch-wise Filtering
The system SHALL allow filtering Students, Trainers, and Attendance records by Branch.

#### Scenario: User filters students by branch
- **WHEN** a user selects "Kochi" from the branch filter on the Students list
- **THEN** the list displays only students assigned to the Kochi branch




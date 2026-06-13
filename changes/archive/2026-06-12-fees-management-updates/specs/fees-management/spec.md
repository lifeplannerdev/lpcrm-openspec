## MODIFIED Requirements

### Requirement: Fee Summary Reporting
The system SHALL provide fee summary dashboard components within the primary fee management workspace that show total due, total paid, overdue amounts, and collection status.

#### Scenario: Manager reviews fee performance
- **WHEN** an authorized manager opens the fees management workspace
- **THEN** the system shows aggregated collections and outstanding balances as a dashboard using the current student set

### Requirement: Fee Event Notifications
The system SHALL generate fee-related notifications for required personnel using Celery Beat for scheduled tasks when a payment is due, overdue, partially paid, or restructured, and MUST instantly notify accounting upon enrollment anomalies.

#### Scenario: Payment reminder is due soon
- **WHEN** a scheduled daily Celery Beat task identifies a fee installment approaching its due date
- **THEN** the system sends a reminder to the configured accounting and management recipients

#### Scenario: Accounting receives enrollment notification
- **WHEN** a student enrollment is created and the fee plan is still pending (no template provided)
- **THEN** the system SHALL immediately notify accounting that a fee plan must be assigned

## MODIFIED Requirements

### Requirement: Student and Finance Permission Vocabulary
The system SHALL recognize student, attendance, finance, and credentials permission strings used by the CRM UI and backend authorization layer.

#### Scenario: New permission string is validated
- **WHEN** the system evaluates `view_students`, `mark_attendance`, `view_fees`, `manage_fees`, `view_credentials`, or `manage_credentials`
- **THEN** the permission engine accepts those strings as valid permissions

#### Scenario: Expanded finance permissions are evaluated
- **WHEN** the system evaluates `restructure_fees`, `record_partial_payment`, `issue_fee_notice`, or `view_fee_reports`
- **THEN** the permission engine accepts those strings as valid permissions

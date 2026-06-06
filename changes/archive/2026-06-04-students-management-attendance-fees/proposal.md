## Why

The CRM already has a partial students and attendance stack, but it does not yet behave like a production-grade academic operations system. Fees are not first-class, attendance permissions are inconsistent, and trainers, accounting, and admins need clearly separated access so the platform can support real school or institute workflows without accidental write access.

## What Changes

- Expand the Students section into a complete student management workspace with profile details, batch/branch assignment, status lifecycle, and linked attendance and fee views.
- Add a dedicated Fees management experience for accounting users to create and manage fee plans, installments, receipts, balances, discounts, payment status updates, restructures, and partial-payment handling.
- Keep trainers able to view fee information in read-only mode, while restricting all fee creation and payment management actions to accounting and other explicitly authorized finance roles.
- Update attendance screens so trainers can continue to mark and review attendance for their assigned students, while higher-privilege users can view cross-trainer attendance data.
- Revamp the academic and fee relationship so course level, package, installment schedule, and attendance policy are connected instead of being maintained as disconnected spreadsheets.
- Align student-related screens with the existing CRM visual theme so the student, attendance, and fees surfaces feel native to the rest of the product.
- Update role and permission handling so student, attendance, and fee screens are driven by explicit permissions instead of ad-hoc role checks.
- Add auditability around fee changes and attendance updates so accounting and operations can trace who changed what and when.

## Capabilities

### New Capabilities
- `student-management`: Complete student profile and lifecycle management, including batch assignment, branch assignment, status tracking, and student detail views.
- `fees-management`: Accounting-owned fee setup and collection workflow, including fee plans, dues, receipts, installment tracking, payment history, restructuring, and partial payment handling.

### Modified Capabilities
- `advanced-attendance`: Attendance screens and workflows need permission-aware access, trainer-scoped editing, and broader read access for authorized operations users.
- `academic-management`: Academic batches and level-based fee mapping need to connect to fee plans and attendance policy so the academic workflow is not isolated from collections.
- `granular-permissions-engine`: Add and formalize student, attendance, and fee permissions and update role templates to distinguish accounting write access from trainer read-only access.
- `permissions-management-ui`: Expose the new student, attendance, and fee permissions in the permissions editor so admins can assign them consistently.

## Impact

- Backend models, serializers, permissions, services, and API routes for students, attendance, and fees.
- Frontend routes, pages, tabs, tables, forms, modals, and filters for student management, attendance marking, and fees management.
- Structured import or backfill from the existing spreadsheet-based fee ledger into the new fee domain.
- Permission templates and permission editor UI for accounting, trainers, admins, and other staff roles.
- Database schema for fee plans, invoices, receipts, balances, and audit records.
- Theme and layout adjustments so the new student section matches the CRM's existing visual language.

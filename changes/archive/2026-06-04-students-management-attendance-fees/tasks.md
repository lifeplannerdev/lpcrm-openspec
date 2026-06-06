## 1. Backend Domain Foundation

- [x] 1.1 Create a dedicated fees domain with models for fee plans, fee accounts, installments, receipts, and adjustments.
- [x] 1.2 Add migrations, relations, and indexes for student-linked fee records and reporting queries.
- [x] 1.3 Extend student and attendance serializers/views so student detail responses can include attendance and fee summary data.
- [x] 1.4 Add audit log entries for fee changes and attendance mutations.
- [x] 1.5 Build an import/backfill path for the existing spreadsheet-based fee ledger and reconcile it into the new structured fee model.

## 2. Permissions and Authorization

- [x] 2.1 Add new permission strings and role templates for student, attendance, and finance access in the backend permission templates.
- [x] 2.2 Update backend permission checks so attendance and fees mutations require explicit permissions instead of broad role checks.
- [x] 2.3 Enforce trainer read-only access on fee endpoints and preserve accounting write access on all fee mutations.
- [x] 2.4 Update the permissions management API/UI payload contract so the new permissions can be saved and restored correctly.

## 3. Frontend Student, Attendance, and Fees UX

- [x] 3.1 Rework the students workspace to support a richer detail view with profile, attendance, and fees tabs in the CRM theme.
- [x] 3.2 Add fees management screens for accounting users with fee plans, balances, payment entry, and history views.
- [x] 3.3 Update the attendance screens so marking controls honor the new permission model and trainer scoping rules.
- [x] 3.4 Wire navigation, route guards, loading states, and empty states for the new or updated student-related screens.
- [x] 3.5 Add fee restructuring and partial-payment flows to the frontend so accounting can convert plans and record exceptional payments.

## 4. Validation and Rollout

- [x] 4.1 Add backend tests for student scoping, attendance authorization, fee read/write separation, and role template seeding.
- [x] 4.2 Add frontend verification for trainer, accounting, and admin flows to confirm the right controls appear in each role.
- [x] 4.3 Validate the migration path with sample data and confirm the new fee screens and permissions can be safely enabled in production.
- [x] 4.4 Run a final end-to-end verification of backend APIs, frontend screens, permissions, notifications, and audit trails after all tasks are complete.

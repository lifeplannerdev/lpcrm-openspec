## 1. Backend fee catalog and sync

- [x] 1.1 Add or extend backend APIs so fee templates can be fetched as a company-scoped dropdown catalog for enrollment and fee setup.
- [x] 1.2 Update fee account creation and restructure serializers so selecting a template auto-fills plan name, plan code, plan type, total due, registration amount, and due day.
- [x] 1.3 Persist a fee-template snapshot on each fee account so historical contracts remain stable after catalog edits.
- [x] 1.4 Add backend handling for pending fee setup, linked student fee state, and fee-aware enrollment status in academic views.
- [x] 1.5 Add or verify notification hooks for fee-plan assignment, restructure, overdue, and settlement events that affect trainers and accounting.

## 2. Frontend template-driven enrollment

- [x] 2.1 Replace manual fee-plan entry with a dropdown-driven template selector in the fee-account form.
- [x] 2.2 Auto-fill the fee-account form from the selected template and keep only controlled override fields editable for accounting users.
- [x] 2.3 Update the student detail and student-enrollment screens so linked fee state is visible in the academic CRM theme.
- [x] 2.4 Show the same fee summary on trainer-visible student screens in read-only mode.
- [x] 2.5 Add batch or program default template suggestions where available, while still requiring explicit selection when no default exists.

## 3. Validation and rollout

- [x] 3.1 Add backend tests for template catalog retrieval, template autofill, fee snapshot persistence, and enrollment/fee linkage.
- [x] 3.2 Add frontend verification for accounting, trainer, and admin flows to confirm dropdown templates and read-only fee visibility behave correctly.
- [x] 3.3 Verify sample data against the known fee structure from the workbook and image so the seeded templates match the real plan catalog.
- [x] 3.4 Run a final end-to-end review of backend APIs, frontend screens, notifications, and student/fee synchronization before release.

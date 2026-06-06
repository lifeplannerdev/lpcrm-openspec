## Context

The current CRM already has a partial student domain in `trainers` with students, attendance, academic batches, and exam results. The frontend also has student list/detail screens and attendance tooling, but fees are not a first-class domain and permission enforcement is still mostly role-driven or inconsistent across modules.

This change adds a more complete student operations layer while preserving the existing CRM visual language and the current monolith-style Django/React structure. The main new domain is fees, which needs stronger auditability and stricter access control than the rest of the student screens.

The workbook and fee image establish the real business rules we need to preserve:
- level-based pricing for `A1`, `A2`, `B1`, and `B2`
- package-level pricing for the full `A1-B2` course
- one-time, installment, and monthly payment routes
- seat booking / registration style upfront payments
- custom negotiated balances and manual ledger entries already used in the current Excel sheets

## Goals / Non-Goals

**Goals:**
- Deliver a robust student management workspace that feels native to the CRM.
- Add accounting-owned fees management with trainer read-only visibility.
- Support structured handling for one-time payment, installment, monthly, partial, and restructured fee scenarios.
- Make attendance and student screens permission-driven instead of relying on ad-hoc role checks.
- Reuse the existing CRM theme, navigation patterns, and data-fetching conventions.
- Keep the system maintainable by separating finance logic from academic tracking where that improves clarity.

**Non-Goals:**
- Rebuilding the whole CRM design system.
- Replacing the existing auth/session stack in this change.
- Introducing a separate microservice for fees.
- Building payroll, payroll deductions, or general accounting beyond student fee workflows.

## Decisions

- **Create a dedicated fees app instead of embedding fee logic into `trainers`.**  
  Fee collection has a different lifecycle from students and attendance: plans, installments, receipts, adjustments, refunds, and audit trails. Keeping that in a separate domain reduces coupling and makes future reporting easier.  
  **Alternative considered:** adding balance columns directly onto `Student`. That would be simpler short-term, but it breaks down as soon as partial payments, multiple receipts, or fee edits are required.

- **Model fees as a contract plus ledger, not as a single balance field.**  
  The spreadsheet currently mixes plans, dates, amounts, and balances in one manual table. The production model should split this into fee catalog definitions, student fee contracts, scheduled dues, and actual payments so the system can answer "what is due, what was promised, what was paid, and what changed?" cleanly.  
  **Alternative considered:** keeping a single editable balance per student. That would be fast to implement, but it would fail partial payments, restructuring, and audit requirements.

- **Keep students and attendance linked to the existing academic domain, but strengthen permission boundaries.**  
  The current `trainers` app already owns the student and attendance models, so the lowest-risk path is to extend it rather than split it apart. The important change is to move enforcement from broad role checks to explicit permissions and role templates.  
  **Alternative considered:** a full domain split into new academic and attendance services. That would be cleaner architecturally, but it is unnecessary for this iteration and would add migration risk.

- **Treat accounting as the owner of mutable fees data; trainers get read-only access.**  
  Trainers need visibility into student payment status without being able to alter it. The UI should show fee summaries to trainers, but all create/update actions must be locked behind finance permissions.  
  **Alternative considered:** hiding fees entirely from trainers. That would remove useful context from student management and make operations harder.

- **Represent fee plans as reusable templates with student-level overrides.**  
  The workbook shows both package pricing and custom negotiated rows. The cleanest approach is to maintain base plans such as one-time, 3-installment, and monthly packages, then allow per-student overrides and restructure actions when special cases occur.  
  **Alternative considered:** hard-coding each workbook row as a unique plan. That would mirror the spreadsheet, but it would make reporting and maintenance impossible.

- **Model payment exceptions explicitly.**  
  Partial installment payments, missed deadlines, plan conversions, and overdue balances should each have their own state or event, not just a free-text note.  
  **Alternative considered:** relying on comments and ad-hoc notes. That would not be reliable enough for accounting or attendance linkage.

- **Use permission strings as the source of truth for page access and mutations.**  
  Roles remain useful as templates, but the actual authorization should be permission-based so the system can support mixed responsibilities cleanly.  
  **Alternative considered:** continuing with role checks only. That would make the new fees flow too fragile, especially with existing role-name drift in the codebase.

- **Keep the CRM visual language consistent.**  
  Student, attendance, and fees pages should reuse the existing card, tab, table, gradient header, and rounded control patterns so the new work looks like part of the same product.

- **Connect fees to attendance through policy, not a hardcoded binary lock.**  
  The business likely needs students with overdue balances to be flagged, warned, or escalated rather than silently blocked. That policy should be configurable so the academic workflow stays usable in special cases.  
  **Alternative considered:** auto-blocking attendance when fees are overdue. That is too rigid for exceptions and special approvals.

- **Import the spreadsheet as a controlled migration input.**  
  The workbook is the operational source for current balances and plans, so the new model should support a guided import/backfill path and preserve the original plan history for audit.  
  **Alternative considered:** re-entering all records manually. That is too error-prone and would lose historical context.

## Risks / Trade-offs

- **[Risk]** Existing student pages may need route and permission updates in several places.  
  **Mitigation:** introduce shared permission constants and route guards before wiring new screens.

- **[Risk]** Fee balance logic can become inconsistent if it is stored only as a denormalized total.  
  **Mitigation:** store a ledger of fee plans, installments, payments, and adjustments, then derive summaries from that ledger.

- **[Risk]** Restructured plans may create ambiguity about the original contract and the new contract.  
  **Mitigation:** keep immutable plan snapshots and create a new contract version whenever a student changes plan.

- **[Risk]** Partial payments and negotiated balances can make overdue reporting more complex.  
  **Mitigation:** separate scheduled due amounts from paid amounts and compute aging from due dates plus outstanding residuals.

- **[Risk]** Trainers may accidentally gain edit paths if the UI hides controls but the backend still accepts requests.  
  **Mitigation:** enforce write permissions server-side for every fee and attendance mutation.

- **[Risk]** Spreadsheet import may introduce inconsistent legacy data.  
  **Mitigation:** validate imported records, flag anomalies for review, and keep an import report before activating the new fee ledger.

- **[Risk]** New fee models may need reporting and index tuning later.  
  **Mitigation:** add audit fields, branch/company scoping, and indexes on student, status, due date, and payment date from the start.

- **[Risk]** Changing permission templates may affect existing staff accounts.  
  **Mitigation:** ship a controlled migration that preserves explicit overrides while updating default templates for the new permissions.

## Migration Plan

1. Add the new fee domain models, serializers, APIs, and permission strings.
2. Update permission templates and the permissions management UI to expose the new student/attendance/fee permissions.
3. Add frontend routes and student detail tabs for attendance and fees.
4. Backfill any seed data or default permission presets for accounting and trainer roles.
5. Import or reconcile the existing spreadsheet-based fee records into the new structured fee ledger.
6. Verify trainer read-only access on fees and authorized write access for accounting.
7. Roll out behind existing auth and company scoping, then validate with a few real staff roles before broad production release.

Rollback should be straightforward because the change is additive: disable the new routes, remove the new permission assignments, and stop routing users to the new fee screens if any issue appears.

## Open Questions

- Should fee plans be attached directly to academic batches, to individual students, or both?
- Do we need receipt numbering that is global across the company or scoped by branch/company?
- Should accounting users be able to edit historical payments, or only add reversals/adjustments?
- Should trainers see only their own students' fee summaries, or all students they can already view?
- Which fee changes should trigger notifications to accounting, trainers, and management?

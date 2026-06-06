## Context

The CRM already has a fee domain, student records, attendance, and fee-account APIs. The remaining gap is the operational workflow: staff still need a template-first way to choose fee plans, and the current student/fee surfaces must stay aligned without requiring duplicate manual entry.

The existing backend already stores fee-plan templates and fee accounts, but the UX can still expose manual plan typing paths. That creates two risks: staff enter incorrect plan names or amounts, and the same fee plan can drift across student and accounting screens. The goal of this change is to make canonical fee templates the source of truth and ensure a student’s academic record and fee record stay synchronized as a single lifecycle.

Stakeholders:
- Accounting users who create and manage fee accounts
- Trainers who need read-only visibility into fee state for their students
- Admins who need to maintain the fee template catalog
- Operations users who need consistent student/fee status across screens

## Goals / Non-Goals

**Goals:**
- Make fee plan selection template-driven with dropdowns for the standard plans.
- Eliminate free-form plan naming and amount entry for normal fee setup.
- Auto-populate fee account fields from the selected template.
- Keep the student record, fee account, and related summary views synchronized.
- Preserve controlled overrides for restructuring, negotiated balances, and exceptional cases.
- Keep accounting as the owner of fee mutations and trainers as read-only viewers of fee state.

**Non-Goals:**
- Replacing the existing authentication or permissions model.
- Rebuilding the entire student workflow from scratch.
- Moving fee logic into a separate service.
- Removing support for custom restructures or exception handling.

## Decisions

- **Use fee templates as the canonical source of truth for normal plans.**  
  The fee image and workbook show a limited set of standard offerings, so the system should present those as dropdown options rather than requiring manual text entry.  
  **Alternative considered:** leaving fee setup as free-form fields. That is simpler in the UI, but it recreates the spreadsheet problem and makes reporting unreliable.

- **Keep a dedicated template catalog separate from per-student fee accounts.**  
  Templates define the standard plan shape; fee accounts represent the student-specific contract and ledger. This separation allows one template to be reused across many students while still supporting overrides.  
  **Alternative considered:** copying template fields directly onto each student record. That would make the form look simpler, but it would blur catalog data with live accounting data and make changes harder to audit.

- **Synchronize student enrollment and fee status through the backend, not the UI alone.**  
  The UI should reflect the same student lifecycle on both the academic side and the accounting side, but the backend must be the source of truth for linking fee accounts to student records.  
  **Alternative considered:** trusting the frontend to keep both views in sync. That would be fragile and would break as soon as another client or API consumer is introduced.

- **Keep accounting as the mutable owner of fees.**  
  Trainers should see fee state, but should not be able to create or mutate fee plans. This preserves a clean division between academic onboarding and financial control.  
  **Alternative considered:** letting trainers assign templates directly. That would speed up enrollment, but it increases the chance of incorrect financial setup and weakens controls.

- **Support controlled overrides instead of arbitrary edits.**  
  When a student needs a special arrangement, the user should start from a known template and then apply explicit overrides or restructures.  
  **Alternative considered:** allowing entirely custom plans for every case. That would make the UI flexible, but it would destroy consistency and reporting quality.

- **Seed the template catalog from the known fee structure.**  
  The current fee sheet provides the baseline plans, so the system should support bootstrap templates for the known package, installment, monthly, and level-based pricing.  
  **Alternative considered:** requiring manual creation of all templates in production. That would slow rollout and increase the risk of missing the standard plans.

## Risks / Trade-offs

- **[Risk]** Users may expect to edit template-derived fields freely after selection.  
  **Mitigation:** lock standard fields to the selected template by default and expose only approved override controls.

- **[Risk]** Template changes could affect downstream student fee accounts if the data model is not separated clearly.  
  **Mitigation:** snapshot the selected template on the account and keep the live catalog independent from historical account state.

- **[Risk]** Dual views for trainers and accounting can drift if one side caches stale data.  
  **Mitigation:** re-fetch fee summaries from the backend after account creation, restructure, or payment events.

- **[Risk]** Custom exceptions may become a back door to uncontrolled fee editing.  
  **Mitigation:** require explicit accounting permissions and audit logging for any override or restructure path.

- **[Risk]** Existing staff may continue using the manual workflow out of habit.  
  **Mitigation:** make the dropdown-first path the default and progressively reduce the visibility of free-form plan entry.

## Migration Plan

1. Expose or reuse a fee-template catalog endpoint for the dropdown source.
2. Update the fee-account creation form to select a template first and auto-fill plan details.
3. Keep a custom path available for exceptional cases, but make it secondary to the template flow.
4. Refresh student detail and accounting views so the same fee state appears in both places.
5. Seed the standard templates from the known fee structure and verify that the plan list matches the operational fee sheet.
6. Validate trainer read-only access and accounting write access after the UI and backend wiring is complete.
7. Roll out behind existing permissions and confirm that student enrollment changes appear in fee views and vice versa.

Rollback should disable the template-first enforcement and restore the prior form behavior while preserving the underlying fee-account data.

## Open Questions

- Should the dropdown show only active templates for the user’s company, or should admins be able to see inactive historical templates too?
- Should student enrollment create a pending fee account automatically, or should accounting still explicitly create the fee account after enrollment?
- Should template overrides be captured as a new account version or as a separate restructure event?
- Should the dropdown defaults differ by branch, company, or academic batch?

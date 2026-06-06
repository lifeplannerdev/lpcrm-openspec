## Why

The current fee-account workflow still leaves too much room for manual plan entry, which makes onboarding slow, inconsistent, and error-prone when staff do not know the correct plan names or amounts. We need a template-driven fee setup so accounting can choose a known plan from a dropdown, while the student record, fee account, and related screens stay synchronized automatically.

## What Changes

- Convert fee plan selection into a template-first workflow with dropdowns for canonical plans such as one-time, installment, monthly, and level-based packages.
- Remove the expectation that staff manually type plan names, codes, or pricing for standard fee setup.
- Auto-fill fee account fields from the selected template, while still allowing controlled custom overrides for exceptional cases.
- Keep student enrollment and fee account state linked so changes made in one place appear consistently in the other.
- Preserve special-case handling for restructures, partial payments, and negotiated balances without falling back to free-form fee definitions.
- Keep trainers on read-only fee visibility while accounting retains ownership of fee-plan creation and mutation.

## Capabilities

### New Capabilities
- `fee-plan-catalog`: Managed fee plan templates, dropdown selection, and template-driven autofill for student fee setup.
- `student-fee-enrollment-sync`: Student enrollment and fee-account state synchronization so academic and finance screens reflect the same student lifecycle.

### Modified Capabilities
- `academic-management`: Academic enrollment status and fee linkage must remain aligned so the student lifecycle reflects the active fee plan.

## Impact

- Frontend fee-account and student-enrollment forms, including dropdown selection, autofill behavior, and validation.
- Backend fee-plan template APIs, fee-account creation, and restructure flows.
- Student detail and accounting views that need to reflect the same plan state from different permissions.
- Existing fee catalog seed data and any import/migration logic for legacy workbook plans.
- Permission-aware UI behavior so accounting can edit plans while trainers see the linked state read-only.

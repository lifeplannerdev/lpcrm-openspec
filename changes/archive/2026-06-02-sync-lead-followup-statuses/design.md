## Context

Currently, updating a `FollowUp` record to "Contacted" or "Not Interested" in the CRM does not affect the associated `Lead`. The parent lead remains in its original status (often "Enquiry"). However, the frontend components (like the Customer Journey stepper) expect the lead's main status to reflect progress. This disconnect causes confusion and requires manual double-entry.

## Goals / Non-Goals

**Goals:**
- Automatically sync Follow-Up status updates up to the parent Lead.
- Add "CONTACTED" as an official Lead status option in the backend to match the frontend expectations.
- Ensure all frontend elements (Customer Journey, Lead Detail Badges) accurately and gracefully handle the "CONTACTED" state.

**Non-Goals:**
- Complete restructuring of the CRM lead flow beyond ensuring FollowUp parity.
- Re-architecting how Customer Journeys are evaluated (we will fix the data parity, not rewrite the React component structure).

## Decisions

1. **Adding CONTACTED to Lead.STATUS_CHOICES**
   - **Rationale**: The frontend `getStatusColor` mapping already references "CONTACTED". By adding it to the backend `STATUS_CHOICES`, we gain exact parity and eliminate hardcoded string discrepancies.

2. **Signal-based Status Sync**
   - **Rationale**: Hooking into Django's `post_save` signal on the `FollowUp` model guarantees that whenever a FollowUp's status is saved as `contacted`, the parent Lead will automatically be bumped to `CONTACTED`. This approach works universally across the system (API, admin panel, management commands) rather than just in specific views.

## Risks / Trade-offs

- **[Risk]** Unintended downgrades: A user marks a FollowUp as "contacted" (upgrading the lead), but later reverts the FollowUp to "pending" by mistake.
  - **Mitigation**: We will only automatically upgrade the Lead status in a forward direction (e.g. from `ENQUIRY` to `CONTACTED`). We will not automatically downgrade statuses. Any regression of Lead status should be a deliberate manual action by the user.

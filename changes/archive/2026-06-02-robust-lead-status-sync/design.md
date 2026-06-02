## Context
We currently automatically sync `FollowUp` status changes up to the parent `Lead`. However, if a user deletes a follow-up or changes its status *back* to pending, the Lead stays stuck in the advanced state (`CONTACTED` or `NOT_INTERESTED`). We need to recalculate the lead status accurately when follow-ups are altered or deleted.

## Goals / Non-Goals

**Goals:**
- Recalculate a Lead's status when a FollowUp is modified or deleted.
- Revert a Lead's status to `ENQUIRY` if there are no remaining FollowUps that justify the `CONTACTED` or `NOT_INTERESTED` status.
- Safely handle regressions without downgrading leads that have manually been advanced to states like `QUALIFIED` or `CONVERTED`.

**Non-Goals:**
- Rebuilding the entire Lead status state machine.
- Propagating regressions between advanced states (e.g., we won't regress from `QUALIFIED` to `CONTACTED`). We only handle the base `ENQUIRY` -> `CONTACTED` -> `ENQUIRY` flow.

## Decisions

1. **Helper Function for Recalculation**
   - **Rationale**: We will extract the logic into a `recalculate_lead_status(lead)` helper to be called from both `post_save` and `post_delete` signal receivers on the `FollowUp` model. This centralizes the logic and avoids duplication.

2. **Selective Regression Checks**
   - **Rationale**: The recalculation function will first check if `lead.status` is strictly in `['ENQUIRY', 'CONTACTED', 'NOT_INTERESTED']`. If the Lead is in `QUALIFIED` or higher, the function immediately returns without downgrading. This prevents destructive state overwrites. 

3. **Aggregate Querying**
   - **Rationale**: If the lead is eligible for recalculation, it will query the Lead's follow-ups to see if any `contacted` or `not_interested` follow-ups exist, and adjust the Lead status accordingly.

## Risks / Trade-offs

- **[Risk]** Extra database queries on every FollowUp save/delete.
  - **Mitigation**: The query is lightweight and only occurs on saving/deleting FollowUps, which is a relatively infrequent write operation per lead. The data integrity benefits far outweigh the minor performance cost.

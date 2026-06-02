
## 1. Helper Implementation

- [x] 1.1 Create `recalculate_lead_status(lead)` helper function in `leads/signals.py`
- [x] 1.2 Implement guard clauses inside the helper to exit early if `lead.status` is an advanced state (e.g. `QUALIFIED`, `CONVERTED`, `REGISTERED`)
- [x] 1.3 Query `lead.followups.all()` inside the helper to check for any existing `contacted` or `not_interested` follow-ups and update the `lead.status` appropriately (or revert to `ENQUIRY` if none exist)

## 2. Signal Integration

- [x] 2.1 Refactor the existing `sync_lead_status_from_followup` `post_save` receiver to call the new helper function instead of manual one-way sync logic
- [x] 2.2 Add a new `post_delete` receiver for `FollowUp` (or hook into the existing one) that also calls `recalculate_lead_status(instance.lead)`

## 3. Verification

- [x] 3.1 Verify creating a `contacted` FollowUp promotes an `ENQUIRY` Lead to `CONTACTED`
- [x] 3.2 Verify changing that FollowUp back to `pending` reverts the Lead to `ENQUIRY`
- [x] 3.3 Verify deleting the FollowUp entirely reverts the Lead to `ENQUIRY`
- [x] 3.4 Verify that if a Lead is manually set to `QUALIFIED`, altering or deleting its FollowUps does not degrade its status

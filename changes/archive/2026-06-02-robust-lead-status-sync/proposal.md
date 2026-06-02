## Why
We recently introduced automated syncing that promotes a Lead's status to `CONTACTED` or `NOT_INTERESTED` when a FollowUp is marked as such. However, this creates a one-way street: if that FollowUp is later deleted (or its status reverted), the Lead remains stuck in the advanced state indefinitely. We need a robust recalculation approach to ensure backward synchronization (reverting Lead statuses) without accidentally downgrading leads that have already moved further down the funnel.

## What Changes
- Refactor the automated sync logic to recalculate the Lead's status by examining all of its FollowUps.
- Run this recalculation logic on both `post_save` and `post_delete` of FollowUps.
- Only downgrade a Lead's status back to `ENQUIRY` if its current status is exactly `CONTACTED` or `NOT_INTERESTED` AND there are no longer any valid FollowUps proving contact.
- Do not downgrade Leads that have progressed to `QUALIFIED`, `CONVERTED`, or `REGISTERED`.

## Capabilities

### Modified Capabilities
- `status-synchronization`: Adding robust recalculation and regression handling when FollowUps are deleted or reverted.

## Impact
- **Backend**: `leads/signals.py` - will introduce a new `recalculate_lead_status` helper function.
- **Data Integrity**: Ensures that the `Lead.status` perfectly reflects the aggregate state of its `FollowUp`s without manual intervention, handling edge cases gracefully.

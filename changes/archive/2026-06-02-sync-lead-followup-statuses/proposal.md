## Why

When follow-up calls are completed and their status updated to "Contacted", the parent Lead's status remains "Enquiry". This creates a synchronization gap between the backend data and the frontend components (like the Customer Journey stepper), which rely on the Lead's main status. This change ensures that follow-up activities correctly sync back to the parent lead, keeping the frontend UI and backend data consistent.

## What Changes

- Add `CONTACTED` as an officially supported status in the backend `Lead.STATUS_CHOICES` to match frontend expectations.
- Automate Lead status transitions: When a `FollowUp` is marked as `contacted`, automatically update the parent `Lead` status from `ENQUIRY` to `CONTACTED`.
- Ensure frontend components (like the Customer Journey stepper) accurately reflect the "Contacted" state based on these synchronized statuses.
- Validate that no other components are broken or disconnected as a result of unifying these status codes.

## Capabilities

### New Capabilities

- `status-synchronization`: Automatically sync state changes between FollowUps and Leads.

### Modified Capabilities
- `lead-management`: Updates to Lead status definitions and transitions.

## Impact

- **Backend**: `leads/models.py` (STATUS_CHOICES), `leads/signals.py` (automation logic).
- **Frontend**: Minor verification in `CustomerJourney.jsx` and `LeadDetailPage.jsx` to ensure it renders correctly with the newly synced backend states.

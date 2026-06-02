## 1. Backend Modifications

- [x] 1.1 Add 'CONTACTED' to `STATUS_CHOICES` in `leads/models.py`
- [x] 1.2 Generate Django migrations for the new `STATUS_CHOICES`
- [x] 1.3 Add a new `post_save` or `pre_save` signal for `FollowUp` in `leads/signals.py` to automatically update parent `Lead` status from `ENQUIRY` to `CONTACTED` when follow-up status is marked as `contacted`
- [x] 1.4 Add signal logic to automatically update parent `Lead` status from `ENQUIRY` to `NOT_INTERESTED` when follow-up status is marked as `not_interested`

## 2. Frontend Verifications

- [x] 2.1 Verify `getStatusColor` correctly maps `CONTACTED` and handles color rendering in `src/Pages/LeadDetailPage.jsx`
- [x] 2.2 Verify `src/Components/leads/CustomerJourney.jsx` accurately reflects the "Contacted" milestone when `lead.status` is `CONTACTED`
- [x] 2.3 Test the full flow: Add a follow-up, mark as contacted, and verify the UI immediately updates without page reload (or after standard re-fetch)

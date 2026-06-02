## 1. Backend Core (Models & Timeline)

- [x] 1.1 Add `LeadDocument` model to `leads/models.py` for file attachments.
- [x] 1.2 Generate and run makemigrations for `LeadDocument`.
- [x] 1.3 Create `UnifiedTimelineAPIView` in `leads/views/leads.py` merging remarks, updates, follow-ups, and webhook logs.
- [x] 1.4 Add URL route for `UnifiedTimelineAPIView` in `leads/urls.py`.

## 2. Backend Enhancements (Escalations & Mentions)

- [x] 2.1 Implement Django pre_save signal in `leads/signals.py` to parse `@username` in `RemarkHistory` and create Notifications.
- [x] 2.2 Create `escalate_followups.py` Django management command in `leads/management/commands/`.
- [x] 2.3 Implement the 24h notification logic in `escalate_followups.py`.
- [x] 2.4 Implement the 72h reassignment logic in `escalate_followups.py`.

## 3. Frontend Architecture (Command Center)

- [x] 3.1 Refactor `LeadDetailPage.jsx` layout to accommodate Customer Journey and Timeline side-by-side.
- [x] 3.2 Build the `CustomerJourney.jsx` component mapping creation, assignment, and conversion states.
- [x] 3.3 Update `UnifiedTimeline.jsx` to consume the new `UnifiedTimelineAPIView`.
- [x] 3.4 Integrate `react-big-calendar` (or similar) into `AllFollowUpsPage.jsx`.

## 4. Frontend Enhancements (Collaboration & Cleanup)

- [x] 4.1 Add file upload drag-and-drop zone to `LeadDetailPage.jsx` calling the `LeadDocument` API.
- [x] 4.2 Update Remark input field to support `@username` autocomplete dropdown.
- [x] 4.3 Remove deprecated legacy components from `src/Components/leads/` and clean up unused imports.

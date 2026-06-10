## Why

The current `LeadsPage` requires full page navigation to view lead details, causing context loss and slowing down user workflows. Additionally, the Unified Timeline is read-only, forcing users to navigate away just to add a quick note or schedule a follow-up. This change introduces a Split-Pane Master-Detail View and Inline Timeline Actions to significantly enhance the speed, responsiveness, and usability of lead management.

## What Changes

- Add a split-pane layout to `LeadsPage.jsx` using flexbox, triggered by a selected lead ID in the URL.
- Implement a new `LeadSidePanel.jsx` component that displays condensed lead info, the timeline, and assignments via mini-tabs.
- Update `UnifiedTimeline.jsx` to include an interactive inline form for adding remarks and scheduling follow-ups.
- Implement nested routing (`/leads` and `/leads/:leadId`) for robust state management and deep linking.
- Implement a responsive full-screen slide-over drawer for mobile devices to maintain UX on small screens.

## Capabilities

### New Capabilities
None. This change improves the UI for existing capabilities.

### Modified Capabilities
- `lead-management`: Adding nested routing requirement for split-pane UI and full-screen mobile drawer overlay.

## Impact

- **Affected Code**: `LeadsPage.jsx`, `LeadsTable.jsx`, `LeadsKanbanBoard.jsx`, `UnifiedTimeline.jsx`, `App.jsx` (routing).
- **New Code**: `LeadSidePanel.jsx`.
- **UX**: Desktop users will experience a fast split-pane layout; Mobile users will experience a slide-over drawer.

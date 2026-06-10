## 1. Routing and Infrastructure Setup

- [x] 1.1 Update `App.jsx` routing to support nested routes for `/leads` and `/leads/:leadId` using `LeadsPage`.

## 2. LeadSidePanel Component Creation

- [x] 2.1 Scaffold `LeadSidePanel.jsx` component inside `src/Components/leads/`.
- [x] 2.2 Implement data fetching inside `LeadSidePanel` using the `leadId` parameter from the URL.
- [x] 2.3 Build the sticky header UI (Avatar, Name, Status, Priority, Quick Call/Email actions, Close button).
- [x] 2.4 Implement Mini-Tabs state management (Info, Timeline, Assignment).
- [x] 2.5 Build the "Info" tab UI with condensed contact and lead details.
- [x] 2.6 Build the "Assignment" tab UI to display current, primary, and sub-assignments.

## 3. Split-Pane Layout & Mobile Drawer

- [x] 3.1 Update `LeadsPage.jsx` to read `leadId` via `useParams()`.
- [x] 3.2 Refactor `LeadsPage.jsx` main content area into a flex container with conditional width classes (`w-full` vs `w-[calc(100%-400px)]`).
- [x] 3.3 Add CSS transitions for smooth table compression when the side panel is active.
- [x] 3.4 Integrate `LeadSidePanel` into the `LeadsPage.jsx` flex layout on desktop.
- [x] 3.5 Add responsive classes (`fixed`, `inset-0`, `z-50`) to `LeadSidePanel` to render as a slide-over drawer on screens `< 1024px`.
- [x] 3.6 Implement the backdrop overlay (`bg-black/50`) for the mobile drawer.
- [x] 3.7 Ensure the 'X' button and backdrop click call `navigate('/leads')` to close the panel.

## 4. Unified Timeline Upgrades (Inline Actions)

- [x] 4.1 Update `UnifiedTimeline.jsx` to render inside `LeadSidePanel`'s Timeline tab.
- [x] 4.2 Add action toggle buttons ("Add Remark", "Schedule Follow-up") below the sticky header.
- [x] 4.3 Implement the "Add Remark" form (textarea, submit button) and connect to the POST endpoint.
- [x] 4.4 Implement the "Schedule Follow-up" form (datetime picker, dropdowns) and connect to the POST endpoint.
- [x] 4.5 Implement optimistic UI updates so submitted remarks/follow-ups immediately prepend to the `events` timeline list.

## 5. UI Consistency and Bug Fixes

- [x] 5.1 Update `LeadsTable.jsx` row click handler to `navigate('/leads/${lead.id}')`.
- [x] 5.2 Update `LeadsKanbanBoard.jsx` card click handler to `navigate('/leads/${lead.id}')`.
- [x] 5.3 Verify that sorting, filtering, and pagination in `LeadsPage` still work correctly when the split-pane is open.
- [x] 5.4 Test mobile drawer behavior and scroll-locking.

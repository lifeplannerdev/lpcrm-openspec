## Context

The current `LeadsPage` uses a traditional list-detail pattern where users must navigate away from the list to view lead details (`LeadDetailPage`). This breaks flow and context. The `UnifiedTimeline` on the details page is currently read-only, forcing users to navigate to separate tabs to add a note or follow-up. 

## Goals / Non-Goals

**Goals:**
- Implement a Split-Pane layout on desktop allowing users to view lead details without leaving the Leads list.
- Implement a full-screen drawer for the same functionality on mobile devices.
- Make the `UnifiedTimeline` interactive with inline forms for remarks and follow-ups.
- Ensure deep-linking works (e.g., sharing a URL opens the specific lead's side panel).

**Non-Goals:**
- We are not replacing `LeadDetailPage` entirely. It will remain accessible for full, deep editing and complex history views.
- We are not changing the backend API for leads, remarks, or follow-ups.

## Decisions

**1. Routing Strategy: Nested Routes vs Query Params**
*Decision*: Use React Router nested routes (`/leads` and `/leads/:leadId`).
*Rationale*: Nested routes are cleaner, handle browser history (back button) better, and provide a more app-like feel on mobile when the drawer opens and closes. `LeadsPage` will use `useParams()` to check if a `leadId` is present and mount the side panel accordingly.

**2. Desktop Layout Strategy: Flexbox Compression**
*Decision*: Use a flex container for the main layout. When a `leadId` is present, the table will compress (e.g., `w-[calc(100%-400px)]`) and the `LeadSidePanel` will render in the remaining 400px.
*Rationale*: This prevents modal-fatigue and allows users to keep scrolling the list while viewing details. CSS transitions will be used for smooth sliding.

**3. Mobile Strategy: Fixed Slide-Over Drawer**
*Decision*: On `< 1024px` screens, the `LeadSidePanel` switches to `position: fixed` with an overlay.
*Rationale*: A split pane is impossible on mobile. An overlay drawer ensures the list scroll position is preserved underneath.

**4. Side Panel Content: Mini-Tabs**
*Decision*: The side panel will have a sticky header (with quick call/email actions) and mini-tabs (Info, Timeline, Assignment).
*Rationale*: The full detail page has too much information to cram into 400px. Mini-tabs keep the side panel organized and focused on quick actions.

**5. Timeline Inline Actions**
*Decision*: Add a small tabbed form (Remark / Follow-up) directly below the sticky header of `UnifiedTimeline.jsx`.
*Rationale*: Places the action exactly where the user is looking. We will use optimistic UI updates so the timeline feels instantaneous after submission.

## Risks / Trade-offs

- **Risk**: The Leads Table might feel cramped when compressed to `w-2/3`.
  **Mitigation**: Use `overflow-x-auto` on the table wrapper and ensure columns shrink gracefully or become scrollable horizontally.
- **Risk**: API calls from the Side Panel might feel slow.
  **Mitigation**: Add skeleton loaders to `LeadSidePanel` while it fetches the specific lead's data. Wait, we could pass data from the list, but fetching is safer to ensure fresh data and proper `LeadDetailPage` parity.

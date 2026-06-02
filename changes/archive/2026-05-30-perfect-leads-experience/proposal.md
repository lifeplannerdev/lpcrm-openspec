## Why

The current Leads Management System has a solid foundational architecture with good permissions, assignment rules, and basic UI structure. However, it lacks a premium "wow factor" and optimal scalability as data grows. We need to perfect the UI with a split-pane Command Center, Drag-and-Drop Kanban pipelines, a Unified Timeline, and highly optimized backend processing (specifically bulk uploads) to ensure the system is lightning-fast, highly scalable, and a joy to use for the sales and operations teams.

## What Changes

- Redesign the Leads list and detail views into a unified "Command Center" with a side-panel for rapid lead preview and actioning.
- Implement a Drag-and-Drop Kanban view for visual lead pipeline management.
- Consolidate the "Follow-Ups", "Assignment", and "History" tabs into a beautifully designed vertical Story Timeline with micro-interactions.
- Replace native select elements with searchable comboboxes and upgrade form designs with glassmorphism and floating labels.
- Introduce automated follow-up cascading prompts upon lead reassignment.
- Enforce strict visual flags for leads in ENQUIRY/CONTACTED states missing scheduled next actions.
- Refactor the monolithic `leads/views.py` into modular, domain-specific files (`views/leads.py`, `views/assignments.py`, `views/followups.py`, `views/uploads.py`).
- Optimize the `BulkLeadUploadView` using `bulk_create` and O(1) in-memory duplicate checks to handle massive Excel uploads without timeouts.
- Add composite database indexing on `models.py` (e.g., `['assigned_to', 'status']`) for large-scale query optimization.
- **NOTE:** The previously explored Pusher Follow-up reminders are explicitly excluded from this scope.

## Capabilities

### New Capabilities
- `leads-command-center`: The split-pane master-detail view for rapid lead interaction.
- `leads-kanban-board`: Drag-and-drop visual pipeline for leads.
- `leads-unified-timeline`: A consolidated history, assignment, and follow-up view.
- `smart-followup-rules`: Automated cascading and missing-action flags for follow-ups.

### Modified Capabilities
- `leads-bulk-upload`: Changing the underlying implementation to use bulk database operations for scale (though this is mostly implementation, it changes the performance contract).

## Impact

- **Frontend:** Major updates to `LeadsPage.jsx`, `LeadDetailPage.jsx`, `LeadFollowUps.jsx`. Addition of new Kanban and Command Center components.
- **Backend:** Splitting `leads/views.py` into multiple files. Updates to `leads/models.py` for new composite indexes.
- **Dependencies:** May require new frontend UI libraries for Comboboxes (e.g., Headless UI or Radix) and Drag-and-Drop (e.g., dnd-kit or react-beautiful-dnd).

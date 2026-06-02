## 1. Backend Architecture & Optimization

- [x] 1.1 Create `views/` directory inside `leads/` app and add `__init__.py`
- [x] 1.2 Refactor `LeadListView`, `LeadCreateView`, `LeadDetailView` into `views/leads.py`
- [x] 1.3 Refactor assignment views into `views/assignments.py`
- [x] 1.4 Refactor follow-up views into `views/followups.py`
- [x] 1.5 Refactor `BulkLeadUploadView` into `views/uploads.py`
- [x] 1.6 Update `BulkLeadUploadView` to use `bulk_create` for insertions
- [x] 1.7 Add in-memory O(1) duplicate checking to `BulkLeadUploadView`
- [x] 1.8 Add composite index `models.Index(fields=['assigned_to', 'status'])` to `Lead` model

## 2. Frontend Infrastructure & Libraries

- [x] 2.1 Install `dnd-kit` (or similar) for Kanban drag-and-drop
- [x] 2.2 Install Headless UI or Radix primitives for comboboxes
- [x] 2.3 Create reusable `Combobox` component for robust searchable selects

## 3. Leads UI Components

- [x] 3.1 Create `LeadsCommandCenter.jsx` component for the split-pane layout
- [x] 3.2 Create `LeadsKanbanBoard.jsx` component and integrate drag-and-drop
- [x] 3.3 Create `UnifiedTimeline.jsx` combining follow-ups, processing, and history
- [x] 3.4 Update `LeadsFilters.jsx` to use the new `Combobox` component

## 4. Smart Rules & Integrations

- [x] 4.1 Implement missing action warnings for leads without scheduled follow-ups
- [x] 4.2 Add assignment cascading prompt to `LeadAssignView` flow on frontend
- [x] 4.3 Ensure `LeadsPage.jsx` can toggle between Command Center list and Kanban view

## 5. Testing & Cleanup

- [x] 5.1 Test bulk upload with 1000+ rows to verify timeout elimination
- [x] 5.2 Verify all drag-and-drop state updates correctly sync with backend
- [x] 5.3 Test unified timeline rendering and inline actions

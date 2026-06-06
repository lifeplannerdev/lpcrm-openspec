## Context

Currently, the system provides several API endpoints for managing fees, including `/api/fees/catalog/` which supports GET and POST operations to list and create fee plan templates (`FeePlanTemplate`). The frontend (`FeesManagementPage.jsx`) only has the capability to fetch and display the existing templates in a dropdown to select from when creating a student fee account. The user has provided fee structures (like "FLAG German Language Course" and "LEVEL BASED FEES") that they wish to add as templates easily from the dashboard.

## Goals / Non-Goals

**Goals:**
- Provide a simple UI in the frontend for administrators to create custom fee plan templates.
- Support various plan types (ONE_TIME, INSTALLMENT, MONTHLY, CUSTOM, PACKAGE) and their required fields.
- Integrate smoothly with the existing `POST /api/fees/catalog/` endpoint.

**Non-Goals:**
- We are not modifying the backend models or endpoints.
- We are not building a full comprehensive edit/delete management suite for templates in this change, just creation to unblock data entry.

## Decisions

- **UI Placement**: A "Create Template" button will be added near the "Create Fee Account" section or as a separate tab/modal in `FeesManagementPage.jsx`. We'll use a modal dialog to keep the main page clean.
- **Form Fields**: The form will include dynamic fields based on the selected `plan_type`. For example, if `plan_type` is MONTHLY, it will show fields for `duration_months` and `monthly_amount`.
- **State Management**: Upon successful creation, the frontend will automatically re-fetch the templates so the new one appears in the dropdown immediately.

## Risks / Trade-offs

- **Risk**: Creating templates requires `manage_fees` permissions on the backend.
  **Mitigation**: The "Create Template" button will only be rendered if the user has `canManageFees` permissions.

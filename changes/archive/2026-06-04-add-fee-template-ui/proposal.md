## Why

Currently, there is no user interface in the React frontend to create custom fee plan templates. Administrators and finance managers need a way to easily add new templates (like the FLAG German Language Course packages) directly from the dashboard without needing to use API clients or direct database access.

## What Changes

- Add a "Create Template" button and modal/form to the fee management or fee catalog area in the frontend.
- Allow users to input template details: `company`, `plan_type` (e.g. ONE_TIME, INSTALLMENT, MONTHLY, CUSTOM, PACKAGE), `name`, `code`, `course_label`, `total_amount`, and other plan-specific fields (like `registration_amount`, `monthly_amount`, `installment_count`, `duration_months`, `due_day`, `notes`).
- Submit this data to the existing `POST /api/fees/catalog/` backend endpoint to create the template.
- Refresh the template dropdown list after successful creation.

## Capabilities

### New Capabilities
- `fee-template-management`: The ability for authorized users to create and manage fee plan templates via the frontend UI.

### Modified Capabilities
None.

## Impact

- **Frontend:** Adds a new modal component or page in the React frontend (`lpcrm-frontend-main`). Modifies the fee management section to include this UI and interact with the `/api/fees/catalog/` endpoint.
- **Backend:** None, the API endpoint already exists.

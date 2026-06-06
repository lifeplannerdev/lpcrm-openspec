## ADDED Requirements

### Requirement: Authorized users can create fee plan templates
The frontend SHALL provide a user interface to create new fee plan templates by submitting data to the `/api/fees/catalog/` endpoint.

#### Scenario: Successful creation of a new fee template
- **WHEN** an authorized user opens the "Create Template" modal, fills in the required fields (e.g., code, name, plan_type, total_amount), and submits
- **THEN** a POST request is made to `/api/fees/catalog/`
- **THEN** the template is created in the backend
- **THEN** the frontend refreshes the template list and closes the modal

#### Scenario: Dynamic fields based on plan type
- **WHEN** the user selects `MONTHLY` as the plan type
- **THEN** the form SHALL reveal additional inputs for `registration_amount`, `monthly_amount`, `duration_months`, and `due_day`
- **WHEN** the user selects `INSTALLMENT` as the plan type
- **THEN** the form SHALL reveal additional inputs for `installment_count` and `installment_amount`

#### Scenario: Restricting access to template creation
- **WHEN** a user without the `manage_fees` permission views the Fees Management page
- **THEN** the "Create Template" button SHALL NOT be visible to them

## ADDED Requirements

### Requirement: Multi-Parameter Report Filtering
The system SHALL support filtering reports simultaneously by Employee, Date, Status, and Search Keyword on the backend list APIs.

#### Scenario: Aggregating End-of-Day HR Reports
- **WHEN** an HR user selects "Today" for date, a specific "Employee" from the dropdown, and searches for a specific string
- **THEN** the backend accurately returns the intersection (AND) of all those applied filters, fetching only that employee's reports submitted today that match the keyword.

### Requirement: Employee Filtering Dropdown
The frontend Reports pages SHALL display an Employee filter dropdown populated with active employees.

#### Scenario: Select an Employee
- **WHEN** the user selects an employee from the dropdown
- **THEN** the frontend triggers a network request to the backend appending `employee_id=<id>` to the query parameters.

### Requirement: Correct Currency Symbol for Penalties
The system SHALL use the Indian Rupee symbol (₹) instead of the Dollar sign ($) for penalty amounts.

#### Scenario: Viewing a Penalty
- **WHEN** the user views the Penalty Management page
- **THEN** they see the amounts prefixed or labeled with `₹` rather than `$`.

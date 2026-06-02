## ADDED Requirements

### Requirement: Staff Record Company Assignment
The Staff management system SHALL allow assigning staff to a specific company and respect the per-page company switcher.

#### Scenario: Admin with dual access adds staff
- **WHEN** user with both `access_lp` and `access_flag` opens the Add Staff modal
- **THEN** a dropdown field for "Company" (`LP` or `FLAG`) is displayed and required

#### Scenario: User with single access adds staff
- **WHEN** user with only `access_lp` opens the Add Staff modal
- **THEN** the "Company" field is hidden and silently defaults to `LP` upon submission

#### Scenario: Viewing Staff Grid
- **WHEN** viewing the Staff page
- **THEN** the grid only shows staff members belonging to the company selected in the page's Company Switcher

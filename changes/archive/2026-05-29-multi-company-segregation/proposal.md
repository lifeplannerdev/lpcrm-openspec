## Why

The CRM needs to securely segregate data between two distinct companies ("LP" and "FLAG") operating within the same system. While most employees are strictly assigned to one company, high-level executives (like the MD, CEO, and HR) require the ability to access and manage data for both companies. The solution must provide a seamless, per-page context switching mechanism so executives can view LP data on one page and FLAG data on another without global state conflicts.

## What Changes

- Add a `company` field (choices: `LP`, `FLAG`, default: `LP`) to all core data models including Tasks, Staff/Users, Leads, Penalties, Candidates, Students, Reports, Attendance, and Activities.
- Introduce an `access_flag` permission into the existing granular permissions JSON system.
- Enforce backend API security: Users can inherently only query data matching their own `company`. Users with the `access_flag` permission can query FLAG data even if they belong to LP.
- Implement a reusable "Company Switcher" tab component in the React frontend that sits at the top of individual pages (e.g., Tasks Page, Staff Page), visible only to users with the `access_flag` permission.
- Update creation/edit forms (e.g., Add Staff, Add Task) to include a company dropdown for users with dual access; for single-company users, silently assign records to their permitted company.

## Capabilities

### New Capabilities
- `multi-tenant-company-segregation`: Defines the architecture and rules for separating LP and FLAG data across the system, including API filtering and per-page context switching.

### Modified Capabilities
- `granular-permissions-engine`: Add `access_flag` to the permission list and update default role templates to assign this to executives.
- `staff-management`: Update staff creation/edit forms and grids to respect and display the `company` field.
- `task-kanban`: Update task assignment and viewing to respect company segregation.

## Impact

- **Database**: Schema migrations required to add the `company` column across multiple apps (accounts, tasks, leads, etc.).
- **Backend API**: ViewSets must override `get_queryset` to filter by company and validate permissions.
- **Frontend UI**: Page components must integrate the new local company switcher state, passing it to `fetch` calls.
- **Data Migration**: Existing records will need to be safely migrated and defaulted to `LP` or `FLAG` as appropriate.

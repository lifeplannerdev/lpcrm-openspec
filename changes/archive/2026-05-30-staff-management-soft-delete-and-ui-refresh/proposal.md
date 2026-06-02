## Why

Data preservation is critical for CRM integrity. Currently, staff members can be hard-deleted, which causes cascading data loss or broken foreign keys in related records (like leads assigned to them or activity logs). To protect data integrity, we must replace hard deletion with a "soft delete" (inactivation) mechanism. Concurrently, the staff management UI needs a premium refresh to provide a clean, highly optimized, and "wow factor" experience, ensuring that all filters, metrics, and granular permission controls work flawlessly.

## What Changes

- **BREAKING**: Remove hard deletion functionality for staff members entirely from both frontend UI and backend APIs.
- Introduce an "Active/Inactive" toggle for staff members.
- Inactive staff members will not be able to log in, but their historical data and associations will remain intact.
- Premium UI refresh of the Staff Management dashboard, featuring better metric cards, streamlined filtering, and a modern layout.
- Premium UI refresh of the "Edit Staff Member" page and "Manage Granular Permissions" modal to make it clean, structured, and visually stunning.
- Optimize the backend query for fetching staff lists to handle pagination and filtering efficiently.

## Capabilities

### New Capabilities
- None

### Modified Capabilities
- `staff-management`: Update requirements to explicitly forbid hard deletion, introduce inactive status, and mandate new premium UI standards for the staff management and permissions interfaces.
- `user-auth`: Update requirements to ensure inactive staff members cannot authenticate.

## Impact

- **Backend (`accounts` app)**: User deletion endpoints will be removed or restricted. User listing API must support filtering by `is_active` status. Authentication mechanisms must block inactive users.
- **Frontend (`Staff Management` pages)**: Delete buttons will be removed from all staff lists and cards. UI will be upgraded to use premium design tokens, dynamic hover effects, and clean layouts.
- **Database**: No schema changes required if `is_active` is already a standard Django field, otherwise requires modifying the User model to include a robust status field.

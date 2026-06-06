## 1. Upgrade Staff & HR Components

- [x] 1.1 Update `src/Pages/StaffPage.jsx`, `AddStaffPage.jsx`, and `EditStaffPage.jsx` to use `hasPermission('staff:edit_any')` (or tenant variants) instead of `.includes()`.
- [x] 1.2 Update `src/Pages/PenaltyManagementPage.jsx` to use `hasPermission('penalties:edit_any')`.
- [x] 1.3 Update `src/Components/common/CompanySwitcher.jsx` to check wildcard or superuser traits instead of `access_flag`.

## 2. Upgrade Tasks & Leads Components

- [x] 2.1 Update `TasksPage.jsx`, `MyTasksPage.jsx`, `TaskViewPage.jsx`, and `TaskCreationPage.jsx` to utilize `hasPermission` for task logic instead of array lookups.
- [x] 2.2 Update `src/Components/leads/ConversionDetailSection.jsx`, `src/Components/leads/LeadsTable.jsx`, `LeadsPage.jsx`, `LeadDetailsPage.jsx`, and `AddLeadPage.jsx` to eliminate `userRole` and array checks, applying explicit `hasPermission('leads:...')` evaluation.
- [x] 2.3 Refactor `src/Components/leads/newlead/AssignedToSection.jsx` role-based filtering logic.

## 3. Upgrade Students & Fees Components

- [x] 3.1 Update `src/Pages/FeesManagementPage.jsx` to map `manage_fees`, `restructure_fees`, etc., to `fees:edit_any` or `hasAnyPermission('fees')`.
- [x] 3.2 Update `src/Components/students/StudentCard.jsx` to remove `.includes()`.
- [x] 3.3 Update `src/Pages/CandidatesPage.jsx` and `CandidateDetailPage.jsx`.

## 4. Upgrade Global Context & Dashboard

- [x] 4.1 Update global routes in `src/App.jsx` to consume `usePermissions()` logic.
- [x] 4.2 Replace `user.role === 'ADMIN'` and `isAdmin` flag derivations in `src/Pages/DashboardOverview.jsx`, `src/Pages/AllFollowUpsPage.jsx`, and `RecentActivities.jsx` to derive capabilities natively via `hasPermission('staff:read_any')` or wildcard checks.

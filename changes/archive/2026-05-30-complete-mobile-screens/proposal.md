## Why

The mobile application currently only implements a subset (5 out of 13) of the CRM screens available on the web version. Because the Dynamic Tab Navigator strictly filters tabs based on the backend RBAC permissions, users who have permissions only for the missing screens (e.g., HR viewing Penalties or Candidates) see a blank app or fewer tabs than expected, with the Menu button disappearing entirely. This change builds out the rest of the CRM mobile screens to reach 100% feature parity with the web platform.

## What Changes

- Create mobile React Native screens for:
  - Mark Attendance
  - Penalties
  - Attendance Docs
  - Candidates
  - Staff Reports
  - Voxbay (Call Analytics)
- Ensure all new screens match the company design language (Purple/Indigo and White).
- Update `MainTabNavigator.tsx`'s `mobileMasterNavigation` to map the backend permissions for these new screens so they dynamically appear in the Tab Bar or the "Menu" overflow screen based on user roles.

## Capabilities

### New Capabilities
- `mobile-extended-crm`: Implements the UI and API wiring for the extended set of CRM features on mobile (Attendance, Penalties, Candidates, Reports, Call Analytics).

### Modified Capabilities
- `mobile-app-foundation`: Modifies the navigation config to register all 13 screens.

## Impact

- **Mobile Frontend (`lpcrm-mobile`)**: Addition of several new screen components in `src/screens/`. Update to navigation stack and tab configuration. No impact to backend APIs.

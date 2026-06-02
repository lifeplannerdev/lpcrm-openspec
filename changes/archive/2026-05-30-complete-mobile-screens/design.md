## Context

The React Native application currently uses a `MainTabNavigator` with an array `mobileMasterNavigation` that only defines 5 screens. The backend RBAC returns permissions that cover 13 different areas (such as Penalties, Attendance, Candidates, etc.). Without mapping these permissions to physical React Native screens, users with non-standard roles see an incomplete UI. 

## Goals / Non-Goals

**Goals:**
- Implement all remaining CRM screens required by the backend RBAC (Mark Attendance, Penalties, Attendance Docs, Candidates, Staff Reports, Voxbay).
- Ensure all screens conform to the company design language (Purple and White, `bg-gray-50` backdrop, `ScreenWrapper`, white cards).
- Wire these new screens into `mobileMasterNavigation` so they can dynamically appear in the Tab Bar or Menu based on the user's permissions.

**Non-Goals:**
- We are not fully implementing the complex backend API logic for every single new screen in this initial pass; they will start as structured, styled placeholders that can be wired to the API incrementally.
- We are not modifying the backend RBAC logic.

## Decisions

- **Screen Placement**: We will group related screens into files (e.g., `HrScreens.tsx` for Penalties and Attendance, `ReportScreens.tsx` for Reports and Call Analytics) to avoid cluttering the `screens/` directory with 10 different files.
- **Styling Strategy**: We will consistently use `ScreenWrapper`, `Text`, and `View` from React Native wrapped with NativeWind utility classes (e.g., `bg-white p-4 rounded-xl shadow-sm border border-gray-100`) to perfectly match the existing UI. Purple (`#7c3aed` or `text-purple-600`) will be used for primary accents.
- **Navigation Configuration**: `MainTabNavigator.tsx` will be updated to include all 13 items with precise `requiredPermission` fields matching the backend schema exactly (e.g. `view_penalties`, `view_candidates`).

## Risks / Trade-offs

- **Risk**: Creating placeholders means the data isn't real yet.
- **Mitigation**: We will clearly indicate empty states or loading states so the user knows the UI is a structured layout awaiting data integration.

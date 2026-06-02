## Context

The current ecosystem consists of a React-based web application (`lpcrm-frontend-main`) and a Node.js/Express backend (`lpcrmbackend-main`) deployed on Vercel. There is a strategic need to expand the product offering with a native mobile application that encompasses the full functionality of the web CRM, including Lead Management, Staff Management, Tasks, Reports, Attendance, Call Analytics, and Chat. 
The new mobile app must be built with React Native and Expo, providing a unified and high-quality UI/UX for both iOS and Android platforms, including compatibility with the latest Android 16 platform.

## Goals / Non-Goals

**Goals:**
- Architect a new mobile application using React Native and Expo.
- Ensure 100% feature parity with the web version (Dashboard, Leads, Staff, Students, Tasks, Reports, Chat, Calls).
- Implement a premium, responsive, and beautiful mobile UI utilizing modern React Native styling and component libraries.
- Seamlessly integrate with the existing Vercel-hosted backend APIs.
- Deliver cross-platform support out-of-the-box (iOS and Android 16).

**Non-Goals:**
- Modifying the core architecture of the backend APIs.
- Introducing features in the mobile app that do not exist in the web app.
- Migrating the web app to a different framework.

## Decisions

- **Framework: React Native with Expo**
  - *Rationale*: Expo provides a robust and streamlined development environment for React Native. It handles complex native dependencies, allows rapid iteration (via Expo Go / Dev builds), and simplifies the build and deployment process (EAS Build) for both iOS and Android.
  - *Alternatives considered*: Bare React Native (higher maintenance overhead for native modules), Flutter (would require learning Dart, whereas the team already knows React/JS).

- **UI & Styling: NativeWind (Tailwind for React Native) or Restyle / Expo UI**
  - *Rationale*: To achieve a beautiful and modern UI rapidly, adopting a utility-first styling library like NativeWind or a robust component library (like React Native Paper or UI Kitten) is essential. Given the requirement for a "beautiful" UI, we will lean towards custom styled components combined with Reanimated for micro-animations.
  - *Alternatives considered*: Standard StyleSheet (can be verbose and harder to maintain for a large app).

- **Navigation: React Navigation**
  - *Rationale*: The industry standard for React Native routing. It supports complex nested navigators (Stack, Tab, Drawer) which are required for a CRM app with many pages.
  - *Alternatives considered*: Expo Router (a viable modern alternative if file-based routing is preferred; we will evaluate Expo Router during implementation for potential DX improvements).

- **State Management: Zustand / React Context**
  - *Rationale*: Lightweight, boilerplate-free state management for handling global state (Auth, User Profile, global notifications).
  - *Alternatives considered*: Redux Toolkit (might be overkill unless the state is exceptionally complex).

- **Data Fetching: Axios / TanStack Query**
  - *Rationale*: TanStack Query (React Query) is optimal for caching, background fetching, and managing server state derived from the Vercel backend.

## Risks / Trade-offs

- [Risk] Performance bottlenecks in heavy list views (e.g., All Follow Ups, Call Analytics) on older mobile devices.
  - *Mitigation*: Utilize `FlashList` (by Shopify) instead of standard `FlatList` for performant rendering of large datasets.
- [Risk] Push notifications setup complexity for Chat and Tasks.
  - *Mitigation*: Leverage Expo Notifications which provides a unified API for interacting with APNs and FCM.
- [Risk] Android 16 specific edge cases.
  - *Mitigation*: Use the latest version of Expo SDK and test early on Android 16 emulators.

## Migration Plan

- The mobile app will be developed in a completely separate repository/folder (`lpcrm-mobile`).
- It will consume the existing production (or staging) APIs. No backend migration is necessary, although minor API tweaks (like returning pagination metadata in a mobile-friendly format) might be requested if needed.
- Rollout can be staged via TestFlight (iOS) and Google Play Console Internal Testing (Android).

## Open Questions

- Should we use Expo Router (file-based routing) or stick to the traditional React Navigation imperative API?
- Do we need offline support for any CRM features, or is an always-online assumption acceptable?
- Are there any specific native device features (e.g., Camera for Attendance Documents, Contacts integration) that require custom Expo plugins?

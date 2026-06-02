## 1. Project Initialization

- [x] 1.1 Create new React Native Expo project named `lpcrm-mobile` using `npx create-expo-app`
- [x] 1.2 Setup ESLint, Prettier, and basic project configuration
- [x] 1.3 Install and configure navigation libraries (React Navigation)
- [x] 1.4 Install and configure UI and styling libraries
- [x] 1.5 Install data fetching and state management libraries (TanStack Query, Zustand, Axios)

## 2. Core Navigation & Layout

- [x] 2.1 Create the Root Navigator handling authenticated and unauthenticated states
- [x] 2.2 Create the Auth Stack Navigator (Login, Forgot Password)
- [x] 2.3 Create the Main Tab Navigator (Dashboard, Leads, Tasks, Chat, Profile)
- [x] 2.4 Build the base layout components (Header, Screen wrapper, SafeAreaView integration)

## 3. Authentication & API Setup

- [x] 3.1 Create Axios instance with base URL pointing to the Vercel backend
- [x] 3.2 Implement interceptors for attaching the auth token to requests
- [x] 3.3 Implement login form UI and wire it to the `/api/auth/login` endpoint
- [x] 3.4 Implement secure token storage (saving upon login, retrieving on startup, deleting on logout)

## 4. CRM Features: Dashboard & Leads

- [x] 4.1 Implement Dashboard UI with summary metrics (total leads, tasks due, etc.)
- [x] 4.2 Wire Dashboard metrics to backend API using TanStack Query
- [x] 4.3 Implement Leads List view with FlatList/FlashList and basic search/filtering
- [x] 4.4 Wire Leads List to backend API
- [x] 4.5 Implement "Add Lead" mobile form with validation
- [x] 4.6 Implement Lead Detail View

## 5. CRM Features: Staff, Students, Tasks

- [x] 5.1 Implement Staff List and Detail views
- [x] 5.2 Implement Students List, Add Student form, and Detail views
- [x] 5.3 Implement Tasks List (My Tasks, All Tasks based on role)
- [x] 5.4 Implement Task Creation and Edit mobile forms
- [x] 5.5 Wire Tasks screens to backend API

## 6. Advanced Features: Chat, Reports, Analytics

- [x] 6.1 Implement mobile Chat interface
- [x] 6.2 Implement Reports views
- [x] 6.3 Implement Call Analytics views

## 7. Polish & Optimization

- [x] 7.1 Review application UI across Android and iOS emulators
- [x] 7.2 Optimize list rendering performance (FlashList integration where needed)
- [x] 7.3 Implement comprehensive loading states and pull-to-refresh on lists
- [x] 7.4 Test against Android 16 simulator for any deprecation issues or UI glitches
- [x] 7.5 Create standard application icon and splash screen configuration

## 8. Dynamic Role-Based Navigation

- [x] 8.1 Create mobile master navigation configuration mapping permissions to components
- [x] 8.2 Refactor MainTabNavigator to filter tabs based on user permissions
- [x] 8.3 Implement "More Menu" fallback for users with >4 permissions

## Purpose
Defines the capabilities, architecture, navigation, and feature parity requirements for the React Native (Expo) mobile application.

## Requirements

### Requirement: React Native Expo Project Structure
The mobile application SHALL be built as a standalone React Native project initialized via Expo.

#### Scenario: App Initialization
- **WHEN** the user opens the application
- **THEN** the Expo framework loads the root navigation container

### Requirement: Cross-Platform Support
The application SHALL function correctly on both iOS and Android (including Android 16) with platform-specific optimizations where necessary.

#### Scenario: Running on Android 16
- **WHEN** the application is compiled and run on an Android 16 device
- **THEN** the application renders correctly without deprecation warnings or crash loops

### Requirement: Vercel Backend Integration
The mobile application SHALL communicate with the existing Node.js/Express backend hosted on Vercel.

#### Scenario: Fetching Data from Backend
- **WHEN** the app requests a list of tasks
- **THEN** it successfully connects to the Vercel API, parses the JSON response, and updates the local state

### Requirement: Network Error Handling
The application SHALL gracefully handle network errors, timeouts, and offline states since mobile connections can be unstable.

#### Scenario: API Timeout
- **WHEN** an API request times out due to poor connectivity
- **THEN** the application displays a user-friendly error message and offers a retry option

### Requirement: Mobile Authentication Flow
The application SHALL implement login and registration interfaces specifically designed for mobile screens.

#### Scenario: Successful Login
- **WHEN** a user enters valid credentials and taps Login
- **THEN** the system authenticates the user, stores the token securely, and redirects to the Dashboard

### Requirement: Secure Token Storage
The application SHALL store authentication tokens securely using encrypted storage on the device.

#### Scenario: App Restart with Token
- **WHEN** the user closes and reopens the app
- **THEN** the application retrieves the stored token and automatically logs the user in without requiring credentials

### Requirement: Global Screen Wrapper
The system SHALL provide a `ScreenWrapper` component to standardize screen layouts.

#### Scenario: Rendering a standard screen
- **WHEN** a screen uses `ScreenWrapper`
- **THEN** it renders with an edge-to-edge `LinearGradient` background (Deep Indigo to White)
- **THEN** it respects the safe area insets using `SafeAreaView`

### Requirement: Mobile Premium UI
The features SHALL be presented using a beautiful, responsive, and modern mobile UI using a robust styling system.

#### Scenario: Interacting with Lists
- **WHEN** the user scrolls through a long list of students or leads
- **THEN** the UI remains smooth (60fps) and visual feedback is provided

### Requirement: Navigation Structure
The application SHALL implement robust navigation using React Navigation to handle auth flows, tab navigation, and stack navigation for deep links.

#### Scenario: Navigating between tabs
- **WHEN** the user taps a bottom tab icon
- **THEN** the application smoothly transitions to the selected tab's screen

### Requirement: Role-Based Navigation System
The system SHALL dynamically filter the mobile MainTabNavigator based on the logged-in user's permissions array. It MUST support up to 13 distinct CRM screens.

#### Scenario: User has permissions for all screens
- **WHEN** user logs in with an Admin role
- **THEN** the Tab Bar renders the first 4 screens (e.g. Dashboard, Leads, Tasks, Chat)
- **THEN** the Tab Bar renders a 5th 'Menu' tab
- **THEN** clicking 'Menu' opens a grid containing the remaining screens

### Requirement: Tasks Module Navigation
The system SHALL support deep navigation within the Tasks tab.

#### Scenario: Navigating to Task Details
- **WHEN** the user is on the main Tasks screen
- **THEN** they see a list of tasks
- **WHEN** they tap a specific task
- **THEN** the app pushes the `TaskDetailsScreen` onto the navigation stack, preserving the bottom tab bar.

### Requirement: Task Creation Form
The system SHALL provide a form to create a new Task.
- The form MUST include fields for Title, Description, Priority, Deadline, and Assigned Staff.
- The form MUST only be accessible to users with the `edit_tasks` permission.

#### Scenario: Authorized user creates a task
- **GIVEN** a user has `edit_tasks` permission
- **WHEN** they tap the Create Task FAB on the Tasks list
- **THEN** they are presented with the Task Creation form
- **WHEN** they submit valid details
- **THEN** the task is created on the backend and they are returned to the Tasks list

### Requirement: Task Details and Status Update
The system SHALL allow users to view detailed information about a task and update its status.

#### Scenario: User updates a task status
- **WHEN** a user taps a task in the list
- **THEN** they are navigated to the Task Details screen
- **WHEN** they change the status dropdown from PENDING to COMPLETED
- **THEN** the backend is updated and the list reflects the new status

### Requirement: Dashboard Parity
The mobile application SHALL provide a dashboard summarizing key metrics, mirroring the capabilities of the web application.

#### Scenario: Viewing Dashboard Metrics
- **WHEN** the user navigates to the Dashboard tab
- **THEN** they see an overview of their leads, tasks, and recent activities formatted for a mobile screen

### Requirement: CRM Features Parity
The mobile application SHALL implement all core CRM features including Leads, Staff, Students, Tasks, and Reports.

#### Scenario: Adding a New Lead
- **WHEN** the user taps the "Add Lead" button and fills out the mobile-optimized form
- **THEN** the new lead is successfully created and appears in the Leads list

### Requirement: Mark Attendance Screen
The system SHALL provide a screen for users with `mark_attendance` permission to view and mark attendance.

#### Scenario: User navigates to Mark Attendance
- **WHEN** user selects Mark Attendance from the mobile menu
- **THEN** they see the Attendance interface matching the purple and white UI guidelines

### Requirement: Penalties Screen
The system SHALL provide a screen for users with `view_penalties` permission to view HR penalties.

#### Scenario: User navigates to Penalties
- **WHEN** user selects Penalties from the mobile menu
- **THEN** they see the Penalties interface

### Requirement: Attendance Docs Screen
The system SHALL provide a screen for users with `view_attendance_docs` permission to view HR attendance documents.

#### Scenario: User navigates to Attendance Docs
- **WHEN** user selects Attendance Docs
- **THEN** they see the document interface

### Requirement: Candidates Screen
The system SHALL provide a screen for users with `view_candidates` permission to view recruitment candidates.

#### Scenario: User navigates to Candidates
- **WHEN** user selects Candidates
- **THEN** they see the Candidates interface

### Requirement: Staff Reports Screen
The system SHALL provide a screen for users with `view_staff_reports` permission to view daily reports.

#### Scenario: User navigates to Reports
- **WHEN** user selects Staff Reports
- **THEN** they see the Reports interface

### Requirement: Voxbay Analytics Screen
The system SHALL provide a screen for users with `view_voxbay` permission to view call analytics.

#### Scenario: User navigates to Voxbay
- **WHEN** user selects Voxbay
- **THEN** they see the Call Analytics interface

## MODIFIED Requirements

### Requirement: Global Screen Wrapper
The system SHALL provide a `ScreenWrapper` component to standardize screen layouts.

#### Scenario: Rendering a standard screen
- **WHEN** a screen uses `ScreenWrapper`
- **THEN** it renders with an edge-to-edge `LinearGradient` background (Deep Indigo to White)
- **THEN** it respects the safe area insets using `SafeAreaView`


<!-- Synced from complete-mobile-screens -->

## MODIFIED Requirements

### Requirement: Role-Based Navigation System
The system SHALL dynamically filter the mobile MainTabNavigator based on the logged-in user's permissions array. It MUST support up to 13 distinct CRM screens.

#### Scenario: User has permissions for all 13 screens
- **WHEN** user logs in with an Admin role
- **THEN** the Tab Bar renders the first 4 screens (e.g. Dashboard, Leads, Tasks, Chat)
- **THEN** the Tab Bar renders a 5th 'Menu' tab
- **THEN** clicking 'Menu' opens a grid containing the remaining 9 screens (Staff, Students, Penalties, Candidates, Reports, etc.)



<!-- Synced from create-mobile-app -->

## ADDED Requirements

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

### Requirement: Navigation Structure
The application SHALL implement robust navigation using React Navigation to handle auth flows, tab navigation, and stack navigation for deep links.

#### Scenario: Navigating between tabs
- **WHEN** the user taps a bottom tab icon
- **THEN** the application smoothly transitions to the selected tab's screen


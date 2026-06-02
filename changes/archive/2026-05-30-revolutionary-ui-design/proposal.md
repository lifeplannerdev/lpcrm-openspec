## Why

The current mobile app utilizes a clean, utilitarian design (white cards with borders on a gray background). While functional, it lacks the "wow factor" expected of a premium, modern enterprise CRM. We need a revolutionary, state-of-the-art UI overhaul that makes the app feel dynamic, expensive, and deeply engaging, while strictly adhering to the established brand scheme of Purple and White.

## What Changes

- **Glassmorphism & Gradients**: Replace flat gray backgrounds with deep, sweeping mesh gradients in shades of purple and indigo. 
- **Translucent Cards**: Convert solid white flat cards into frosted-glass translucent panels (`expo-blur`) to create a stunning depth effect.
- **Micro-animations**: Integrate smooth entrance animations and press interactions (bouncing icons, scaling cards) using React Native Reanimated.
- **Curved Typography & Layouts**: Introduce softer border radii (`rounded-3xl`), dynamic greeting headers, and floating action elements to break out of rigid grid structures.
- **Redesigned Menu & Dashboard**: The Menu grid will be transformed from a static list of icons into a floating, animated launchpad.

## Capabilities

### New Capabilities
- `premium-ui-system`: Introduces the glassmorphic components, animated wrappers, and gradient backgrounds.

### Modified Capabilities
- `mobile-app-foundation`: Modifies the base `ScreenWrapper` to support dynamic mesh gradient backgrounds instead of a flat gray color.

## Impact

- **Mobile Frontend (`lpcrm-mobile`)**: Heavy modifications to `ScreenWrapper`, `MenuScreen`, and `DashboardScreen`. Addition of dependencies `expo-linear-gradient`, `expo-blur`, and `react-native-reanimated`. No backend API changes.

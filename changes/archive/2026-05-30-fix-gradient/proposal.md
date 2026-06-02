## Why
The newly implemented revolutionary UI design failed to render the deep purple gradient background. This occurred because NativeWind's utility classes (`className="absolute w-full h-full"`) did not properly pass width and height dimensions to the third-party `LinearGradient` component. As a result, the gradient collapsed to zero dimensions, causing the white text to render invisibly on a light gray default background.

## What Changes
- Modify `ScreenWrapper.tsx` to use standard React Native absolute positioning instead of NativeWind classes for the `LinearGradient`.

## Capabilities
### Modified Capabilities
- `premium-ui-system`: Updates the foundational UI wrappers to ensure glassmorphic gradients render robustly.

## Impact
- **Mobile Frontend (`lpcrm-mobile`)**: Modifies `src/components/ScreenWrapper.tsx`. No other files or systems are impacted.

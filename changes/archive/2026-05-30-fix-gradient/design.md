## Context
We are fixing a bug where `LinearGradient` from `expo-linear-gradient` renders as a 0x0 pixel component because NativeWind fails to pass `className` utility dimensions correctly to this third-party module.

## Goals / Non-Goals
**Goals:**
- Fix the rendering of `LinearGradient` in `ScreenWrapper`.

## Decisions
- We will use inline style `style={{ position: 'absolute', left: 0, right: 0, top: 0, bottom: 0 }}` on the `LinearGradient` component.
- We will keep NativeWind classes on the `SafeAreaView` and parent `View` since those are standard React Native components that integrate perfectly with NativeWind.

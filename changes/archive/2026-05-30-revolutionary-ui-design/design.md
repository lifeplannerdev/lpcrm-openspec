## Context

The current mobile UI is built entirely with TailwindCSS (NativeWind) utility classes over standard React Native `View` and `Text` components. While this is efficient, it results in a somewhat flat, generic appearance. To achieve a "wow factor", we need to introduce advanced UI techniques that break away from standard flat design while keeping the purple and white branding.

## Goals / Non-Goals

**Goals:**
- Implement a premium, revolutionary UI utilizing Glassmorphism and Mesh Gradients.
- Integrate `expo-blur` and `expo-linear-gradient` to create depth.
- Use `react-native-reanimated` (or standard `Animated`) to add micro-animations to user interactions.
- Completely redesign the `MenuScreen` and `DashboardScreen` to showcase this new aesthetic.

**Non-Goals:**
- We are not changing the core navigation flow or the data fetching logic (TanStack Query remains intact).
- We are not modifying backend endpoints.

## Decisions

- **Backgrounds**: The `ScreenWrapper` will be modified to support an `expo-linear-gradient` background. For the primary brand scheme, we will use a sweeping gradient from deep indigo (`#4c1d95`) to vibrant purple (`#7c3aed`), fading into a soft white/gray (`#f8fafc`) near the bottom of the screen.
- **Glassmorphic Cards**: Instead of `<View className="bg-white">`, we will use `<BlurView intensity={80} tint="light" className="bg-white/40">` or similar transparent overlays. This allows the beautiful gradient background to shine through the cards, giving a frosted glass appearance.
- **Animations**: We will wrap interactive elements in an `Animated.View` that shrinks slightly on press (`Pressable` with `onPressIn` and `onPressOut`) to give immediate tactile feedback, making the app feel alive and responsive.
- **Typography**: We will utilize bolder weights, tighter tracking, and high-contrast text (`text-gray-900` on glass, or `text-white` on deep gradients) to ensure the UI remains highly readable.

## Risks / Trade-offs

- **Risk**: Overusing blurs and gradients can impact rendering performance on older Android devices.
- **Mitigation**: We will keep the blur intensity moderate and avoid nesting multiple BlurViews. We can also use FlashList for long lists to maintain 60FPS scrolling performance.

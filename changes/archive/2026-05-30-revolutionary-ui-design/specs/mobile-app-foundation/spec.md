## MODIFIED Requirements

### Requirement: Global Screen Wrapper
The system SHALL provide a `ScreenWrapper` component to standardize screen layouts.

#### Scenario: Rendering a standard screen
- **WHEN** a screen uses `ScreenWrapper`
- **THEN** it renders with an edge-to-edge `LinearGradient` background (Deep Indigo to White)
- **THEN** it respects the safe area insets using `SafeAreaView`

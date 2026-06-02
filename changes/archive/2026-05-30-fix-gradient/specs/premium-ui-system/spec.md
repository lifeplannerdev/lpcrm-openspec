## MODIFIED Requirements

### Requirement: Global Screen Wrapper
The system SHALL provide a `ScreenWrapper` component to standardize screen layouts.

#### Scenario: Rendering the gradient background
- **WHEN** the `ScreenWrapper` is rendered
- **THEN** it MUST render a `LinearGradient` that stretches to the absolute bounds of the screen, providing a reliable background for white text overlays.

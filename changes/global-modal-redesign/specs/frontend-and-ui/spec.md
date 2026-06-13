## ADDED Requirements

### Requirement: Premium Frontend Modals
The system SHALL display modals and popups using a bounded, internally-scrollable structure to prevent content from hiding beneath sticky headers.
- Modals MUST NOT rely on scrolling the background overlay to view content.
- Modals MUST enforce a maximum height (e.g. `90vh`) relative to the viewport.
- Modals MUST have a fixed header and fixed footer.
- The modal form body MUST scroll independently within the modal container.

#### Scenario: User views a tall form in a modal
- **WHEN** a user opens a modal containing a form taller than the screen
- **THEN** the modal container stays entirely within the screen bounds
- **THEN** the modal body area displays an internal scrollbar
- **THEN** the modal header (title) and footer (save/cancel buttons) remain fixed and visible at all times

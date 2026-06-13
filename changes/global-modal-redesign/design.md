## Context

Currently, frontend modals are using a generic `fixed inset-0 overflow-y-auto` structure. When the modal content exceeds the viewport height, the entire backdrop scrolls, pushing top fields underneath the sticky, semi-transparent header (`sticky top-0 bg-white/80 backdrop-blur-md`). This makes fields like "Asset Name" in the `AssetManagementPage` completely inaccessible or confusingly invisible, breaking the user experience.

## Goals / Non-Goals

**Goals:**
- Implement a consistent, fixed-height, internally-scrollable modal architecture across the entire CRM frontend.
- Ensure headers and footers are always visible without scrolling.
- Prevent fields from becoming hidden behind sticky elements.
- Give a premium, contained "popup" feel rather than a "page that covers the screen".
- Introduce a `Branch` model to group `Location`s by physical offices.

**Non-Goals:**
- We are not changing the backend APIs.
- We are not redesigning the business logic or form validation.
- We are not converting these into separate page routes.

## Decisions

1. **Fixed Container with Internal Scroll**: 
   Instead of `overflow-y-auto` on the dark backdrop overlay, the backdrop will be `flex items-center justify-center overflow-hidden`. The modal card itself will have `max-h-[90vh] flex flex-col`. The internal form wrapper will have `overflow-y-auto flex-1`.
   *Rationale*: This strictly contains the scrolling to the form body. The header and footer will stay perfectly in place.

2. **Fixed Action Footer**:
   The "Save" and "Cancel" buttons, currently placed at the bottom of the long form, will be moved into a fixed footer block at the bottom of the modal (`shrink-0 border-t bg-white px-6 py-4`).
   *Rationale*: Users won't have to scroll all the way down to submit a form. It improves accessibility and usability.

3. **Tighter Form Layout**:
   Inputs padding will be reduced (e.g. from `py-2.5` to `py-2`) and grid gaps slightly tightened.
   *Rationale*: A more compact UI fits more fields on-screen, reducing the need to scroll inside the modal.

4. **Branch Hierarchy**:
   Create a new `Branch` model in `hr/models.py`. Update `Location` to have a foreign key to `Branch`. This allows filtering spaces and assets by Branch (e.g. "Kochi Office").
   *Rationale*: A single flat list of locations isn't scalable across multiple cities.

## Risks / Trade-offs

- **Risk**: Moving submit buttons to a fixed footer might cause issues if forms rely on `onSubmit` handlers deep inside child components. 
  - **Mitigation**: Ensure the submit buttons use `form="form-id"` or we trigger submission via state, or we just wrap the entire `flex flex-col` modal in the `<form>` tag. Wrapping the modal in `<form>` is the cleanest approach.
- **Risk**: Some modals might have unique layouts (like complex grids or tabs) that break when constrained by `max-h-[90vh]`.
  - **Mitigation**: We will manually test each modified page to ensure the internal scrolling works perfectly for edge cases like dropdowns or date pickers.

## Context

The current `DailyReport` model merges the evening report and the next day's agenda into a single submission flow and single timestamp. This prevents granular tracking of when an employee plans their day vs when they report on it. To solve this, we are splitting the submission into two distinct parts (Morning Agenda and Evening Report) and introducing `ReportTimingSettings` to allow admins to define strict deadlines for each employee.

## Goals / Non-Goals

**Goals:**
- Separate "Morning Agenda" and "Evening Report" data internally while displaying them in a unified daily view.
- Support strict deadlines configured per employee via `ReportTimingSettings`.
- Automatically pre-fill the "Morning Agenda" if an employee filled out "Next Day's Agenda" the previous evening.
- Expose clear flags (`On-Time`, `Late Agenda`, `Late Report`, `Missing`) to the frontend for filtering.

**Non-Goals:**
- Removing old reports: Old reports with a single `heading` and `next_day_agenda` will remain, but going forward they will be treated gracefully by the new system.
- Completely preventing late submissions: Users can still submit late, but they will be flagged.

## Decisions

**1. Data Model Split:**
We will update `DailyReport` to have:
- `report_heading` (replaces `heading`)
- `report_text`
- `report_submitted_at`
- `agenda_heading` (new)
- `next_day_agenda` (acts as the Agenda text)
- `agenda_submitted_at` (new)
*Rationale:* Tracking these in one model simplifies the "Daily View" rather than having two separate models for Report and Agenda.

**2. `ReportTimingSettings` Model:**
We will create a new model linked 1-to-1 with `User`.
- `agenda_policy`: Choices of `EVENING_BEFORE` or `MORNING_OF`.
- `agenda_deadline`: e.g., 18:00 or 10:00.
- `report_deadline`: e.g., 18:00.
*Rationale:* Provides ultimate flexibility. The frontend doesn't need to know the policy; it just checks if the text is filled and looks at the calculated flags.

**3. Auto-Carryover Logic:**
When creating or fetching a `DailyReport` for Day N, the system checks Day N-1's `next_day_agenda`. If it exists, the `agenda_heading`, `next_day_agenda` and `agenda_submitted_at` fields on Day N are pre-populated from Day N-1.
*Rationale:* Seamless workflow. The user plans on Monday evening, and Tuesday morning is already handled.

**4. Flag Calculation:**
Flags are calculated dynamically via model properties (`is_agenda_late`, `is_report_late`) by comparing `agenda_submitted_at` to the specific user's `ReportTimingSettings`.

## Risks / Trade-offs

- **Risk:** Existing records won't have `agenda_submitted_at` or `report_submitted_at`.
  **Mitigation:** Fallback to `created_at` or `submission_time` for historical records when calculating lateness.
- **Risk:** Auto-carryover might confuse users if they edit Monday's agenda on Tuesday.
  **Mitigation:** Once a DailyReport is created for Tuesday, it copies the text over. Subsequent edits to Monday's agenda won't affect Tuesday.

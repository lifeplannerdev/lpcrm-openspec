## Context

The "Create Fee Account" form (`FeesManagementPage.jsx`) currently uses a standard text input for the Student ID, which is cumbersome and prone to error since users cannot memorize student IDs. We need to implement a searchable dropdown to select active students, fetched from the backend API. 

## Goals / Non-Goals

**Goals:**
- Replace the Student ID text input with a searchable select component.
- Fetch active students from the existing API (`/trainers/students/` or similar endpoint).
- Pass the selected student's ID into the form state (`createForm.student`).

**Non-Goals:**
- Implementing a brand new student search API if a suitable one already exists.
- Refactoring the entire `FeesManagementPage` state management logic.

## Decisions

- **UI Component**: We will use a standard searchable dropdown or `<select>` depending on what library is already available in the project (e.g. `react-select`). Since there are many students, a simple `<select>` might become unwieldy, but we will start by fetching them and mapping to options. If a combobox library is available, we'll use it.
- **API Endpoint**: We will utilize the existing backend endpoint (likely `GET /students/?company=...`) to retrieve a list of students, storing it in a new state variable `students` alongside `templates` and `accounts`.

## Risks / Trade-offs

- [Risk] Fetching all students at once might be slow if the database is massive. → Mitigation: We can fall back to a paginated search or simple select, but for now, assuming standard usage, a single API fetch for active students on component mount is sufficient.

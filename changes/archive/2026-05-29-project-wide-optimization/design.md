## Context

The current application (both Django backend and React frontend) has grown in features but lacks systematic performance optimizations. As a result, users experience slow page loads across the platform. Since this is a production application, any optimizations must strictly preserve the existing functionality, API contracts, and user interfaces.

## Goals / Non-Goals

**Goals:**
- Eliminate N+1 queries in Django views using `select_related` and `prefetch_related`.
- Optimize large datasets handling (e.g., Reports, Tasks, Leads) on the backend.
- Refactor backend code for cleanliness and better structural organization without altering logic.
- Reduce frontend rendering bottlenecks by implementing React memoization (`React.memo`, `useMemo`, `useCallback`).
- Ensure no breaking changes are introduced to production functionality.

**Non-Goals:**
- Upgrading major framework versions (e.g., migrating from React 17 to 18, or upgrading Django versions) if it introduces breaking changes.
- Completely rewriting the frontend UI or backend architecture.
- Altering any existing API schemas or request/response payloads.

## Decisions

- **Backend Optimization Strategy:** We will systematically audit `views.py` files across all apps (leads, tasks, reports, accounts). We will focus on `get_queryset` methods, ensuring that foreign key relationships are eagerly loaded when serialized. We will also ensure database operations inside loops are vectorized or batched.
- **Frontend Optimization Strategy:** We will audit high-traffic components (e.g., `ReportsPage`, `TasksPage`, `KanbanBoard`). We will wrap child components in `React.memo` to prevent cascading re-renders and wrap inline object/function props with `useMemo` and `useCallback`.
- **Validation:** Every change will be verified by ensuring the API responses remain identical in structure and the UI behaves exactly as before.

## Risks / Trade-offs

- **[Risk] Unintended Breaking Changes:** Modifying querysets or component lifecycles might inadvertently break an edge-case feature.
  - *Mitigation:* Changes will be scoped and isolated per component/view. We will rely on manual or automated testing before pushing to production.
- **[Risk] Memory Overhead:** Aggressive `prefetch_related` or `useMemo` can increase memory usage.
  - *Mitigation:* We will only memoize complex computations/renders and only prefetch data that is strictly accessed during serialization.

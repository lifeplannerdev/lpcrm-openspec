## 1. Backend: Setup & Global Optimization

- [x] 1.1 Review Django middleware and database settings to ensure optimal connection pooling and caching configurations.
- [x] 1.2 Implement a query logging utility (or use Django Debug Toolbar temporarily in dev) to identify the slowest views and endpoints.

## 2. Backend: App-Level Query Optimization

- [x] 2.1 Audit and optimize `accounts` app (views and serializers) using `select_related` and `prefetch_related`.
- [x] 2.2 Audit and optimize `leads` app queries to resolve N+1 issues when fetching related user or status records.
- [x] 2.3 Audit and optimize `tasks` app queries (e.g., eager loading `assigned_to` and `assigned_by`).
- [x] 2.4 Audit and optimize `reports` app queries, especially the daily reports aggregations.
- [x] 2.5 Refactor repetitive or bloated view logic across apps into cleaner, centralized utility functions (without changing API contracts).

## 3. Frontend: Component Memoization & Render Optimization

- [x] 3.1 Audit `TasksPage.jsx` and `KanbanBoard.jsx`. Apply `React.memo`, `useMemo`, and `useCallback` to prevent unnecessary re-renders during drag-and-drop or filtering.
- [x] 3.2 Audit `ReportsPage.jsx`. Memoize table rows and filter callbacks to speed up UI responsiveness when applying multiple filters.
- [x] 3.3 Audit `LeadsPage.jsx` and `DashboardOverview.jsx`. Optimize data fetching dependencies and avoid redundant API calls on component remounts.
- [x] 3.4 Review core UI components (Navbar, Sidebar, Modals) and ensure they are not causing app-wide re-renders on minor state changes.

## 4. Final Validation & Cleanup

- [x] 4.1 Perform a complete manual regression test of the optimized pages to ensure no UI or functionality is broken.
- [x] 4.2 Verify network tab payloads to confirm API responses have identical structures to their pre-optimized versions.
- [x] 4.3 Clean up any temporary logging or profiling code added during the optimization process.

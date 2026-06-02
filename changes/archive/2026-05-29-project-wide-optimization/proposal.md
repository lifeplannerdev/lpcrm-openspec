## Why

The application currently suffers from significant performance issues, with noticeable loading times across every page of the website. Because the system is in production and actively used, these performance bottlenecks directly impact user experience and productivity. This change aims to comprehensively optimize both the frontend and backend to deliver a fast, responsive application without introducing any breaking changes to existing features.

## What Changes

- **Backend Query Optimization**: Identify and eliminate N+1 queries in Django ORM, add `select_related` and `prefetch_related` where necessary, and ensure database indexes are utilized effectively.
- **Backend Code Structuring**: Clean up and refactor existing backend views and serializers for efficiency and readability without altering the API contracts.
- **Frontend Render Optimization**: Implement memoization (`React.memo`, `useMemo`, `useCallback`) in the React frontend to prevent unnecessary re-renders.
- **Frontend Data Fetching**: Optimize API calls, potentially introducing better caching or debouncing for search and filter operations.
- **Production Safety**: Ensure all optimizations are strictly non-breaking (no changes to API request/response schemas or core business logic).

## Capabilities

### New Capabilities
- `performance-optimization`: Establishes the non-functional requirements and baselines for system-wide performance and structural cleanliness.

### Modified Capabilities
None

## Impact

- **Backend Views and Serializers**: Widespread but logically identical changes to querysets and data serialization.
- **Frontend Components**: Updates to component lifecycle management and state hooks to improve rendering efficiency.
- **User Experience**: Drastically reduced load times and a smoother UI interactions.
- **Risk**: Since changes are widespread, regression testing is critical to ensure no existing functionality breaks.

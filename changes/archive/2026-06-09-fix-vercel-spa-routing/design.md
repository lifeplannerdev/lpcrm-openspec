## Context

The Single Page Application is deployed on Vercel. Currently, client-side routing works for internal link clicks, but direct navigation or page refreshes to sub-paths (e.g., `/leads`) return a 404 error from Vercel's server because those files do not exist.

## Goals / Non-Goals

**Goals:**
- Fix the 404 error on page refresh or direct navigation for all valid client-side routes.
- Use Vercel's native configuration file for a simple, maintainable solution.

**Non-Goals:**
- Implement Server-Side Rendering (SSR).
- Modify the React Router setup or change how routes are defined in the frontend code.

## Decisions

- **Add `vercel.json` rewrite rule**: We will add a `vercel.json` file to the root of the frontend project (`lpcrm-frontend-main`) with a `rewrites` configuration that routes all traffic (`/(.*)`) to `/index.html`. This tells Vercel to serve the main HTML file for any route not found, allowing React Router to handle the URL on the client-side.

## Risks / Trade-offs

- **Broken Static Assets**: Static assets (like images or CSS) might be accidentally rewritten to `index.html` if their paths are broken. → Mitigation: Vercel prioritizes existing files over rewrites by default, so valid assets will still load correctly.

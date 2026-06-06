## Why

When users navigate directly to a route like `/leads` or refresh the page, they encounter a Vercel 404 NOT_FOUND error. This happens because the React app relies on client-side routing, but the server is looking for actual files at those paths instead of serving `index.html`. We need to fix this to ensure a seamless experience for users accessing or reloading any valid client-side route.

## What Changes

- Add a Vercel configuration file (`vercel.json`) to the frontend directory (`lpcrm-frontend-main`) to implement a catch-all rewrite rule.
- Configure all missing routes to fallback to `/index.html`, allowing React Router to handle the routing properly.

## Capabilities

### New Capabilities

- `spa-routing-fallback`: Catch-all routing fallback for the Single Page Application hosted on Vercel.

### Modified Capabilities

## Impact

- Frontend application (`lpcrm-frontend-main`).
- Vercel deployment configuration.

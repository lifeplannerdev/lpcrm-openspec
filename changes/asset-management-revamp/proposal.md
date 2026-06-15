# Asset Management & Staff View Refactoring

## Problem
Currently, the asset management system handles mobile devices and SIM cards inefficiently (as text fields). It lacks advanced filtering and search by phone number. Furthermore, the Space Inventory detail views and the Staff Profile views fail to fully surface assigned assets, locations, and responsibilities, leading to a fragmented view of resource allocation.

## Proposed Solution
1. **First-Class SIM Assets:** Model SIM cards as their own assets. Mobile phones will link to SIM assets via `primary_sim` and `secondary_sim` fields.
2. **Simplified Lifecycle:** Remove the redundant `status` field. All unassigned assets are "Available", and broken/maintenance items are simply assigned to the "IT Department".
3. **Enhanced Discovery:** Upgrade the global asset search to support phone number lookups, and add a Category/Type filter dropdown.
4. **Space Inventory Sync:** Fix the backend APIs and frontend UI for Location Detail views to correctly show the people and assets assigned to that specific room/location.
5. **Unified Staff View:** Upgrade both the admin's Staff Detail page and the staff's own "My Assets" page to comprehensively display assigned Mobiles, assigned SIMs, and locations they are responsible for.

## Scope
- Backend (`hr` app): Asset model changes, migrations, updated serializers for Assets, Locations, and Staff.
- Frontend (`lpcrm-frontend-main`): Asset Management list updates (filters/search), Asset Modal updates (SIM dropdowns & swap logic), Location Details page updates, and Staff View / My Assets page updates.

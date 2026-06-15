## 1. Backend: Asset Model & Migrations
- [x] 1.1 Update `Asset` model: add `primary_sim` and `secondary_sim` (ForeignKey to self), add `provider` field, remove `status` field.
- [x] 1.2 Create and run Django migrations.
- [x] 1.3 Update `AssetSerializer` to handle the new fields and nested read views for SIMs.

## 2. Backend: API Logic & Filters
- [x] 2.1 Implement SIM swap logic in the Asset `update` view/serializer.
- [x] 2.2 Update Asset ViewSet search backends to search by `primary_sim__name` and `secondary_sim__name`.
- [x] 2.3 Add `category` filter to Asset ViewSet.
- [x] 2.4 Update Location API to include `assigned_staff` and `assigned_assets`.
- [x] 2.5 Update Staff/Me API to include `assigned_assets` and `responsible_locations`.

## 3. Frontend: Asset Management & Search
- [x] 3.1 Update `AssetManagementPage.jsx` to include the Category filter dropdown.
- [x] 3.2 Ensure the global search bar queries phone numbers effectively.
- [x] 3.3 Update the Add/Edit Asset Modal:
  - Remove `status` field.
  - Add Provider field (visible only if Category is "SIM Card").
  - Add Primary/Secondary SIM dropdowns (visible if Category is "Mobile").
  - Implement the UI prompt confirming a SIM swap.

## 4. Frontend: Space Inventory & Staff Views
- [x] 4.1 Fix the Space Inventory Location Detail view to correctly render assigned people and personal assets.
- [x] 4.2 Upgrade the Admin Staff Detail view to show assigned mobiles, SIMs, and responsible areas.
- [x] 4.3 Upgrade the Employee "My Assets" view to reflect the same comprehensive data.

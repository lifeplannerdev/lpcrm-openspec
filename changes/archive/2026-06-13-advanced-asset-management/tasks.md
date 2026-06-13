## 1. Backend Database Changes

- [x] 1.1 Create `Location` model in `hr/models.py` with fields: name, company.
- [x] 1.2 Create `AssetCategory` model in `hr/models.py` with fields: name.
- [x] 1.3 Add `assigned_location` (ForeignKey to Location), `category` (ForeignKey to AssetCategory), `primary_phone_number` (CharField), and `secondary_phone_number` (CharField) to the `Asset` model.
- [x] 1.4 Write and execute a data migration script to populate initial AssetCategories (Mobiles, Laptops, AC, Teapoy, etc.) and map existing `Asset.asset_type` to `Asset.category`.
- [x] 1.5 Remove `asset_type` field from `Asset` model and drop `ASSET_TYPE_CHOICES` from the code.
- [x] 1.6 Update Django Admin for `hr` app to include `Location` and `AssetCategory`, and update `Asset` admin view.

## 2. Backend API Updates

- [x] 2.1 Update `AssetSerializer` in `hr/serializers.py` to include location details, category details, and the new phone number fields.
- [x] 2.2 Create ModelViewSets and serializers for `Location` and `AssetCategory`.
- [x] 2.3 Add routing for `/locations/` and `/asset-categories/` endpoints in `hr/urls.py` (or appropriate router).
- [x] 2.4 Update `AssetViewSet` to support filtering by `location_id` and `category_id`.
- [x] 2.5 Implement aggregated summary API endpoint (or modify list view) to return assets grouped by Location (for the Macro Dashboard).

## 3. Frontend Data and API Hooks

- [x] 3.1 Create/Update API service functions in frontend for fetching, creating, and updating Locations.
- [x] 3.2 Create/Update API service functions in frontend for fetching AssetCategories.
- [x] 3.3 Update `AssetManagementPage.jsx` data fetching logic to load Locations and Categories alongside Assets.

## 4. Frontend UI: Space Inventory Dashboard (Macro View)

- [x] 4.1 Build the "Space Inventory" grid layout in `AssetManagementPage.jsx` (or a dedicated component) displaying cards for each Location.
- [x] 4.2 Render summarized badges inside Location cards (e.g., icons with counts for Desktop Setup, AC, etc.).

## 5. Frontend UI: Micro Detail View and Forms

- [x] 5.1 Build the Location Detail modal/view showing specific occupants, bundled Desktop Setups, and individual Room Fixtures.
- [x] 5.2 Update the "Add/Edit Asset" form in `AssetManagementPage.jsx` to replace the static Asset Type dropdown with the dynamic `AssetCategory` dropdown.
- [x] 5.3 Update the "Add/Edit Asset" form to show `Location` assignment alongside the existing `User` assignment (mutually exclusive or distinct fields).
- [x] 5.4 Update the form to dynamically show `Primary Phone Number` and `Secondary Phone Number` inputs if the selected category is "Mobiles".

## 6. Frontend UI: Missing Management Features

- [x] 6.1 Add a "Add Location" button in the Space Inventory view and implement the modal form to create a new Location.
- [x] 6.2 Add a "Manage Categories" button and implement a modal form to create a new AssetCategory.

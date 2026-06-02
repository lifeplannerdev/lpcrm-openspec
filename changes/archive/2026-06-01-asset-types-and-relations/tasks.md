## 1. Backend Data Model Updates

- [x] 1.1 Update `hr.models.Asset`: Add `parent_asset` self-referential `ForeignKey` and enforce choices for `asset_type`.
- [x] 1.2 Update `hr.models.Asset.save()` method to automatically sync `assigned_to` with its parent asset (and update children when parent changes).
- [x] 1.3 Generate and apply Django database migrations for the `hr` app.

## 2. Backend API Updates

- [x] 2.1 Update `hr.serializers.AssetSerializer` to include `parent_asset` and ensure it can be read/written via the API.
- [x] 2.2 Add nested serialization for `attached_assets` so parents can easily return their attached children if necessary.

## 3. Frontend Form Updates

- [x] 3.1 Update `AssetManagementPage.jsx`: Change `asset_type` input to a strict `<select>` dropdown (Mobiles, Monitors, PC, Keyboard, Mouse, Laptops, SIM).
- [x] 3.2 Update `AssetManagementPage.jsx`: Dynamically render "IMEI Number" as the label for `serial_number` when "Mobiles" is selected.
- [x] 3.3 Update `AssetManagementPage.jsx`: Add a "Attach to Asset" `<select>` field to choose a parent asset.
- [x] 3.4 Update `AssetManagementPage.jsx`: Disable or hide the "Assigned To" dropdown when a Parent Asset is selected, since assignment is inherited.

## 4. Frontend Profile View Updates

- [x] 4.1 Refactor `AssignedAssetsSection.jsx` in the Staff Edit profile to visually nest attached assets underneath their primary parent devices.

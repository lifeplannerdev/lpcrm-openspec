## Context

The current Asset model (`hr.Asset`) in the Django backend tracks items using free text fields (`asset_type`) and assigns them directly to employees. There is a need to structure these types into a set list, properly label IMEI numbers for mobile devices, and support hierarchical asset relationships (like a SIM card inside a Mobile phone).

## Goals / Non-Goals

**Goals:**
- Enforce predefined choices for `asset_type` (Mobiles, Monitors, PC, Keyboard, Mouse, Laptops, SIM).
- Repurpose `serial_number` dynamically as "IMEI Number" on the UI for Mobiles.
- Allow assets to be linked to other assets (e.g., SIM -> Mobile).
- Automatically sync the assignment (`assigned_to`) of an attached asset to match its parent asset.

**Non-Goals:**
- Implementing multi-level deep nesting (we only expect one level of nesting, e.g., Device -> Accessory).
- Complex validation algorithms for IMEI lengths/checksums.

## Decisions

### 1. Self-Referential Foreign Key
To support attachments, we will add a `parent_asset = models.ForeignKey('self', on_delete=models.SET_NULL, null=True, blank=True, related_name='attached_assets')` to the `Asset` model.
*Rationale:* This is the standard way to model hierarchical data in Django without creating separate models for Accessories vs Primary Devices.

### 2. Assignment Syncing
We will update the `Asset` model's `save()` method. If an asset has a `parent_asset`, its `assigned_to` will be forced to match `self.parent_asset.assigned_to`. Furthermore, when a parent asset's `assigned_to` changes, all its `attached_assets` should also update their `assigned_to`.
*Rationale:* This prevents data inconsistency where a Mobile is assigned to User A, but its internal SIM is accidentally assigned to User B.

### 3. UI-Only Field Renaming for IMEI
Instead of adding a new database column for IMEI, we will keep the `serial_number` database field. On the React frontend (`AssetManagementPage.jsx`), we will dynamically change the input label to "IMEI Number" if the selected `asset_type` is "Mobiles".
*Rationale:* Avoids database bloat and schema complexity, as an asset will generally have either an IMEI or a Serial Number, rarely both in our context.

## Risks / Trade-offs

- **Risk: Circular references** (Asset A is attached to Asset B, and Asset B is attached to Asset A).
  *Mitigation:* Can be handled by simple UI constraints (only showing unattached primary devices in the "Attach To" dropdown) or a Django `clean()` validation check.
- **Risk: Complex UI nesting.**
  *Mitigation:* Keep the UI simple by only showing one level of indentation on the Staff profile page for attached items.

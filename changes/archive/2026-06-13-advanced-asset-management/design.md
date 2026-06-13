## Context

The current Asset Management system uses a flat `Asset` model with a hardcoded list of asset types, and only allows assignment to a `User`. The business requires tracking physical spaces (Cabins, Reception) and office fixtures (ACs, Teapoys), while visualizing assets in a Matrix/Space view. A change is proposed to introduce `Location`, dynamic `AssetCategory`, and expand the `Asset` model.

## Goals / Non-Goals

**Goals:**
- Introduce a `Location` model for physical office tracking.
- Create an `AssetCategory` model to remove hardcoded types.
- Support assigning assets to Locations instead of Users.
- Flatten mobile tracking by adding primary/secondary phone number fields directly to Mobile-type assets.

**Non-Goals:**
- We are not implementing geospatial tracking or interactive visual floor plans. Simple location categories (like "Cabin 1") are sufficient.

## Decisions

- **Decision 1: Assigning Assets to Locations vs Users**
  - **Rationale**: An `Asset` can have a nullable `assigned_to` (User ForeignKey) and a nullable `assigned_location` (Location ForeignKey). If `assigned_to` is populated, the asset is personal. If `assigned_location` is populated, the asset is an office fixture.
- **Decision 2: Dynamic Asset Categories**
  - **Rationale**: Replaces `ASSET_TYPE_CHOICES`. An `AssetCategory` model with a `name` field. This allows admins to add unlimited categories without deploying code.
- **Decision 3: Flattening Mobile Phone fields**
  - **Rationale**: Instead of creating separate "SIM" assets and linking them via `parent_asset`, the `Asset` model gets `primary_phone_number` and `secondary_phone_number` fields. The frontend will dynamically render these fields if the selected Category name is "Mobiles".

## Risks / Trade-offs

- **Risk**: Migrating existing hardcoded `asset_type` string data to the new `AssetCategory` foreign key.
  - **Mitigation**: A data migration script must be written to first create the standard categories (e.g., 'Mobiles', 'Laptops') and then map existing `Asset.asset_type` strings to the new ForeignKey.
- **Risk**: The frontend Space Inventory dashboard might be computationally heavy if rendering hundreds of assets at once.
  - **Mitigation**: The backend API should provide aggregated summary counts (e.g., "3 Chairs, 1 AC") per Location endpoint instead of forcing the frontend to fetch and map all individual asset records.

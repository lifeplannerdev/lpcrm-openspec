# Design Decisions: Asset Management & Staff Views

## 1. Asset Model Architecture
- **Self-Referencing Foreign Keys:** The `Asset` model will gain `primary_sim` and `secondary_sim` as nullable foreign keys to `self` (or `Asset`). 
- **Provider Field:** Add a `provider` (CharField) to track telecom networks (Jio, Airtel) for SIM cards.
- **Status Removal:** Remove the `status` field. The state of an asset is purely derived from `assigned_to`. Broken assets are assigned to the "IT Department" user.

## 2. SIM Reassignment Logic (Swap)
When an Asset (Phone) is saved with a SIM that is already assigned to another Phone:
- The backend will forcefully `nullify` the SIM from the original Phone and attach it to the new Phone. 
- *UI Consideration:* The frontend will prompt the user to confirm this swap before sending the API request.

## 3. Search & Filtering
- **Search:** The backend search on `/api/hr/assets/` will check `name`, `serial_number`, `primary_sim__name`, and `secondary_sim__name`. (Assuming SIM assets use their phone number as their `name`).
- **Filter:** Add `category` to the DjangoFilterBackend for the Asset ViewSet.

## 4. Location Details (Space Inventory)
- The Location API needs to serialize `assigned_staff` (users assigned to this location) and `assigned_assets` (assets physically at this location).
- Frontend `LocationDetailsView` must map over these arrays and render them properly.

## 5. Staff View
- The Staff API (and "Me" API) needs to serialize `assigned_assets` (both Mobiles and SIMs) and `responsible_locations`.
- The frontend Staff Profile and "My Assets" components will separate these into clear sections:
  - **Mobiles:** (Shows phone details + nested attached SIMs)
  - **Standalone SIMs:** (SIMs assigned directly to the user, not in a company phone)
  - **Responsible Areas:** (Locations they manage)

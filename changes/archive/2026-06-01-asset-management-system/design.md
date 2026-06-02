## Context

The company needs a robust system to track physical and digital assets (e.g., laptops, monitors, software licenses) assigned to staff members. Currently, there is no centralized database tracking these assignments, which leads to accountability gaps and difficulty during offboarding. The system requires an intuitive UI, multi-tenant company segregation (e.g., LP vs. FLAG), and deep integration with the existing Staff module.

## Goals / Non-Goals

**Goals:**
- Provide a centralized `Asset` model to track inventory.
- Build a dedicated, highly visual Asset Management frontend with filtering by company, status, and staff member.
- Seamlessly integrate assigned assets into the Staff Profile detail view.
- Implement fine-grained access control so only authorized users can view or manage assets.
- Ensure data separation between different company entities (LP vs FLAG).

**Non-Goals:**
- Deep integration with financial depreciation systems or automatic network discovery of IT assets.
- Multi-step asset request/approval workflows (assets are directly assigned by administrators or authorized staff).

## Decisions

1. **Asset Data Model (Backend):**
   - We will introduce an `Asset` model within the `hr` Django app, as asset management strongly aligns with employee tracking.
   - Fields: `name`, `asset_type` (e.g., Laptop, Mobile, Furniture, License), `serial_number`, `status` (Available, Assigned, Maintenance, Retired), `company` (LP / FLAG), `assigned_to` (ForeignKey to `User`), and `attachment` (CloudinaryField for photos/invoices).
   - Rationale: Storing it in `hr` prevents app sprawl while maintaining a clear relationship with staff.

2. **Company Segregation:**
   - Similar to the `Lead` model, the `Asset` model will include a `company` field with choices `LP` and `FLAG` and a `db_index=True`.
   - All API endpoints returning assets will filter by the requesting user's company context or specific requested company tabs (if the user has access to both).

3. **Frontend UI and UX:**
   - The Asset Management page will use a modern, dynamic table or grid layout (a "wow" design with micro-animations) to display assets.
   - It will feature "LP" and "FLAG" tabs at the top for quick context switching, mimicking the optimized SQL operations used in the Leads list.
   - Staff Profile pages will fetch and display a list of assets where `assigned_to` equals the staff member's ID.

4. **Permissions:**
   - We will utilize Django's built-in permission system, adding specific `view_asset`, `add_asset`, `change_asset`, and `delete_asset` capabilities.
   - The frontend's Staff Permission Assign Screen will be updated to expose these new asset permissions so they can be toggled per staff member.

## Risks / Trade-offs

- **Risk:** Staff profiles become cluttered with historical assets that have been returned.
  - **Mitigation:** Only actively assigned assets (where `status == 'Assigned'`) will show on the main staff profile; historical assignments can be viewed via an audit log or separate tab.
- **Risk:** Cross-company data leakage.
  - **Mitigation:** Ensure all API views implement strict `.filter(company=request_company)` checks aligned with the user's role and allowed companies.

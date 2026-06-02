## Context

The CRM currently assumes a single company context. The new requirement dictates that data must be segregated between two distinct companies ("LP" and "FLAG"), but specific executive roles (CEO, MD, HR) require access to both. The system must filter all list queries by company, validate access control dynamically, and provide a per-page context switching UI.

## Goals / Non-Goals

**Goals:**
- Securely segregate data for LP and FLAG across all major database models.
- Provide a smooth UI toggle for users with dual access, allowing per-page context switching (e.g., viewing FLAG Tasks on one browser tab and LP Staff on another).
- Ensure users who only have access to one company never see the toggle and only see their permitted data.

**Non-Goals:**
- We are **not** building a fully dynamic N-tenant architecture (SaaS-style multi-tenancy). The business logic strictly assumes exactly two companies.

## Decisions

1. **Data Modeling: CharField vs ForeignKey**
   - *Decision:* We will add a `company` `CharField(max_length=10, choices=[('LP', 'LP'), ('FLAG', 'FLAG')], default='LP')` directly to the models rather than creating a separate `Company` table and `ForeignKey`.
   - *Rationale:* Since the scope strictly bounds the system to exactly two companies forever, a CharField is vastly simpler, avoids unnecessary SQL JOINs, and simplifies frontend form handling.

2. **Access Control: Base Field + Single Granular Permission**
   - *Decision:* A user inherently has access to data matching their own `company` field. We will add a single `access_flag` permission to the existing JSON `permissions` array for executives (who belong to LP) so they can access FLAG data.
   - *Rationale:* Avoids redundant permissions like `access_lp`. Since FLAG employees never access LP, and LP employees occasionally access FLAG, a single cross-company permission (`access_flag`) elegantly solves the problem without extra mapping tables.

3. **API Filtering: Base Mixin**
   - *Decision:* Create a `CompanyFilterMixin` for DRF ViewSets.
   - *Rationale:* The Mixin will inspect the `company` query parameter. If it matches the user's own `company`, access is granted. If they are querying `FLAG` and have the `access_flag` permission, access is granted. Otherwise, it is blocked. The queryset is then filtered accordingly, significantly reducing the risk of accidental data leakage.

4. **Frontend State: Per-Page URL Query Params**
   - *Decision:* The frontend "Company Switcher" component will store its state locally on the page component, or via the URL (`?view_company=FLAG`), rather than in global React Context.
   - *Rationale:* A global state would cause all pages to flip simultaneously. By keeping it page-scoped, an executive can have the Tasks page open for LP and the Reports page open for FLAG in separate browser tabs without them interfering with each other.

## Risks / Trade-offs

- **Risk:** Developers forget to add the `CompanyFilterMixin` to new endpoints, causing data leakage.
  - *Mitigation:* Clear documentation and code review standards.
- **Risk:** Existing data is left unassigned during the migration.
  - *Mitigation:* The Django database migration will define a default `company='LP'` for all existing records to ensure nothing breaks.

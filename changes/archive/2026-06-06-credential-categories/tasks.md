## 1. Backend Data Model

- [x] 1.1 Create the `CredentialCategory` model (name, color, icon_name)
- [x] 1.2 Add `category` ForeignKey field to the `Credential` model (`on_delete=models.SET_NULL`, `null=True`)
- [x] 1.3 Create and run the Django migrations for the new model and field

## 2. Backend API

- [x] 2.1 Create `CredentialCategorySerializer`
- [x] 2.2 Create `CredentialCategoryViewSet` with standard CRUD operations
- [x] 2.3 Implement permissions on `CredentialCategoryViewSet` (require `credentials:manage` for unsafe methods)
- [x] 2.4 Update `CredentialSerializer` and `CredentialDetailSerializer` to include category details
- [x] 2.5 Update API routing for `/api/credential-categories/`

## 3. Frontend UI - Category Management (Admin)

- [x] 3.1 Create a "Manage Categories" button in `CredentialsVault.jsx`, visible only if `hasPermission('credentials:manage')`
- [x] 3.2 Build the `ManageCategoriesModal.jsx` component to list existing categories and provide forms to add/delete them
- [x] 3.3 Create a utility function to map string names to `lucide-react` icons
- [x] 3.4 Wire the "Manage Categories" UI to the backend `/api/credential-categories/` endpoints

## 4. Frontend UI - Forms

- [x] 4.1 Update `fetchCredentials` or create a new hook to fetch all categories on load
- [x] 4.2 Update the "Add Credential" modal to fetch dynamic categories and show a `<select>` dropdown
- [x] 4.3 Update the "Propose Update" modal to include a dropdown for dynamic categories (if supported)

## 5. Frontend UI - Display & Filtering

- [x] 5.1 Add a "Filter by Category" dropdown next to the search bar
- [x] 5.2 Add a "Group by Category" toggle button
- [x] 5.3 Update the credentials list/grid rendering to group items if the toggle is active
- [x] 5.4 Ensure each credential badge displays the correct color and Lucide icon fetched from its linked category

## 6. Verification

- [x] 6.1 Test creating and deleting a dynamic category as an admin
- [x] 6.2 Test creating a credential with a dynamic category, and verify it falls back gracefully if the category is deleted
- [x] 6.3 Test the frontend filtering and grouping UI logic

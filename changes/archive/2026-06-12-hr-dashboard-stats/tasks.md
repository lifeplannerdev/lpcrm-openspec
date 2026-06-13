## 1. Backend Implementation

- [x] 1.1 Update `DashboardStatsAPIView` in `accounts/views.py` to remove strict `ADMIN` role check and initialize an empty dictionary
- [x] 1.2 Import `Candidate`, `Asset`, and `has_dynamic_permission` into `accounts/views.py`
- [x] 1.3 Add conditional check for `leads:read_tenant` to fetch `total_leads`
- [x] 1.4 Add conditional check for `students:read_tenant` to fetch `total_students`
- [x] 1.5 Add conditional check for `staff:read_tenant` to fetch `active_staff`
- [x] 1.6 Add conditional query to fetch `staff_on_leave` count (`User.objects.filter(is_on_leave=True)`) if user has `staff:read_tenant`
- [x] 1.7 Add conditional query to fetch `pending_candidates` count (`Candidate.objects.filter(status='applied')`) if user has `staff:read_tenant` or similar
- [x] 1.8 Ensure API raises `PermissionDenied` if the final response dictionary is empty

## 2. Frontend Implementation

- [x] 2.1 Update `DashboardOverview.jsx` to map new fields (`staff_on_leave`, `pending_candidates`) from the backend response using strict `!== undefined` fallback to `null`
- [x] 2.2 Update `AdminStatsGrid.jsx` to conditionally render `Total Leads`, `Active Staff`, and `Total Students` only when `!== null`
- [x] 2.3 Import additional Lucide icons (`UserMinus`, `UserPlus`) in `AdminStatsGrid.jsx`
- [x] 2.4 Add conditional rendering in `AdminStatsGrid.jsx` for the `Staff On Leave` metric card
- [x] 2.5 Add conditional rendering in `AdminStatsGrid.jsx` for the `Pending Candidates` metric card

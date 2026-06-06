## 1. Update Accounts App

- [x] 1.1 Replace `instance.role` usages in `accounts/signals.py`
- [x] 1.2 Update role checks and metadata assignments in `accounts/views.py`

## 2. Update Leads App

- [x] 2.1 Update role checks in `leads/views/followups.py`
- [x] 2.2 Update role checks in `leads/views/leads.py`
- [x] 2.3 Update role checks in `leads/views/assignments.py`
- [x] 2.4 Update role checks in `leads/serializers.py`

## 3. Update Other Core Apps

- [x] 3.1 Replace `user.role` usages in `tasks/views.py`
- [x] 3.2 Update role checks in `reports/views.py`
- [x] 3.3 Update role checks in `credentials/views.py`
- [x] 3.4 Replace `instance.role` usages in `trainers/signals.py`

## 4. Verification

- [x] 4.1 Test creating a staff user to ensure no 500 error occurs
- [x] 4.2 Test fetching `/api/followups/today/` to ensure no 500 error occurs
- [x] 4.3 Run a global grep for `.role` in `lpcrmbackend-main` to verify no leftover references exist on user objects

## 1. Backend Updates

- [x] 1.1 Update `StudentSerializer.create` in `trainers/serializers.py` to add an `else` block that sends a notification to finance users when a student is created without a `fee_template`.
- [x] 1.2 Verify/Configure Celery Beat settings in the Django project to enable periodic tasks.
- [x] 1.3 Create a new Celery task `send_daily_fee_reminders` in `fees/tasks.py` to query upcoming fee installments and send reminders via `Notification.objects.create`.
- [x] 1.4 Register the `send_daily_fee_reminders` task in the Celery Beat schedule to run daily.

## 2. Frontend Updates

- [x] 2.1 Update `FeesManagementPage.jsx` to fetch the fee summary array from `FeeSummaryAPIView`.
- [x] 2.2 Create a `FeeSummaryDashboard` section at the top of `FeesManagementPage.jsx` to aggregate and display Total Due, Total Paid, Balance Due, and Overdue Amount.

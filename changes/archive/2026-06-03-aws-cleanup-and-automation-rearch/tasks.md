## 1. Vercel & QStash Cleanup

- [x] 1.1 Remove `.env.vercel` and `vercel.json` from the `lpcrmbackend-main` directory.
- [x] 1.2 Remove QStash-specific dependencies from `requirements.txt` (e.g., `upstash-qstash` if it exists).
- [x] 1.3 Remove QStash authentication middleware or signature verification logic from webhook views.
- [x] 1.4 Delete any Vercel-specific API route files or configuration settings that are obsolete on EC2.

## 2. Celery Infrastructure Foundation

- [x] 2.1 Add `celery` and `redis` to `requirements.txt`.
- [x] 2.2 Create `lpcrm/celery.py` to initialize the Celery application instance.
- [x] 2.3 Update `lpcrm/__init__.py` to ensure the Celery app is loaded when Django boots.
- [x] 2.4 Update `lpcrm/settings.py` to include `CELERY_BROKER_URL` and `CELERY_RESULT_BACKEND` pointing to the local Redis instance.

## 3. Core Notification Refactoring

- [x] 3.1 Refactor Pusher notification logic in `utils.py` into a `@shared_task` so it can be called via `.delay()`.
- [x] 3.2 Refactor Email sending logic in `utils.py` into a `@shared_task` to prevent blocking the main thread.

## 4. Webhook & Automation Refactoring

- [x] 4.1 Create `leads/tasks.py` and move the Meta Lead Ad processing logic into a `@shared_task`.
- [x] 4.2 Create `tasks.py` in the telephony app (or inside `leads`) and move the Voxbay processing logic into a `@shared_task`.
- [x] 4.3 Update all incoming webhook endpoints to simply parse the payload, enqueue the respective Celery task, and immediately return a `200 OK`.

## 5. Celery Beat Scheduling

- [x] 5.1 Identify any remaining pseudo-cron logic, management commands, or external pings used for scheduled tasks.
- [x] 5.2 Implement these tasks as `@shared_task` functions inside their respective apps.
- [x] 5.3 Configure `CELERY_BEAT_SCHEDULE` in `settings.py` to define the execution schedule for these background jobs.

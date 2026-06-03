## Why

The current CRM architecture contains residual code and dependencies tied to Vercel (e.g., QStash webhooks, `.env.vercel`, Vercel-specific API configs) which are no longer needed now that the project is running natively on a bare-metal AWS EC2 instance. Furthermore, background tasks, cron jobs, and automations are currently scattered across models, dummy cron files, and external services. To ensure maximum reliability and ease of adding future automations, we need to clean out the unused Vercel artifacts and fully re-architect the background task system around a centralized, robust broker (Celery + Redis) that runs natively on the AWS server.

## What Changes

- **Cleanup Vercel Dependencies**: Remove all Vercel-specific configuration files (`vercel.json`, `.env.vercel`) and uninstall any Vercel/QStash specific packages from `requirements.txt`.
- **Remove Scattered Automations**: Hunt down and remove scattered dummy cron scripts and model-bound automation logic.
- **Centralized Task Broker**: Implement a robust Celery worker and Celery Beat architecture backed by Redis to handle all asynchronous processing.
- **Background Tasks Migration**: Refactor existing webhooks, email sending, and Pusher notifications to utilize the new centralized `@shared_task` system.
- **Automations Architecture**: Define a clean directory structure (e.g., `tasks.py` inside each Django app) where all future automations will natively reside.

## Capabilities

### New Capabilities
- `centralized-task-broker`: A unified Celery + Redis architecture for handling all asynchronous tasks and scheduled automations securely within the AWS VPC.

### Modified Capabilities
- `cron-jobs-system`: Transitioning from external triggers/dummy crons to native Celery Beat scheduled tasks.
- `aws-infrastructure`: Removing Vercel remnants and establishing systemd services for the new Celery workers.

## Impact

- **Codebase**: Deletion of obsolete configuration files; modification of `requirements.txt`; updates to webhook views and `utils.py` to route through Celery.
- **Infrastructure**: Introduces Redis and Celery worker/beat processes to the AWS EC2 instance.
- **Dependencies**: Drops QStash/Vercel dependencies and introduces `celery` and `redis`.

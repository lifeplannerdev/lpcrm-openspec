## Context

The system originally evolved with deployment to Vercel in mind, which introduced serverless-specific constraints (e.g., using QStash for webhooks, missing robust background worker queues, relying on pseudo-cron files or third-party pings for scheduled tasks). Now that the deployment has successfully transitioned to an AWS EC2 instance, these constraints are obsolete. We need to shed the technical debt of the serverless era and embrace a traditional, robust asynchronous architecture (Celery + Redis) to handle all automations, webhook processing, notifications, and scheduled crons.

## Goals / Non-Goals

**Goals:**
- Completely remove all code, configuration files, and dependencies associated with Vercel and QStash.
- Centralize all asynchronous processing (email, pusher notifications, webhook ingestion) into Celery.
- Replace dummy cron and third-party cron triggers with a centralized Celery Beat scheduling architecture.
- Define a standard convention where all app-specific background tasks reside in `tasks.py` inside their respective Django apps.

**Non-Goals:**
- Refactoring the core business logic of the automations (e.g., the actual rules for lead assignment or deduplication). This is strictly an architectural migration of *how* and *where* they run.
- Moving away from the current AWS EC2 architecture.

## Decisions

**Decision 1: Use Celery + Redis**
- *Rationale*: Celery is the industry standard for Django background tasks. Redis is already part of the target EC2 stack (often used for caching or websockets) and serves as an excellent, low-latency broker for Celery.
- *Alternatives Considered*: 
  - Django-Q or Huey: Lighter weight, but Celery offers the best ecosystem, community support, and scalability for complex workflows (canvas, retries).
  - AWS SQS: Better for distributed microservices, but adds AWS SDK overhead and complexity. Redis on the local EC2 is simpler and cheaper for a monolithic setup.

**Decision 2: Remove QStash and Vercel Configs**
- *Rationale*: QStash was explicitly used to bridge the gap for long-running webhooks in Vercel's serverless environment. With Celery, we simply ingest the webhook, push the payload to Redis, and return an immediate `200 OK` response. Thus, QStash is obsolete.

**Decision 3: App-Scoped `tasks.py` convention**
- *Rationale*: Following Django best practices, each app (e.g., `leads`, `hr`, `reports`) will have its own `tasks.py` module containing its specific `@shared_task` functions.

## Risks / Trade-offs

- **Risk: Increased EC2 Memory Usage** → *Mitigation*: Celery workers and Redis will consume additional memory on the EC2 instance. We must monitor the `t4g.medium` instance resources and configure Celery concurrency appropriately (e.g., `--concurrency=2` rather than auto-scaling to all CPU threads if memory is tight).
- **Risk: Missing Tasks during Deployment** → *Mitigation*: Ensure the `deploy.yml` GitHub Actions script cleanly restarts the `lpcrm-celery` and `lpcrm-beat` systemd services to load the new code without dropping active jobs.

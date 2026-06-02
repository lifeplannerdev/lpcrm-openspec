## Context

The current application (LifePlanner CRM) runs on a non-AWS hosting provider with a Python backend, a serverless Postgres database (Neon), and Cloudify for file storage. The system serves a small company (15-60 users). We want to migrate to AWS to improve performance (fewer white screens), implement robust background jobs (Celery/Redis), and aggressively optimize monthly operational costs.

## Goals / Non-Goals

**Goals:**
- Consolidate backend compute, database, and caching onto a single AWS EC2 instance.
- Migrate file storage from Cloudify to Amazon S3.
- Migrate PostgreSQL from Neon to a local Postgres instance on the EC2 server.
- Implement automated nightly database backups to Amazon S3.
- Implement background workers using Celery and Redis managed by `systemd`.
- Migrate React/Vite frontend to AWS Amplify.
- Achieve an estimated total AWS bill of ~$30/month.

**Non-Goals:**
- Using complex container orchestration (Docker/ECS/Fargate) which adds unnecessary overhead for our scale.
- Paying a premium for managed database services (RDS/Aurora).
- Refactoring the entire React frontend code.

## Decisions

- **Hosting the Backend:** We will use a bare-metal AWS EC2 instance (e.g., `t4g.medium`). *Rationale:* Running Python natively with Nginx and `systemd` is incredibly fast, simple to debug, and avoids container orchestration costs.
- **Database:** Local PostgreSQL on the EC2 instance. *Rationale:* Saves ~$15-$45/month compared to RDS/Aurora. Latency between the web API and database is 0ms.
- **Database Backups:** Nightly `pg_dump` uploaded to Amazon S3. *Rationale:* Ensures we never lose data if the EC2 instance fails, utilizing S3's incredibly cheap storage (~$0.05/mo for backups).
- **File Storage:** Amazon S3. *Rationale:* S3 is the industry standard for scalable object storage. It replaces Cloudify for pennies a month.
- **Background Jobs:** Celery and Redis. *Rationale:* Runs natively on the EC2 instance, managed by `systemd`.
- **Hosting the Frontend:** AWS Amplify. *Rationale:* Easiest integration for React/Vite, offering built-in CI/CD, SSL, and CDN.

## Risks / Trade-offs

- **Risk:** EC2 hardware failure causes temporary downtime. → *Mitigation:* The database is safely backed up to S3 every night. If the server dies, we simply provision a new EC2 instance, pull the code, and restore the database from S3.
- **Risk:** Deployment downtime. → *Mitigation:* Deploying code via SSH and restarting `systemd` services takes ~5 seconds, which is acceptable for a small internal CRM. Deployments will be scheduled during off-peak hours.

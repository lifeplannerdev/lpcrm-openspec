## Why

We are migrating our entire architecture to AWS to build a unified, single-platform system while drastically reducing operational costs. By consolidating our compute, caching, and database onto a single, high-performance bare-metal EC2 instance, and utilizing Amazon S3 for documents and backups, we can achieve extreme cost-efficiency (~$30/mo) while gaining the robust background processing (Celery/Redis) we were previously missing.

## What Changes

- Migration of the Python backend from current hosting to a single bare-metal AWS EC2 instance.
- Migration of our PostgreSQL database (Neon) to a local PostgreSQL instance running directly on the EC2 server.
- Implementation of a nightly automated database backup system (`pg_dump` -> AWS S3).
- Setup of local Redis and Celery (Worker + Beat) on the EC2 instance for background cron jobs.
- Migration of our file storage from Cloudify to Amazon S3.
- Migration of the frontend (React/Vite) to Vercel.
- Separation of backend and frontend into independent deployment pipelines (`lpcrmaws-backend` and `lpcrmaws-frontend`).

## Capabilities

### New Capabilities
- `aws-infrastructure`: Core AWS infrastructure setup (EC2, S3, IAM Roles, Security Groups).
- `bare-metal-setup`: Configuration of Ubuntu, Nginx, Python virtual environments, and `systemd` services.
- `cron-jobs-system`: Background processing and scheduling system using Celery and Redis.
- `database-migration`: Migration strategy from Neon to local EC2 PostgreSQL, and automated S3 backups.
- `file-storage-migration`: Migration of documents and media from Cloudify to Amazon S3.
- `ci-cd-pipeline`: Automated deployment pipelines for bare-metal backend updates (SSH) and frontend (Vercel).

### Modified Capabilities


## Impact

- **Infrastructure:** Shift from managed hosting and Neon to a bare-metal, highly optimized EC2 setup.
- **Codebase:** Updates to deployment scripts, configuring Python AWS SDK (boto3) for S3 access, and updating the backend to use S3 for file storage instead of Cloudify.
- **Data:** Moving all existing documents from Cloudify to AWS S3, and migrating Neon data to the local EC2 database.
- **Cost:** Significantly lower and more predictable monthly operational costs.

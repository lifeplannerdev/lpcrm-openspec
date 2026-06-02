## 1. AWS Core Infrastructure

- [x] 1.1 Create AWS Account and configure IAM policies.
- [x] 1.2 Provision a single EC2 Instance (e.g., Ubuntu on `t4g.medium`) and attach an Elastic IP.
- [x] 1.3 Configure EC2 Security Groups (Open ports 80, 443 for web, 22 for SSH, restrict everything else).
- [x] 1.4 Provision an Amazon S3 bucket for file storage and database backups, and configure an IAM User with access keys for the backend.
- [x] 1.5 Configure S3 Lifecycle rules to automatically delete files in the `/backups` folder older than 30 days.

## 2. Bare-Metal EC2 Provisioning

- [x] 2.1 SSH into EC2, update the OS, and create a dedicated `lpcrm` user for running the application.
- [x] 2.2 Install Nginx, PostgreSQL, Redis, and Python 3 on the EC2 instance.
- [x] 2.3 Clone the `lpcrmaws-backend` repository into the `lpcrm` user's home directory.
- [x] 2.4 Set up a Python Virtual Environment (`venv`) and install requirements.

## 3. Database & File Migration

- [ ] 3.1 Create the PostgreSQL database and user on the local EC2 Postgres instance.
- [ ] 3.2 Export the current database from Neon and import it into the local EC2 Postgres instance.
- [ ] 3.3 Write and test a bash script that runs `pg_dump` and uses the AWS CLI to upload the compressed `.sql.gz` file to the S3 bucket.
- [ ] 3.4 Add the backup script to the `lpcrm` user's crontab (e.g., to run daily at 2:00 AM).
- [ ] 3.5 Write a one-off migration script to copy all files and documents from Cloudify to the Amazon S3 bucket.
- [ ] 3.6 Run the file migration script and verify file integrity on S3.

## 4. Backend Configuration & systemd

- [ ] 4.1 Update the backend code to use `boto3` for S3 file storage instead of Cloudify.
- [ ] 4.2 Create the `.env` file on the EC2 instance with the local Database URL, Redis URL, and S3 credentials.
- [ ] 4.3 Create the `lpcrm-web.service` systemd file to run the Python API (Gunicorn/Uvicorn).
- [ ] 4.4 Create the `lpcrm-celery.service` and `lpcrm-beat.service` systemd files for background workers.
- [ ] 4.5 Enable and start all systemd services, and configure Nginx as a reverse proxy (with Certbot/Let's Encrypt for SSL).

## 5. Frontend Deployment (AWS Amplify)

- [ ] 5.1 Connect the `lpcrmaws-frontend` repository to AWS Amplify.
- [ ] 5.2 Configure Amplify build settings for Vite/React (`npm run build`).
- [ ] 5.3 Setup environment variables (e.g., API URL pointing to the new EC2 Elastic IP / Domain).
- [ ] 5.4 Deploy frontend and verify successful page load and API communication.

## 6. DNS and Domain Cutover

- [ ] 6.1 Update your domain's DNS records to point the backend API subdomain to the EC2 Elastic IP.
- [ ] 6.2 Update DNS records to point the frontend root domain to the AWS Amplify endpoint.
- [ ] 6.3 Verify end-to-end traffic flow.

## 7. CI/CD Pipeline Automation

- [ ] 7.1 Setup a GitHub Actions workflow in `lpcrmaws-backend` that securely SSHs into the EC2 instance, runs `git pull`, updates pip dependencies, and restarts the systemd services.
- [ ] 7.2 Verify AWS Amplify triggers automatic deployments on commits to the frontend repository.

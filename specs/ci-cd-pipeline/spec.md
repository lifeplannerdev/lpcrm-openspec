## Purpose
Defines the capabilities and requirements for this domain.

## Requirements

### Requirement: Automated Backend Deployment
The CI/CD pipeline SHALL automatically deploy the Python backend upon merging code to the main branch.

#### Scenario: Successful backend deployment
- **WHEN** a pull request is merged into the `main` branch of the backend repository
- **THEN** GitHub Actions securely SSHs into the EC2 instance, pulls the latest code, and restarts the `systemd` services

### Requirement: Automated Frontend Deployment
The CI/CD pipeline SHALL automatically build and deploy the React frontend via AWS Amplify upon code changes.

#### Scenario: Successful frontend commit
- **WHEN** new code is pushed to the tracked branch for the frontend
- **THEN** AWS Amplify automatically triggers a build and updates the live site

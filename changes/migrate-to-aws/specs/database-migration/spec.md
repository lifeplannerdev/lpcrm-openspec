## ADDED Requirements

### Requirement: Database Parity
The new local EC2 PostgreSQL database SHALL contain all schemas, tables, and data exactly as they exist in the current Neon database post-migration.

#### Scenario: Successful data import
- **WHEN** the `pg_restore` command completes
- **THEN** querying the new database yields the identical record count as the old database

### Requirement: Automated Database Backups
The system SHALL automatically back up the PostgreSQL database every night and store the compressed backup in Amazon S3.

#### Scenario: Nightly backup execution
- **WHEN** the cron job triggers at 2:00 AM
- **THEN** a `.sql.gz` file is created and successfully uploaded to the S3 bucket's `/backups` folder

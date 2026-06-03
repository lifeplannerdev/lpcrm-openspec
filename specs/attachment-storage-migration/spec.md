## ADDED Requirements

### Requirement: S3 Migration Script
The system SHALL provide a management command to download all existing files from Cloudinary and upload them to AWS S3.

#### Scenario: Running the migration
- **WHEN** the `migrate_cloudinary_to_s3` command is executed
- **THEN** it downloads the files associated with `DailyReportAttachment`, `AttendanceDocument`, `Asset`, `Candidate`, and `Message` models, saves them natively to the S3 `FileField`, and commits the transaction

### Requirement: Legacy Cloudinary Removal
The system SHALL NOT contain any references to the `cloudinary` SDK or `CloudinaryField` models in its codebase.

#### Scenario: Serializing file URLs
- **WHEN** the frontend requests a list of reports or attachments
- **THEN** the API serializer returns the native `url` attribute from the `FileField` (which points to S3) without attempting string manipulation or Cloudinary transformations

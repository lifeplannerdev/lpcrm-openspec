## Context

The application currently relies on Cloudinary for handling file attachments across various modules (`reports`, `hr`, `chats`, `accounts`). However, the existing implementation is throwing errors when attempting to parse Cloudinary URLs (specifically for the "LP" company reports), leading to a 500 error when listing reports. The frontend correctly displays the report count because the stats endpoint uses SQL `COUNT()` which bypasses the broken serializer.

To consolidate infrastructure, ensure better file integrity, and permanently resolve the serialization bug, we are migrating all file storage from Cloudinary to AWS S3. 

## Goals / Non-Goals

**Goals:**
- Completely remove `cloudinary` and `CloudinaryField` dependencies from the codebase.
- Replace all usages with Django's native `FileField` or `ImageField`.
- Create a data migration script to download all existing files from Cloudinary and re-upload them to AWS S3.
- Update the API serializers to serve native S3 URLs.
- Fix the frontend listing bug for LP reports by removing the broken Cloudinary URL parsing logic.

**Non-Goals:**
- Changing the frontend UI components beyond any minor tweaks needed to support the new URL formats.
- Modifying the actual business logic of report creation or reviewing.

## Decisions

**Decision 1: Use `FileField` over custom S3 Fields**
- *Rationale*: Django's `FileField` automatically delegates storage operations to the configured `DEFAULT_FILE_STORAGE`. Since we already have `storages.backends.s3boto3.S3Boto3Storage` configured in `settings.py`, we simply use standard `FileField`s. This keeps models clean and decoupled from the specific storage backend.

**Decision 2: Migration Script Approach**
- *Rationale*: We will create a custom Django management command (`python manage.py migrate_cloudinary_to_s3`). The script will iterate through all instances of `DailyReportAttachment`, `AttendanceDocument`, `Asset`, `Candidate`, and `Message`, use the `requests` library to download the file from the Cloudinary URL (using the provided credentials if necessary), and save it to the new `FileField` using Django's `ContentFile`.
- *Alternatives Considered*: A manual database script or external ETL tool. A Django management command is safer, utilizes the existing ORM, and triggers the `S3Boto3Storage` backend automatically.

**Decision 3: Fix Company Filter Bug via S3 Migration**
- *Rationale*: The serialization error in `DailyReportSerializer.get_view_url` was attempting to manually manipulate `http://` strings to `https://` and use Cloudinary's specific `/upload/fl_attachment` transformation. By migrating to S3, `FileField.url` will natively return a valid, pre-signed HTTPS URL. We can completely remove the complex string manipulation, which inherently fixes the crash for LP reports.

## Risks / Trade-offs

- **Risk: Downtime during data migration** 
  - *Mitigation*: The migration script should be idempotent. It will check if the file is already migrated before attempting a download/upload to prevent duplicate work or data loss if interrupted.
- **Risk: Broken references for old files**
  - *Mitigation*: The script will download the files and save them to S3 before the `CloudinaryField` is officially removed from the database schema (we change it to `FileField` which maps to a standard `VARCHAR` in the DB, so the underlying string URL remains until overwritten by the script).

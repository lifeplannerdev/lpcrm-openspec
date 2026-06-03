## Why

The system currently relies on Cloudinary for storing file attachments (e.g., reports, HR documents), but we need to unify our storage infrastructure by migrating to AWS S3. This ensures file integrity, simplifies access control, and consolidates our cloud dependencies. Furthermore, the current integration is causing a critical bug: the "LP" reports list fails to load (returning a 500 serialization error when accessing broken Cloudinary URLs), while the stats count succeeds because it relies purely on SQL `COUNT()`. Migrating to S3 will resolve this issue.

## What Changes

- **BREAKING**: Replace all instances of `CloudinaryField` across the codebase (`reports`, `hr`, `chats`, `accounts` apps) with standard Django `FileField` or `ImageField`.
- Configure Django to use `storages.backends.s3boto3.S3Boto3Storage` for media files so that they are seamlessly served from the AWS S3 bucket.
- Create a data migration script that uses the provided Cloudinary API credentials (`682472894527882`, `XMJkAwE-LzYR1gr8tsVz6orLvOg`) to systematically download existing files from Cloudinary and upload them to the configured AWS S3 bucket.
- Update serializer `get_download_url` and `get_view_url` methods to handle S3 URLs rather than Cloudinary-specific transformations.
- Ensure the Company filter bug is fully resolved by cleaning up attachment serializers.

## Capabilities

### New Capabilities
- `attachment-storage-migration`: A data migration capability to securely transfer existing files from Cloudinary to AWS S3 while preserving file integrity and associations.

### Modified Capabilities
- `aws-infrastructure`: Expand the EC2 setup to formally integrate the AWS S3 bucket for media storage, removing any leftover Cloudinary configuration from the environment.

## Impact

- **Models**: `DailyReportAttachment`, `AttendanceDocument`, `Asset`, `Candidate`, `Message`, and any other model utilizing `CloudinaryField`.
- **APIs**: The Reports List API and view/download endpoints will serve direct S3 presigned URLs or public URLs instead of Cloudinary URLs.
- **Dependencies**: `cloudinary` package will be removed; `boto3` and `django-storages` will handle all file operations.

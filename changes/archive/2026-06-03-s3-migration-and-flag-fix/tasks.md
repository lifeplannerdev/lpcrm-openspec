## 1. Migration Script Creation

- [x] 1.1 Create `reports/management/commands/migrate_cloudinary_to_s3.py`.
- [x] 1.2 Implement the script to iterate over `DailyReportAttachment` and use the provided Cloudinary API credentials to download files via `requests`.
- [x] 1.3 Extend the script to also iterate over `AttendanceDocument`, `Asset`, `Candidate`, and `Message` models and download their respective Cloudinary files.
- [x] 1.4 Save the downloaded files to their respective `FileField` fields using Django's `ContentFile`.

## 2. Model Refactoring

- [x] 2.1 Replace `CloudinaryField` with `models.FileField` in `reports/models.py`.
- [x] 2.2 Replace `CloudinaryField` with `models.FileField` in `hr/models.py`.
- [x] 2.3 Replace `CloudinaryField` with `models.FileField` in `chats/models.py`.
- [x] 2.4 Replace `CloudinaryField` with `models.FileField` in `accounts/models.py`.
- [x] 2.5 Generate Django migrations for the model changes (`python manage.py makemigrations`).

## 3. Serializer & View Refactoring

- [x] 3.1 Update `reports/serializers.py` to remove Cloudinary-specific URL transformations in `get_download_url` and `get_view_url`.
- [x] 3.2 Update `reports/models.py` `DailyReportAttachment.get_download_url()` to return standard S3 URLs without URL replacement logic.
- [x] 3.3 Verify `reports/views.py` `DownloadAttachmentView` handles native S3 URLs gracefully.

## 4. Dependencies Cleanup

- [x] 4.1 Remove `cloudinary` from `requirements.txt`.
- [x] 4.2 Verify AWS S3 config in `settings.py` correctly uses `storages.backends.s3boto3.S3Boto3Storage` as `DEFAULT_FILE_STORAGE`.

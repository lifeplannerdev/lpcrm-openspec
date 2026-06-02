## ADDED Requirements

### Requirement: Document Attachments
The system SHALL allow users to upload and attach files (PDFs, images, docs) to a lead.

#### Scenario: Uploading a file
- **WHEN** a user uploads a file on the lead detail page
- **THEN** the system saves the file and links it to the lead via the `LeadDocument` model.

### Requirement: Mention Notifications
The system SHALL parse `@username` tags in remarks and send a notification to the tagged user.

#### Scenario: Mentioning a user in a remark
- **WHEN** a user saves a remark containing `@john`
- **THEN** the system identifies the user `john` and creates a notification alerting him to the lead.

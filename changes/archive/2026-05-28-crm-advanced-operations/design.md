## Context

The CRM is scaling and taking on advanced operational workflows. Integrations with Voxbay (call logs) and Meta Ads (lead ingestion) are necessary to remove data entry lag. Branch management is needed to split data functionally (e.g. Kochi vs Kottayam). UI elements are expanding to support more complex academic grading, attendance, and reporting.

## Goals / Non-Goals

**Goals:**
- Ingest leads from Meta Ads into the CRM in real-time via webhooks.
- Provide a webhook receiver for Voxbay call data to automatically spawn follow-up tasks and support 1-click lead conversion.
- Implement the `Branch` model and assign trainers and students to specific branches for isolated data viewing.
- Support robust multi-date filtering on tasks and reports, and allow CSV/PDF downloads of the filtered views.
- Extend `AcademicBatch` logic to capture Marks Achieved via an `ExamResult` model.

**Non-Goals:**
- Creating a full two-way chat dialer for Voxbay (this focuses on ingestion and lead creation only).
- Creating complex statistical reporting for marks (just capturing them for now).

## Decisions

**1. Integration Webhooks (Django DRF vs Third-party Middleware)**
*Decision*: Use Django DRF to host custom webhook endpoints (`/api/webhooks/voxbay/` and `/api/webhooks/meta/`). 
*Rationale*: Using a middleware like Zapier costs money at scale. By exposing our own webhook endpoint, Meta and Voxbay can POST data directly to the CRM, and we can validate the payload synchronously and instantly create tasks/leads.

**2. Branch Implementation (Enum vs Model)**
*Decision*: Create a `Branch` Django model.
*Rationale*: While an enum (Choices) is simple, a model allows scaling (e.g. adding branch address, manager, phone number). Trainers and Students will gain a `ForeignKey(Branch)` field.

**3. Exam Marks (Where to store them)**
*Decision*: Create an `ExamResult` model referencing `Student` and `AcademicBatch`.
*Rationale*: A student takes multiple exams, and a batch has multiple students taking the same exam. A junction model (`ExamResult`) scales perfectly for this Many-to-Many relationship with extra data (the score).

**4. Data Exports (Frontend vs Backend)**
*Decision*: Frontend generation (using libraries like `xlsx` and `jspdf`/`html2pdf`).
*Rationale*: Since the data is already fetched via API and rendered in a React table based on complex client-side filters, it is much easier and faster to export the JSON payload on the frontend into a CSV/PDF than sending the exact filter state back to the backend to generate the file.

## Risks / Trade-offs

- **Risk: Webhook Security** -> *Mitigation*: Secure webhook endpoints with signature validation (Meta requires verifying a hub challenge and checking the SHA256 signature).
- **Risk: Filter Performance** -> *Mitigation*: Ensure Django ORM filters on fields like `date` or `branch` are indexed in the database to keep queries fast as the table grows.
- **Risk: Legacy Data Migration** -> *Mitigation*: The `Branch` foreign key on Students must be nullable initially. We can bulk update existing records to a default branch if necessary.

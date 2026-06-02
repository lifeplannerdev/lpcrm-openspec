## ADDED Requirements

### Requirement: Extend Lead Model for Marketing
The system SHALL extend the existing CRM Lead model to include marketing data fields.

#### Scenario: Storing marketing properties
- **WHEN** a lead is created from an Ad source
- **THEN** the system must store `campaign_name`, `adset_name`, `ad_name`, `meta_lead_id`, and `raw_form_data` correctly

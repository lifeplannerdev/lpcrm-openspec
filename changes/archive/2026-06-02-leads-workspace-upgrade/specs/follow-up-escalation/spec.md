## ADDED Requirements

### Requirement: Overdue Follow-up Notification
The system SHALL automatically notify the assigned owner if a follow-up is not marked as completed within 24 hours of its scheduled time.

#### Scenario: 24-hour escalation
- **WHEN** a follow-up is 24 hours past its `follow_up_time` and status is not Completed
- **THEN** the system generates a Notification for the `assigned_to` user.

### Requirement: Overdue Follow-up Reassignment
The system SHALL automatically reassign a lead to a manager or pool if a follow-up is overdue by 72 hours.

#### Scenario: 72-hour escalation
- **WHEN** a follow-up is 72 hours past its `follow_up_time` and status is not Completed
- **THEN** the system reassigns the lead and creates a `LeadAssignment` log.

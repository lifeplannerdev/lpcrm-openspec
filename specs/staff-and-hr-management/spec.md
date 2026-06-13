## Purpose
Unified specification for staff-and-hr-management.

## Requirements

**Subdomain:** staff-management

### Requirement: Staff Soft Deletion Only
The system SHALL NOT permit the hard deletion of staff records under any circumstances from the user interface. Staff records can only be soft-deleted by toggling their `is_active` status to false.

#### Scenario: User attempts to delete a staff member
- **WHEN** a user looks for a delete option on a staff member's record
- **THEN** no delete button is available in the UI
- **AND** the user can only deactivate the staff member using the "Active Status" toggle

### Requirement: Premium Staff Management UI
The Staff Management UI SHALL employ premium visual design standards, including dynamic hover states, soft rounded corners, glassmorphism accents, and highly structured, clean forms.

#### Scenario: Viewing the staff grid
- **WHEN** a user visits the Staff Management page
- **THEN** the grid displays highly optimized, visually premium cards with clear status indicators and action buttons

### Requirement: Display Attached Assets on Staff Profile
The system SHALL display all assets currently assigned to a staff member on their individual Staff Details page, providing a clear list of what company property they currently hold.

#### Scenario: Viewing a staff profile with assigned assets
- **WHEN** an admin views the detailed profile of a staff member who holds a laptop
- **THEN** the profile shows an "Attached Assets" section listing the laptop and its details.

### Requirement: Asset Permission Assignment
The Staff Permission Assign Screen SHALL list the new Asset Management permissions (`view_asset`, `manage_asset`) allowing admins to grant specific staff access to the Asset Management feature.

#### Scenario: Granting asset management permissions
- **WHEN** an admin edits the permissions of an IT staff member
- **THEN** they can select the "Manage Assets" permission flag, saving the setting successfully.


### Requirement: Tabbed Status Filtering for Staff
The system SHALL present staff members in a tabbed UI to clearly separate them by status (All Staff, Active, Inactive, On Leave), ensuring soft-deleted (inactive) users remain accessible for data integrity.

#### Scenario: User views inactive staff
- **WHEN** the user switches to the "Inactive" tab on the Staff page
- **THEN** the grid only displays staff members whose status is Inactive

### Requirement: Staff On Leave Status
The system SHALL support tracking and filtering staff members who are on leave.

#### Scenario: Filtering by On Leave Status
- **WHEN** an admin selects the "On Leave" tab on the Staff Management page
- **THEN** the system fetches and displays only staff members who have their on-leave status set to true

#### Scenario: Staff Statistics Include On Leave Count
- **WHEN** the Staff Management page loads
- **THEN** the statistics cards display the correct count of staff members who are on leave


**Subdomain:** reports-and-exports

### Requirement: Daily Reporting System
The system SHALL provide a Daily Reporting feature allowing employees to submit daily status updates (Morning Agenda and Evening Report) and review their past reports.
The system SHALL track completion as a 2-step process per day (50% for Agenda, 100% for Report).
The system SHALL support auto-carryover of agendas: if an employee submits "Next Day's Agenda", the system SHALL automatically populate the "Morning Agenda" for the following day.

#### Scenario: Employee submits a report
- **WHEN** an employee fills out the Daily Report form and submits it
- **THEN** the report is saved as "pending" for manager review

#### Scenario: Agenda Auto-Carryover
- **WHEN** an employee submits the "Next Day's Agenda" field on Monday evening
- **THEN** their Tuesday report is automatically initialized with the "Morning Agenda" field populated, marking that step as complete.

### Requirement: Policy-Driven Report Timelines
The system SHALL allow administrators to configure specific Report and Agenda deadlines per employee, along with the policy for *when* the Agenda is due (e.g., `EVENING_BEFORE` or `MORNING_OF`).

#### Scenario: Admin configures employee timeline
- **WHEN** an admin sets User A's agenda policy to `MORNING_OF` with a deadline of 10:00 AM
- **THEN** the system expects User A to submit their Morning Agenda on the current day before 10:00 AM.

### Requirement: Granular Lateness Tracking and Filtering
The system SHALL track exact submission timestamps for both the Agenda and the Report independently.
The system SHALL calculate lateness flags (`Late Agenda`, `Late Report`, `On-Time`, `Incomplete`) by comparing the independent submission timestamps against the employee's configured deadlines.

#### Scenario: Late Agenda submission
- **WHEN** an employee submits their Morning Agenda after their configured deadline
- **THEN** the system applies a `Late Agenda` flag to that day's report, even if they submit their Evening Report on time.

#### Scenario: Filtering by granular flags
- **WHEN** an HR user views the Admin Reports page and filters by `Late Agenda`
- **THEN** the frontend requests and displays only reports where the `Late Agenda` flag is active.

### Requirement: Multi-Parameter Report Filtering
The system SHALL support filtering reports simultaneously by Employee, Date, Status, and Search Keyword on the backend list APIs.

#### Scenario: Aggregating End-of-Day HR Reports
- **WHEN** an HR user selects "Today" for date, a specific "Employee" from the dropdown, and searches for a specific string
- **THEN** the backend accurately returns the intersection (AND) of all those applied filters, fetching only that employee's reports submitted today that match the keyword.

### Requirement: Employee Filtering Dropdown
The frontend Reports pages SHALL display an Employee filter dropdown populated with active employees.

#### Scenario: Select an Employee
- **WHEN** the user selects an employee from the dropdown
- **THEN** the frontend triggers a network request to the backend appending `employee_id=<id>` (or `user=<id>`) to the query parameters.

### Requirement: Correct Currency Symbol for Penalties
The system SHALL use the Indian Rupee symbol (₹) instead of the Dollar sign ($) for penalty amounts.

#### Scenario: Viewing a Penalty
- **WHEN** the user views the Penalty Management page
- **THEN** they see the amounts prefixed or labeled with `₹` rather than `$`.

### Requirement: Data Exports
The system SHALL provide functionality for authorized users to export specific datasets (e.g. leads, tasks, attendance) to CSV or Excel formats.

#### Scenario: Exporting filtered data
- **WHEN** a user clicks the "Export" button on a list view
- **THEN** the system generates and downloads a file containing the data currently matching their applied filters.


**Subdomain:** asset-management

### Requirement: Asset Tracking Model
The system SHALL track physical and digital assets with details including name, category, serial number/IMEI, status, company affiliation, assignment to a User OR a Location, and a photo/invoice attachment.

#### Scenario: Creating a new asset
- **WHEN** an admin creates a new asset record
- **THEN** the system stores the asset details and associates it with the specified company and optionally a staff member or a physical location.

### Requirement: Multi-Tenant Asset Filtering
The Asset Management UI SHALL display assets segregated by company (LP vs FLAG) using tabbed views or optimized filtering to ensure strict data separation based on the viewing admin's access.

#### Scenario: Viewing assets for LP company
- **WHEN** an admin clicks the "LP" tab on the Asset Management page
- **THEN** the system fetches and displays only assets where `company == 'LP'`.

### Requirement: Asset Assignment and Status
The system SHALL allow updating the status of an asset (Available, Assigned, Maintenance, Retired) and tracking its current assignee.

#### Scenario: Assigning an asset to a staff member
- **WHEN** an admin assigns an available laptop to "John Doe"
- **THEN** the system sets the asset's assigned_to field to John Doe and its status to 'Assigned'.

### Requirement: Premium Asset UI
The Asset Management page SHALL follow the premium UI guidelines, offering a dynamic, visually appealing grid or table with glassmorphism elements, micro-animations, and clear status indicators.

#### Scenario: Navigating the asset inventory
- **WHEN** the user browses the asset inventory
- **THEN** they see an engaging, responsive interface with hover effects and clear typography.



### Requirement: Dynamic IMEI Labeling
The system SHALL dynamically change the UI label for the hardware identifier field based on the selected asset type.

#### Scenario: Selecting Mobile Asset Type
- **WHEN** a user selects "Mobiles" from the Asset Type dropdown
- **THEN** the label for the hardware identifier field changes from "Serial Number" to "IMEI Number"

#### Scenario: Selecting Non-Mobile Asset Type
- **WHEN** a user selects "Laptops" from the Asset Type dropdown
- **THEN** the label for the hardware identifier field remains "Serial Number"

### Requirement: Attach Asset to Parent Asset
The system SHALL allow an asset (such as a SIM card) to be attached to a parent asset (such as a Mobile phone).

#### Scenario: Attaching a SIM to a Mobile
- **WHEN** a user creates or edits an asset of type "SIM" and selects a "Mobile" from the Parent Asset dropdown
- **THEN** the SIM is saved with the Mobile as its `parent_asset`

### Requirement: Inherit Assigned User from Parent
The system SHALL enforce that any asset attached to a parent asset inherits the `assigned_to` property of its parent.

#### Scenario: Syncing Assignment on Attachment
- **WHEN** an unassigned SIM is attached to a Mobile assigned to User A
- **THEN** the SIM's `assigned_to` field is automatically set to User A

#### Scenario: Syncing Assignment on Parent Update
- **WHEN** a Mobile with an attached SIM is reassigned from User A to User B
- **THEN** the attached SIM's `assigned_to` field is automatically updated to User B




 
  
 T h e   s y s t e m   S H A L L   s u p p o r t   a   d y n a m i c   A s s e t C a t e g o r y   m o d e l ,   a l l o w i n g   a d m i n i s t r a t o r s   t o   a d d ,   e d i t ,   o r   r e m o v e   a s s e t   c a t e g o r i e s   ( e . g . ,   ' T e a p o y ' ,   ' W a s t e   B i n ' ,   ' A C ' )   w i t h o u t   c o d e   c h a n g e s .  
  
 -   * * W H E N * *   a n   a d m i n   a d d s   " T e a p o y "   t o   t h e   A s s e t   C a t e g o r i e s  
 -   * * T H E N * *   " T e a p o y "   i m m e d i a t e l y   b e c o m e s   a v a i l a b l e   i n   t h e   C a t e g o r y   d r o p d o w n   w h e n   c r e a t i n g   a   n e w   a s s e t  
  
 T h e   s y s t e m   S H A L L   s u p p o r t   s t o r i n g   p r i m a r y   a n d   s e c o n d a r y   p h o n e   n u m b e r s   d i r e c t l y   o n   M o b i l e   a s s e t s   t o   f l a t t e n   d a t a   e n t r y .  
  
 -   * * W H E N * *   a   u s e r   c r e a t e s   a n   a s s e t   w i t h   a   c a t e g o r y   o f   ' M o b i l e s '  
 -   * * T H E N * *   t h e   f o r m   d y n a m i c a l l y   s h o w s   ` P r i m a r y   P h o n e   N u m b e r `   a n d   ` S e c o n d a r y   P h o n e   N u m b e r `   f i e l d s ,   w h i c h   a r e   s a v e d   d i r e c t l y   t o   t h e   a s s e t   r e c o r d  
  
 T h e   s y s t e m   S H A L L   s u p p o r t   t h e   c r e a t i o n   a n d   m a n a g e m e n t   o f   p h y s i c a l   L o c a t i o n s   ( e . g . ,   " R e c e p t i o n   1 " ,   " C a b i n   3 " ,   " M D   C a b i n " )   t o   w h i c h   a s s e t s   c a n   b e   a s s i g n e d .  
  
 -   * * W H E N * *   a n   a d m i n   n a v i g a t e s   t o   S p a c e   M a n a g e m e n t   a n d   c r e a t e s   a   n e w   L o c a t i o n   n a m e d   " C a b i n   1 "  
 -   * * T H E N * *   t h e   l o c a t i o n   i s   s a v e d   a n d   b e c o m e s   a v a i l a b l e   a s   a n   a s s i g n m e n t   t a r g e t   f o r   a s s e t s  
  
 T h e   s y s t e m   S H A L L   a l l o w   a n   a s s e t   t o   b e   a s s i g n e d   d i r e c t l y   t o   a   L o c a t i o n ,   i n d i c a t i n g   i t   i s   a n   o f f i c e   f i x t u r e   ( e . g . ,   A C ,   F a n ,   S o f a )   r a t h e r   t h a n   a   p e r s o n a l   a s s i g n m e n t .  
  
 -   * * W H E N * *   a n   a d m i n   e d i t s   a n   A C   a s s e t   a n d   s e l e c t s   " C a b i n   3 "   a s   t h e   l o c a t i o n  
 -   * * T H E N * *   t h e   a s s e t ' s   a s s i g n e d _ l o c a t i o n   i s   u p d a t e d   a n d   a s s i g n e d _ t o   ( U s e r )   i s   c l e a r e d  
  
 T h e   s y s t e m   S H A L L   p r o v i d e   a   S p a c e   I n v e n t o r y   D a s h b o a r d   t h a t   v i s u a l i z e s   t h e   o f f i c e   s p a t i a l l y ,   s h o w i n g   a   c a r d   f o r   e a c h   L o c a t i o n ,   s u m m a r i z i n g   t h e   o c c u p a n t   a n d   t h e   a s s e t s   w i t h i n   i t .  
  
 -   * * W H E N * *   a n   a d m i n   v i s i t s   t h e   S p a c e   I n v e n t o r y   p a g e  
 -   * * T H E N * *   t h e y   s e e   c a r d s   f o r   " R e c e p t i o n " ,   " C a b i n   1 " ,   e t c . ,   w i t h   s u m m a r i z e d   i c o n s   f o r   D e s k t o p   S y s t e m s ,   C h a i r s ,   a n d   A C s   p r e s e n t   i n   e a c h   l o c a t i o n  
 
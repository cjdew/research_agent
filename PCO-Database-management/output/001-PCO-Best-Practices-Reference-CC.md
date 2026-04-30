# Claude Code - PCO Database Management Best Practices Reference

> **Compiled:** April 15, 2026
> **Scope:** Planning Center Online database management across all modules
> **Sources:** PCO official documentation, church technology consultants, nonprofit CRM research

---

## 1. Data Entry Standards

### Naming Conventions
- Establish a written standard for name formatting: first names as given (not nicknames unless preferred name field is used), consistent capitalization, no unnecessary abbreviations.
- Decide upfront how to handle formal names vs. nicknames. PCO supports a "nickname" field — use it rather than overwriting the first name field.
- Avoid all-caps or all-lowercase entries. Clean My PCO (integration) can auto-correct capitalization issues.

**Sources:** [Humanitru — Data Hygiene Tips](https://www.humanitru.com/14-data-hygiene-tips-for-nonprofits/), [NPO Info — Data Hygiene Guide](https://npoinfo.com/nonprofit-data-hygiene/), [Clean My PCO](https://cleanmypco.com/)

### Address Formatting
- Standardize abbreviations: pick either "Street" or "St.", "Drive" or "Dr.", "Road" or "Rd." and enforce consistently. Best practice: use USPS-standard abbreviations (St, Dr, Rd, Ave, Blvd).
- Use full 9-digit ZIP+4 when available for mail deliverability.
- Validate addresses against postal databases (Clean My PCO does this automatically for subscribers).
- Avoid storing duplicate addresses on the same profile.

**Sources:** [Clean My PCO](https://cleanmypco.com/), [Bloomerang — CRM Cleanup Tasks](https://bloomerang.com/blog/crm-cleanup-tasks-for-donor-data/)

### Phone Number Formatting
- Store in a consistent format. PCO normalizes phone numbers, but verify entries aren't using phone numbers as login identifiers (which prevents email-based login).
- Avoid copying parent phone numbers onto children's profiles — this causes duplicate communication.

### Email Management
- Validate email addresses at point of entry where possible.
- Process bounced/blocked emails weekly. Create a list for blocked email addresses and work through them.
- Use email (not phone) as the primary login identifier to enable Church Center access and self-service profile updates.
- Clean My PCO can auto-verify email deliverability.

**Sources:** [ChurchTechToday — 5 PCO Cleanup Tips](https://churchtechtoday.com/planning-center-clean-up/), [Bloomerang — CRM Cleanup Tasks](https://bloomerang.com/blog/crm-cleanup-tasks-for-donor-data/)

---

## 2. Membership Status Taxonomy

### Design Principles
- Keep the taxonomy simple: no more than 5-7 status categories. If a person could fit multiple categories, the definitions are too broad.
- Write a one-paragraph definition for each status and distribute to all staff with data entry access.
- Every person in the database should have a status assigned. "None" or blank should not be the default for anyone who has attended.

### Recommended Categories
Industry consensus across church management platforms suggests these core statuses:

| Status             | Definition                                             |
| ------------------ | ------------------------------------------------------ |
| **Attender**       | Regularly attends (3+ times in last quarter)           |
| **Member/Partner** | Has completed formal membership process                |
| **Visitor/Guest**  | First-time or infrequent visitor (fewer than 3 visits) |
| **Inactive**       | No attendance or engagement in 6+ months               |
| **Deceased**       | Record preserved for historical/giving purposes        |

- Review status assignments quarterly using automated lists.
- Children should inherit a status appropriate to their engagement (typically matches parents' status), not be left as "None."

**Sources:** [ChurchTrac — Member Status](https://www.churchtrac.com/support/people/member-status), [Fellowship One — Managing Statuses](https://help.fellowshipone.com/Content/People Management/People Administration/Managing Statuses.htm), [ChurchTechToday — 5 PCO Cleanup Tips](https://churchtechtoday.com/planning-center-clean-up/)

---

## 3. Duplicate Detection & Merging

### Prevention
- Enable PCO's built-in Duplicate Detector. It compares names (including nicknames and sound-alike matching), birthdays, and contact information.
- Configure form submissions and Church Center signups to check against existing profiles before creating new ones.
- Train staff and volunteers on checking for existing profiles before manual entry.

### Detection
- Run the Duplicate Detector review weekly. PCO's system has merged over 500,000 profiles and identifies 36% more duplicates than earlier versions with 20% fewer false positives.
- Supplement with manual searches for common last names and similar entries.
- Create a "potential duplicates" list for edge cases that need human review.

### Merging
- Merging in PCO is **irreversible** — always review before merging.
- When merging, all data is retained from both profiles: contact info, giving history, group memberships, attendance, registrations, and recurring donations.
- Designate one "primary" profile (typically the one with more complete data or more recent activity).
- After merging, verify household assignments are still correct.

**Sources:** [PCO — Duplicate Detector](https://planning.center/2018/duplicate-detector), [PCO — Prevent Duplicate Profiles](https://pcopeople.zendesk.com/hc/en-us/articles/360051926993-Prevent-duplicate-profiles), [RT Dynamic — CRM Deduplication Guide](https://www.rtdynamic.com/blog/crm-deduplication-guide-2025/)

---

## 4. Household Management

### Structure
- Every person should belong to a household. Single adults get their own household.
- Set a primary contact for each household — this is the person who receives household-level communications.
- Household names should reflect the family unit. PCO auto-generates these, but review for accuracy after merges.

### Common Issues
- Children accidentally creating new households via form submissions or Church Center signups.
- Blended families requiring intentional household naming (legitimate — don't flag mismatched last names without context).
- Inactive members sitting in active households (e.g., adult children who have moved away).
- Duplicate households created by form submissions — delete the duplicate household (not the person).

### Maintenance
- Review households quarterly for orphaned single-person households that should be merged.
- Check that household member addresses match (flag out-of-state addresses for review — may indicate a member who has moved).
- Verify primary contacts are set appropriately (adults, not children).

**Sources:** [PCO — Households](https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households), [Threefold Solutions — PCO Database Guide](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)

---

## 5. Custom Fields & Tabs

### Organization Principles
- Group related fields into purpose-specific tabs (e.g., "Volunteer Info," "Discipleship," "Giving Analytics").
- Use descriptive, consistent naming for both tabs and fields. Avoid abbreviations that are unclear to new staff.
- Use headings within tabs to organize sections.
- Limit the number of custom fields to what is actively used. Every field should have a clear purpose tied to a ministry or operational need.

### Field Types
- Use the most specific field type available (dropdown > free text for categorical data, date picker > text for dates, checkboxes for multi-select).
- Dropdowns enforce consistency better than free text for categorical data.

### Integration-Managed Fields
- Fields populated by third-party integrations (e.g., MortarStone, Parable, PastorsLine) should be clearly separated into their own tabs.
- Do not manually edit integration-managed fields — changes will be overwritten.
- Audit integration tabs periodically for stale or orphaned data.

### Lifecycle
- Archive or remove custom fields and tabs that are no longer actively used (e.g., completed campaigns).
- Before removing, export the data if it has historical value.
- Avoid creating fields that duplicate PCO's built-in functionality (e.g., a custom "Household Name" field when PCO has built-in household management).

### Permissions
- Set appropriate view/edit permissions per tab using PCO's collaborator settings.
- Only managers should create or modify custom field definitions.

**Sources:** [PCO — Manage Custom Fields](https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Manage-custom-fields), [Threefold Solutions — PCO Database Guide](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)

---

## 6. Lists & Automations

### Purpose
Lists are PCO's primary tool for segmentation, reporting, and ongoing data hygiene. They can be rule-based (auto-updating) or static.

### Maintenance Lists (recommended)
Create standing lists for ongoing data quality monitoring:
- Missing email addresses
- Missing phone numbers
- Missing gender or birthdate
- Missing membership status
- Blocked email addresses
- Children marked as household primary
- Background checks expiring within 30 days
- Inactive profiles (no activity in 6+ months)
- Volunteers without recent service activity
- Records missing campus assignment

### Naming & Organization
- Use a consistent naming convention (e.g., prefix with category: "DQ: Missing Email," "Vol: Inactive Volunteers").
- Star actively-used lists for quick access.
- Review and archive/delete unused lists quarterly.

### Automations
- Use list automations to trigger workflows, update fields, or send notifications.
- Review automations quarterly to ensure they're still relevant and not producing false results.
- Paused automations should be either reactivated or removed — don't let them accumulate.

**Sources:** [PCO — List Automation](https://planning.center/2016/list-automations/), [ChurchTechToday — 5 PCO Cleanup Tips](https://churchtechtoday.com/planning-center-clean-up/), [Threefold Solutions — PCO Database Guide](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)

---

## 7. Workflows

### Design Principles
- Each workflow should have a single, clear purpose. Avoid combining unrelated processes into one workflow.
- Name workflows descriptively: "New Visitor Follow-Up" not "Follow Up."
- Organize workflows into categories that match ministry areas.

### Maintenance
- Review all workflows monthly for overdue cards, stalled processes, and unassigned steps.
- Archive completed or obsolete workflows rather than deleting them (preserves history).
- Assign a responsible person (not just a role) to each workflow step.
- Use bulk updates to manage workflow cards efficiently.

### Health Indicators
- High card counts with many overdue items = stalled workflow needing attention.
- Unassigned cards = missing process owner.
- Ready-but-unacted cards = bottleneck or abandoned workflow.

**Sources:** [PCO — Bulk Updates to Workflows](https://planning.center/2018/bulk-updates), [ChurchTechToday — 5 PCO Cleanup Tips](https://churchtechtoday.com/planning-center-clean-up/)

---

## 8. Forms

### Design
- Each form should have a clear, descriptive name indicating its purpose and (if applicable) date/season.
- Only collect information you will actively use. Over-asking creates friction and incomplete submissions.
- Link form fields to PCO profile fields where possible to auto-populate data.

### Lifecycle Management
- Close forms after their event/purpose has ended.
- Archive old forms quarterly (preserves submission data while removing from active view).
- Review active forms for relevance — if a form hasn't received submissions in 3+ months, evaluate whether it should be closed.

**Sources:** [Threefold Solutions — PCO Database Guide](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)

---

## 9. Volunteer Management

### Database Tracking
- Use PCO Services for scheduling and position tracking (this is the system of record for who is serving where and when).
- Avoid dual-tracking volunteers in both Services teams AND custom fields — this creates data drift. Pick one source of truth.
- Track volunteer status (active, on break, retired) to maintain accurate rosters.
- Background check status and expiration should be tracked and monitored with automated lists.

### Data Freshness
- Review team rosters quarterly. Remove people who are no longer serving.
- Verify contact preferences and availability are current.
- Track orientation and training completion dates with expiration alerts where applicable.

**Sources:** [PCO — Services](https://planning.center/services/), [Threefold Solutions — PCO Database Guide](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database), [Vanco — Church Volunteer Management](https://www.vancopayments.com/egiving/blog/church-volunteer-management)

---

## 10. Giving Data Management

### Fund Structure
- Keep fund names clear, descriptive, and non-duplicated.
- Deactivate funds that are no longer accepting donations.
- Use separate funds for distinct purposes (general, missions, building, benevolence) rather than catch-all categories.

### Batch Discipline
- Every donation should be part of a batch for audit trails and reconciliation.
- Process and close batches in a timely manner (weekly or after each service).

### Donor Records
- Ensure all donor records are linked to People profiles. Unlinked donors create orphaned giving data.
- Match anonymous donations to known profiles where possible.
- Reconcile giving data with external accounting systems (e.g., QuickBooks) at least monthly.

### Statement Readiness
- Maintain clean giving data year-round to simplify year-end statement generation.
- Verify donor addresses before statement mailing season.

**Sources:** [PCO — Giving](https://planning.center/giving/), [PCO — Manage Donors](https://pcogiving.zendesk.com/hc/en-us/articles/360011867633-Manage-donors)

---

## 11. Check-Ins

### Configuration
- Check-in events should match current service times and programs. Remove or archive events that no longer occur.
- Location hierarchy should reflect actual physical spaces.
- Security codes should be enabled for children's check-in.
- Label templates should be configured per age group/environment with relevant information (allergies, special notes, security code).

### Grade/Age Promotion
- Configure grade promotions annually. Set the promotion date and verify the schedule.
- Review age-group boundaries to ensure children are in appropriate environments.

### Maintenance
- Archive inactive events and locations to reduce clutter.
- Verify station configurations match current hardware/device deployment.

**Sources:** [PCO — Check-Ins](https://planning.center/check-ins/)

---

## 12. Groups

### Organization
- Use group types to categorize (small groups, classes, ministry teams, etc.).
- Tag groups consistently for reporting and filtering.
- Every active group should have at least one designated leader.

### Enrollment & Attendance
- Set enrollment status intentionally (open/closed/request-to-join) for each group.
- Track attendance to identify disengaged members and groups that may need support.
- Review group membership quarterly — remove members who have left the group.

### Maintenance
- Archive groups that are no longer meeting.
- Verify location data for in-person groups.

**Sources:** [PCO — Groups](https://planning.center/groups/)

---

## 13. Calendar & Registrations

### Calendar
- All recurring events should be managed in PCO Calendar, not just one-offs.
- Assign resources (rooms, equipment) to events to prevent scheduling conflicts.
- Set up approval workflows for resource requests.
- Archive past events to keep the calendar clean.

### Registrations
- Link registrant records to People profiles.
- Close registrations after events conclude.
- Archive completed events.
- Reconcile payments for paid registrations.
- Manage waitlists actively — don't let them grow stale.

**Sources:** [PCO — Calendar](https://planning.center/resources), [PCO — Registrations](https://planning.center/registrations)

---

## 14. Database Maintenance Cadence

### Recommended Schedule

| Frequency                | Tasks                                                                                                                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Weekly** (30-45 min)   | Review duplicate detector, process email bounces, scan new profiles for completeness, review workflow cards                                                                     |
| **Monthly** (2-3 hours)  | Audit naming conventions, standardize addresses, review list freshness, check workflow health, verify volunteer rosters                                                         |
| **Quarterly** (half day) | Archive old forms/events, review custom field usage, audit household structure, run comprehensive duplicate scan, review membership statuses, assess integration data freshness |
| **Annually**             | Full database audit, grade promotions, giving statement preparation, review data retention/privacy policies, train new staff on data standards                                  |

### Team Structure
- Designate 2-3 "PCO Champions" across staff rather than centralizing in one person.
- Assign specific database areas to specific owners (e.g., children's director owns Check-Ins data quality, worship director owns Services data quality).
- Create documentation for data entry standards and onboard new staff.

**Sources:** [Threefold Solutions — PCO Database Guide](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database), [Bloomerang — CRM Cleanup Tasks](https://bloomerang.com/blog/crm-cleanup-tasks-for-donor-data/), [Humanitru — Data Hygiene Tips](https://www.humanitru.com/14-data-hygiene-tips-for-nonprofits/)

---

## 15. Data Privacy & Retention

### Principles
- Only collect personal information you have a clear purpose for.
- Separate sensitive data (background checks, medical notes, financial information) into appropriate access-controlled areas.
- Religious affiliation is considered "special category" data under GDPR and similar frameworks — treat it with elevated care.
- Establish a data retention policy: how long do you keep records for inactive people? Industry guidance suggests reviewing inactive records after 2 years and archiving or removing after 5 years (unless giving history requires longer retention for tax purposes).

### Access Control
- Use PCO's role-based permissions to limit who can view and edit sensitive fields.
- Audit user permissions periodically — remove access for former staff/volunteers promptly.
- Avoid sharing login credentials.

### Integration Security
- Review third-party integration access periodically.
- Ensure integrations follow the principle of least privilege — only grant access to the data they need.

**Sources:** [VinciWorks — Data Protection for Churches](https://vinciworks.com/blog/data-protection-for-churches/), [Planning Center — Security](https://planning.center/security/response), [Planning Center — Privacy](https://planning.center/privacy)

---

## 16. Cross-Module Data Integrity

### Integration Flow
PCO's modules share a common People database. Maintaining integrity means:
- All module-specific records (group members, volunteers, donors, registrants, check-in attendees) should link back to a People profile.
- Orphaned records in any module indicate a data integrity issue.
- When merging duplicates in People, verify the merge propagated correctly to all modules.

### Key Integration Points
| From      | To            | What Flows                                                     |
| --------- | ------------- | -------------------------------------------------------------- |
| People    | Groups        | Member profiles, contact info                                  |
| People    | Services      | Volunteer profiles, contact info, availability                 |
| People    | Check-Ins     | Attendee profiles, family relationships, medical/allergy notes |
| People    | Giving        | Donor profiles, addresses (for statements)                     |
| People    | Registrations | Registrant profiles, contact info                              |
| People    | Calendar      | Event ownership, resource management                           |
| Check-Ins | People        | Attendance history, first-visit tracking                       |
| Giving    | People        | Donation history, recurring giving status                      |
| Forms     | People        | Profile updates, custom field data                             |

### Monitoring
- Periodically check each module for records not linked to People profiles.
- After bulk operations (imports, merges, deactivations), verify cross-module consistency.

**Sources:** [PCO — Developer Documentation](https://developer.planning.center/docs/), [PCO — Church Management System Overview](https://planning.center/use-cases/chms)

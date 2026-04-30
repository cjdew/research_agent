# PCO Database Audit — Local Settings (Mosaic Wadsworth)

## Organization
- **Church name:** Mosaic Church (Mosaic Wadsworth)
- **Location:** Wadsworth / Canton area, Northeast Ohio
- **Campus count:** 1 (single campus)
- **Approximate database size:** 53 people in staff/household sample; full database size TBD on first audit run
- **PCO subscription tier:** [UPDATE — Church Center, basic, etc.]

## Staff Roster (12 staff across 11 households)
- Chris Dewar (Site Admin, Acct Admin) — COO & interim Ministry Pastor
- Adam Barton (Site Admin, Acct Admin) — Lead/Vision Pastor
- Jonathan Swaney (Site Admin, Acct Admin)
- Lauren DeShon (Site Admin) — also has admin account (135237809, kids@mosaicwadsworth.com)
- Nicole Ball (Site Admin)
- Julianna Palitto (Site Admin) — login is personal Gmail, not @mosaicwadsworth.com
- Alyssa Shafer (Site Admin)
- Jen Dawson (Site Admin)
- Joe Bennett
- Stephanie Erbrick
- Adam Erbrick
- Mary Ann Weller

## Custom Tabs on People Profiles
These are the custom tabs currently in use. The audit should inventory all fields within each tab and assess whether they're actively populated and well-organized:

- **33 Degree** — Capital campaign / giving commitment data (Support Level, Amount per Month)
- **Clean My PCO** — Data hygiene flags (e.g., Reason for Failed E-mail Verification)
- **Connections** — Follow-up tracking (Open House Attended)
- **Household Information** — Redundant household name field (may duplicate PCO built-in)
- **Military & Work** — Employment data (Work Title)
- **MortarStone** — Giving analytics integration (Gift Count, Giving Band, Total Given, Last Gift Date, Band Last Changed)
- **Mosaic Steps** — Discipleship pathway tracking (Crash Course Attended, Baptized, Date for New to Mosaic, New to Mosaic Attended)
- **Parable** — Engagement scoring integration (Engagement Tier, Warning Light)
- **PastorsLine.com (Integration)** — SMS/communication integration mapping (PastorsLine Group - List Mapping checkboxes)
- **Volunteer Info** — Extensive volunteer tracking (Current Teams, Leadership/Contractor status, Preferred Contact Method, Preferred Service Time, First time serving date, First Team Served On, Orientation dates, Shirt Size, etc.)

## Membership Status Taxonomy
Current values observed in data:
- **Attender** — Most common (used for staff and regular attendees)
- **Partner** — Used by at least one staff member (Lauren DeShon)
- **Guest** — Used for some children and at least one staff spouse (Corey Palitto)
- **None** — Default/unset, found on many children
- Note: No "Member" or "Visitor" categories observed

## Known Data Quality Patterns (from April 2026 staff audit)
These issues were identified in a 53-person sample and should be checked at database scale:

### High Severity (found in sample)
- Phone numbers used as login identifiers instead of email
- BLOCKED email addresses preventing communication
- Missing gender/birthdate on active profiles
- Children using parent contact info (causing duplicate communications)

### Medium Severity (found in sample)
- Inconsistent address formatting (Road vs Rd, Drive vs Dr, ZIP vs ZIP+4)
- Missing membership status on children (14 of 27 children = ~52%)
- Guest status on people who should be Attenders
- Duplicate phone/address entries on same profile
- Dual admin accounts without clear documentation

### Low Severity (found in sample)
- Outdated medical notes that may need review
- Shared phone numbers between inactive children and parents
- Custom field data completeness varies widely across tabs

## Integration Points
- **MortarStone** — Giving analytics (pushes data to custom fields)
- **Parable** — Engagement scoring (pushes Engagement Tier and Warning Light to custom fields)
- **PastorsLine.com** — SMS/text communication platform (syncs group/list mappings via custom checkboxes)
- **QuickBooks** — Financial/giving reconciliation
- **Church Center** — Public-facing app tied to PCO

## Service Times
- Sunday 9am
- Sunday 11am
- Thursday 6:30pm
- Midweek Days (various)

## Previous Cleanup Efforts
- April 2026: Staff & Household data audit generated (53 people, 11 households)
- "Clean My PCO" tab exists with email verification failure tracking — indicates prior cleanup effort

## Audit-Specific Notes
- The "Volunteer Info" tab is the most heavily populated custom tab — it tracks team assignments, orientation, preferences, and leadership roles. This tab likely needs the most attention for data freshness and consistency.
- MortarStone and Parable are third-party integration tabs — their data is auto-populated. Audit for orphaned/stale data but don't recommend manual edits to these fields.
- PastorsLine checkboxes contain very long group names with hashtags — may indicate auto-generated mapping that's hard to maintain manually.

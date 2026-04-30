# PCO Database Audit Findings — Mosaic Wadsworth

> **Audit Date:** April 15, 2026
> **Auditor:** Automated via PCO People MCP + PCO API
> **Organization:** Mosaic Wadsworth (ID: 87719)
> **Data Access:** Read-only audit. No records were modified.

---

## Database Overview

| Metric | Value | Source |
|--------|-------|--------|
| Organization created | September 10, 2012 | `people_organization` |
| Campus count | 1 (Mosaic: Wadsworth) | `church_campuses` |
| Church Center subdomain | mosaicwadsworth | `people_organization` |
| Total active people | 2,041 | `people_search` (status=active, per_page=1) |
| Total inactive people | 3,838 | `people_search` (status=inactive, per_page=1) |
| Active adults | 1,090 | `people_search` (status=active, age_type=adult) |
| Active children | 951 | `people_search` (status=active, age_type=child) |
| Total households | 1,122 | `people_households` (per_page=1) |
| Custom tabs | 11 | `people_tabs` |
| Custom field definitions | 111 | `people_field_definitions` |
| Total lists | 258 | `people_lists` |
| Total workflows | 24 | `people_workflows` |
| Total forms | 67 | `people_forms` |
| Note categories | 6 | `people_note_categories` |

**Inactive-to-active ratio:** 3,838 inactive vs. 2,041 active = **65% of all records are inactive.** This is high and suggests limited archival or deletion practices over the org's 13-year history.

---

## 2A — Organization & Structure Audit

### Campus Configuration

**Rating: NEEDS ATTENTION**

- Single campus: "Mosaic: Wadsworth" at 118 High St., Wadsworth, OH
- **Finding:** Campus ZIP code is set to **44821** (Attica, OH). Wadsworth, OH should be **44281**. This is a data entry error that could affect location-based features, mailing, and Church Center display.
  - **Confidence:** High. USPS confirms Wadsworth OH = 44281.
  - **Impact:** Medium. Affects campus address display in Church Center and any location-based reporting.
- Campus contact email and phone number are both null. Website is null (org-level website is set to mosaicwadsworth.com).
- Campus has no service times included in the campus record (may be configured elsewhere in Services).

### Custom Tabs Inventory

11 custom tabs in the following order:

| Seq | Tab Name | Field Count | Type | Status Assessment |
|-----|----------|-------------|------|-------------------|
| 1 | Connections | 11 | Manual — visitor/guest tracking | Active |
| 3 | Household Information | 3 | Manual — redundant | **Redundant** |
| 4 | Volunteer Info | 21 | Manual — volunteer tracking | Active, high use |
| 5 | Mosaic Steps | 8 | Manual — discipleship pathway | Active |
| 6 | PastorsLine.com (Integration) | 1 | Integration — SMS mapping | Active but messy |
| 7 | Military & Work | 3 | Manual — employment/military | Low use |
| 8 | Clean My PCO | 3 | Integration — data hygiene | Unknown activity |
| 9 | Automation | 49 | Automated — form field mapping | **Significant concern** |
| 10 | 33 Degree | 2 | Manual — capital campaign | **Review needed** |
| 11 | MortarStone | 9 | Integration — giving analytics | Active |
| 12 | Parable | 2 | Integration — engagement scoring | Active |

**Key Findings:**

1. **Automation tab (49 fields):** This is the largest tab by far. It contains individual boolean fields for every option on the Connect Card and Get Involved forms (e.g., "Connect::More Info: Kids", "Involved::Team Selection: Caffeine Bar"). This is a form-to-field mapping pattern that creates significant field proliferation. Many of these fields duplicate data already captured in the Connections and Volunteer Info tabs via checkbox fields. **Rating: AT RISK.**

2. **Household Information tab (3 fields):** Contains "Household ID" (number), "Household Name" (string), and "Household Primary Contact" (string). All three duplicate PCO's built-in household management feature. This creates a dual-tracking problem — the custom fields can drift from the built-in household data. **Rating: AT RISK.**

3. **PastorsLine.com tab (1 field, 41 checkbox options):** The single "PastorsLine Group - List Mapping" checkbox field contains 41 options with auto-generated names including hashtags, workflow references, and very long descriptive names (e.g., "People Tracked Past 12 Months - Metrics - #dailyrefresh #groups #teams #checkins #registrations #giv"). These are difficult to maintain manually and appear to be auto-generated mappings. **Rating: NEEDS ATTENTION.**

4. **33 Degree tab (2 fields):** Contains "Support Level" (select: Continue Current Giving / Increase Current Giving / Begin Giving) and "Amount per Month" (string). This appears to be a capital campaign. **Unresolved question:** Is this campaign still active? If not, the tab should be archived after exporting data. **Rating: NEEDS REVIEW.**

5. **Clean My PCO tab (3 fields):** Contains cleanup tracking fields (Date of Last Bulk Cleaning, Reason for Failed Address Verification, Reason for Failed E-mail Verification). **Unresolved question:** Is the Clean My PCO subscription still active? The "Date of Last Bulk Cleaning" field would indicate recency. **Rating: NEEDS REVIEW.**

### Field Definitions Summary

| Data Type | Count |
|-----------|-------|
| boolean | 52 |
| checkboxes | 11 |
| string | 17 |
| date | 14 |
| select | 6 |
| number | 4 |
| text | 0 |
| header | 2 |
| file | 0 |

52 of 111 fields (47%) are boolean fields, almost entirely within the Automation tab. This is an unusual pattern — booleans are typically a sign of form-to-field mapping rather than structured data design.

---

## 2B — People Data Quality Audit

### Sample Method
- **Adults:** 100 most-recently-updated active adults, pulled via `people_search` with includes for emails, phone numbers, and addresses. Sorted by `-updated_at` to capture recently-active records.
- **Children:** 50 most-recently-updated active children, same method.
- **Limitation:** This is a recency-biased sample. Stale records may show worse data quality. Database-wide counts use total_count from filtered queries.

### Membership Status Distribution (Active People)

| Membership Type | Count | % of Active |
|-----------------|-------|-------------|
| Attender | 677 | 33.2% |
| Guest | 389 | 19.1% |
| Unassigned (null) | ~895 | **43.8%** |
| Community Event Guest | 47 | 2.3% |
| Non-Attender | 16 | 0.8% |
| Partner | 15 | 0.7% |
| Business | 2 | 0.1% |

**Rating: AT RISK.**

**43.8% of active people have no membership type assigned.** This is the single most impactful data quality issue in the database. It undermines segmentation, communication targeting, follow-up workflows, and reporting accuracy.

- From list data: 874 people with "Unassigned" membership type (as of April 11, 2026 list refresh)
- 329 of those are adults, 545 are children
- The "Adults No Membership Type" cleanup list shows 430 adults (broader criteria, includes some with membership types like "Easter Registration")

**Additional observations:**
- "Easter Registration" and "Online Attender" appear as membership types in the sample but are not in the standard taxonomy — they appear to be ad-hoc additions that blur the line between membership status and engagement channel.
- "Admin Account" appears as a membership type (2 records) — this is a role, not a membership status.
- "Community Event Guest" vs. "Guest" distinction may cause confusion without clear documentation.

### Contact Information Completeness (100-Adult Sample)

| Field | Present | Missing | % Complete |
|-------|---------|---------|------------|
| Email | 96 | 4 | 96% |
| Phone | 96 | 4 | 96% |
| Address | 92 | 8 | 92% |
| Birthdate | 74 | 26 | 74% |
| Gender | 82 | 18 | 82% |

**Database-wide gender gap:** 487 active people have unspecified gender (24% of all active). **Confidence:** High (from `people_search` with gender=Unspecified).

**Blocked emails:** 2 of 108 emails in the adult sample (1.9%).

### Login Identifier Issues

- 51 of 100 sampled adults have a login identifier set.
- **8 of those 51 (16%) use a phone number instead of email.** Phone-based logins prevent Church Center access and self-service profile updates.
- **Confidence:** Medium (sample-based; database-wide rate may differ).

### Address Formatting Issues

**State field inconsistencies (from 93 addresses in sample):**

| Value | Count |
|-------|-------|
| "OH" | 87 |
| "Oh" | 2 |
| "Ohio" | 1 |
| "oh" | 1 |
| "Oh " (trailing space) | 1 |
| "OHIO " (trailing space) | 1 |

6 records use non-standard state formatting. Clean My PCO should catch these if the subscription is active. **Rating: NEEDS ATTENTION.**

**ZIP code distribution:** 38 ZIP-5 only, 54 ZIP+4. Mixed but not critical.

### Children Data Quality (50-Child Sample + Database Counts)

- **951 active children total**
- **Null membership type:** High prevalence. In the 50-child sample, the majority have null membership. Database-wide, ~545 children have no membership type.
- **Missing birthdate:** At least 2 in sample (Zachary Hale, Sabastian Hale — both have grade set but no birthdate).
- **Missing gender:** At least 1 in sample (Sophia Dougherty — grade 0, no gender set).
- **Parent contact info on children:** Multiple children in the sample have parent email/phone copied to their profile (e.g., Cooper/Earley siblings all share brook169@gmail.com and (330) 858-8785; Henricksen siblings share Ern21689@yahoo.com; Harms twins share Kharms@tkscleaning.com). This pattern causes duplicate communications when messaging by email.

**Rating: NEEDS ATTENTION.**

---

## 2C — Lists & Automation Audit

**Rating: NEEDS ATTENTION**

### Summary Metrics

| Metric | Value |
|--------|-------|
| Total lists | 258 |
| Invalid lists | At least 3 |
| Lists with automations active | 8+ |
| Starred lists | 4 (1-month lapse, 2-month lapse, 3-month lapse, 9-month auto inactivate) |
| Auto-refresh enabled | ~25 |

### Key Findings

1. **List proliferation:** 258 lists is high for a church of this size. Many appear to be one-off queries that were never archived (e.g., "Last name starts with 'Dewar' AND First name starts with 'Chris'", "Street Address contains '110' AND Street Address contains 'Over'").

2. **Duplicate lists:** At least two separate lists named "Age at least '18' 'years'" (IDs 2789816 and 2627694), both showing 567 results. At least two separate "Membership type is 'Partner'" lists (IDs 2789801 and 4951656). Multiple lists for the same "Membership type is 'Unassigned'" query (IDs 3249445, 4951659, 4951660).

3. **Invalid lists:** Three lists have `invalid: true` status:
   - "Forms Filled out form 'Mosaic Group Sign Up' since 7 days ago" — likely references a deleted/renamed form
   - "List Get Involved Initial Application Youth has been added since 7 days ago" — broken reference
   - "Forms Filled out form 'How can we pray for you?' since 7 days ago AND Membership type is 'Unassigned'" — broken reference

4. **Stale auto-refresh lists:** "Created since 1 day ago AND named attendee for a specific event '2024 - Operation Easter Basket' with a selection of 'any'" — this list auto-refreshes daily but references a 2024 event. It should be disabled.

5. **Well-organized operational lists:** The "api-Monthly Stats" series (15+ lists) and the MortarStone giving lapse lists (1/2/3 month lapse with automations) show good operational discipline. The naming convention with hashtag tags (#dailyrefresh, #weeklyrefresh, #mailchimpsync) is a strong pattern.

6. **Cleanup-focused lists exist:** "9 Month Auto Inactivate - Cleanup" (553 people), "Adults No Membership Type - Cleanup - #update #monthlyrefresh" (430 people), "Ages 4 thru 9 No Grade and No Checkins - Cleanup - #children #nightlyrefresh" (2 people). These indicate an existing cleanup practice.

---

## 2D — Workflows Audit

**Rating: AT RISK (due to "One Month Follow Up")**

### Summary

| Metric | Value |
|--------|-------|
| Total workflows | 24 |
| Active (not archived) | 21 |
| Archived | 3 |
| Uncategorized | 3 |

### Workflow Categories

| Category | Count | Workflows |
|----------|-------|-----------|
| Admin | 5 | Baptism, Compliance Review, First Time Giver, Get Involved (Serving), Interested in Small Groups, Missed Family Check-in |
| Connections | 8 | Crash Course, Curious About Jesus, First Time Card, Julianna 1st Time Cards, Missed People, New Church Center Profiles, Next Crash/Open House, One Month Follow Up |
| Get Involved | 5 | First Time Serving, New Volunteer Badge/Lanyard, Removed from Team, Volunteer Check In, zArchived Anniversary |
| Uncategorized | 3 | First Time Guests, Old Baptism Workflow, Test automation workflow |

### Critical Issues

**1. "One Month Follow Up" — CRITICAL**
- Total cards: 491
- Completed: 308
- **Overdue: 174**
- **Unassigned: 178**
- Unassigned steps: 1
- This workflow has **no assigned person for its step.** Cards are accumulating with no one responsible. 174 of those cards are overdue. This represents 174 people who were supposed to receive a follow-up and did not.

**2. "Old Baptism Workflow" — archived but not resolved**
- Archived April 13, 2025
- Still has 20 ready cards and 1 overdue card
- These represent people in a baptism process who were never moved to the new workflow or completed.

**3. Empty/unused workflows:**
- "First Time Guests" — 0 cards, 4 steps, all unassigned. Created Feb 2023, never used.
- "Missed Family Check-in" — 0 cards, 2 steps. Created Feb 2023, never used.
- "Test automation workflow" — 0 cards, 0 steps. Should be deleted.

**4. "First Time Card" — high volume, low completion rate**
- Total cards: 2,715
- Completed: 714 (26%)
- Overdue: 6
- Ready: 8
- This is the highest-volume workflow. The 26% completion rate may indicate that most cards are being snoozed or left in intermediate steps rather than completed.

**5. "Next Open House Invite List" — accumulating**
- 676 total cards, 402 completed, 70 ready
- Appears to be accumulating invitees faster than they're processed.

---

## 2E — Forms Audit

**Rating: NEEDS ATTENTION**

### Summary

| Metric | Value |
|--------|-------|
| Total forms | 67 |
| Active (not archived) | ~28 |
| Archived | ~39 |
| Forms with 0 submissions | 17 |

### Key Findings

1. **Year-specific form duplication:** Baptism application forms are created per-date with year in the name (e.g., "Baptism Application for June 2024", "Baptism Application for June 2025", "Baptism Application for June 2026"). This creates 12+ baptism forms over time. Similarly, Easter and Christmas volunteer forms are duplicated yearly. While reasonable for per-event tracking, older versions should be consistently archived.

2. **Duplicate form names:**
   - Two forms named "Blue Tip and Fireworks" (IDs 548063 and 736401)
   - Two forms named "Christmas Volunteer Form - First Impressions " (IDs 640820 and 840065)
   - Two forms named "Serving for Easter at Mosaic" (IDs 533935 and 904308)
   - Three "Household Information Update" variants (IDs 530907, 526880 — both inactive)

3. **Forms with 0 submissions that are still active:**
   - "First Step" (created July 2023, 0 submissions, still active)
   - "How can we help?" (created March 2023, 0 submissions, still active)
   - "Mosaic Group Sign Up" (created March 2023, 0 submissions, still active)
   - "Mosaic Youth Information Form" (created May 2023, 0 submissions, still active)
   - "Volunteer Info Form" (created Feb 2023, 1 submission, still active)
   - These should be reviewed and either promoted for use or closed.

4. **Well-managed forms:** Newer forms like "Get Involved Volunteer Application" (97 submissions), "Connect Form" (111 submissions), and "Get Involved Deeper Application" (53 submissions) show active use and clear naming.

---

## 2F — Households Audit

**Rating: NEEDS ATTENTION**

### Summary

| Metric | Value |
|--------|-------|
| Total households | 1,122 |
| Active adults without any household | ~303 (from list "Adults no household") |
| People in multiple households | 46 |
| Household primary contacts | 500 |

### Key Findings

1. **303 active adults have no household assignment.** This is 28% of active adults. This affects household-level communications and family grouping for Check-Ins.

2. **46 people belong to multiple households.** This can cause confusion in household-level communications and check-in. Some may be legitimate (e.g., blended families, college students), but each should be reviewed.

3. **Household-to-primary-contact ratio:** 500 primary contacts across 1,122 households means 622 households (55%) may not have a primary contact set, or the list query has additional filters. This needs verification.

---

## 2G — Custom Fields & Integration Data Audit

### Volunteer Info Tab (21 fields)

**Rating: NEEDS ATTENTION**

- "Current Teams" (checkboxes, 20 options) — This is the primary volunteer team assignment field. Options include Admin, Baptism Team, Care Team, Cleaning, Coffee, Connections, Counting, Facilities, First Impressions, Groups Leaders, Kids, Media, Outreach, Parking, Prayer, Safety, Worship/Production, Youth, Unscheduled Volunteer, Ushers.
- **Dual-tracking concern:** "Current Teams" checkboxes duplicate PCO Services team assignments. When someone is added/removed from a Services team, the custom checkbox must be manually updated, or they drift apart.
- "First Team Served On" (checkboxes, 15 options) — Team names don't fully match "Current Teams" options (e.g., "Caffeine Bar" vs. "Coffee", "Online Ministry" vs. no equivalent).
- Orientation tracking is thorough (4 fields: attended, date, modules completed, completion date).
- Preference fields (Favorite Coffee, Favorite Snack, Shirt Size, Received a volunteer shirt) are low-priority but show volunteer care culture.

### MortarStone Tab (9 fields)

**Rating: HEALTHY**

Integration-managed giving analytics. Fields include: Giving Band, Gift Count, Total Given, Band Last Changed, Last Gift Date, Tags (checkboxes with membership/event tags), Lists (checkboxes), Status (select with donor lifecycle stages: New Donor, Recurring, Lagging 1-6 months, Lapsed, Restarted).

This is well-structured integration data. The MortarStone Tags field doubles as a secondary membership/engagement taxonomy, which could be confusing alongside PCO's built-in membership type.

### Parable Tab (2 fields)

**Rating: HEALTHY**

- Engagement Tier: Highly Engaged, Engaged, Moderate, Low, Disengaged, Inactive
- Warning Light: No Data, New, Healthy, Needs Attention, Urgent, None

Clean integration data with clear engagement scoring.

### Mosaic Steps Tab (8 fields)

**Rating: NEEDS ATTENTION**

Tracks discipleship pathway: Crash Course (attended + date), New to Mosaic (attended + date), Baptized (boolean + date), Dedicated (child — boolean + date).

- "Dedication Date" is a string field instead of a date field — this prevents date-based filtering and reporting.
- From list data: 113 people have Mosaic Baptism Date set. 11 completed Crash Course in last 12 months.
- **Unresolved question:** What percentage of active adults have any Mosaic Steps data? Low penetration would indicate the tab isn't being consistently maintained.

### Connections Tab (11 fields)

**Rating: NEEDS ATTENTION**

- Contains a mix of visitor tracking (Date of first visit, How did they hear about Mosaic?), engagement indicators (How have they attended?), and follow-up data (Prayer Requests, Notes and Comments).
- "Crash Course Completed" and "Open House Attended" are date fields on the Connections tab but are conceptually part of the Mosaic Steps pathway. This creates split tracking.
- "Is 'Today I Decided to Follow Jesus' Checked?" — boolean field presumably from a connect card form. Located on Connections tab but also duplicated conceptually in the Automation tab's "Connect::Decided to Follow Jesus" field.

---

## 2H — Notes & Communication Audit

**Rating: HEALTHY**

### Note Categories

| ID | Name | Locked | Created |
|----|------|--------|---------|
| 62447 | General | Yes | Nov 2018 |
| 62448 | Prayer Requests | No | Nov 2018 |
| 196527 | Staff Note | No | Feb 2023 |
| 196528 | Pastoral Staff Notes | No | Feb 2023 |
| 223318 | Partner step | No | Jan 2024 |
| 278914 | Text In Church Activity | No | Sept 2025 |

**Observations:**
- 6 categories is a reasonable count.
- "Staff Note" vs. "Pastoral Staff Notes" distinction is clear (general staff vs. pastoral care).
- "Partner step" appears to track the membership partnership process — reasonable.
- "Text In Church Activity" is an integration-generated category from PastorsLine/Text In Church. These notes can clutter profiles with automated text message logs. Volume should be monitored.
- General is locked (system default) — appropriate.
- No sensitive-data-specific category (e.g., "Confidential" or "Counseling"). If sensitive pastoral notes exist, they're mixed into "Pastoral Staff Notes." Consider whether additional access controls are needed.

---

## Audit Areas Not Directly Accessible via MCP

The following audit areas require direct PCO API access (REST calls to Groups, Services, Check-Ins, Giving, Calendar, Registrations modules). These were not fully audited in this pass due to tool limitations but are documented here for future audit runs:

- **2I — Groups:** Group types, tags, leader assignments, enrollment status, attendance freshness
- **2J — Services:** Team rosters, position coverage, plan scheduling gaps, people linkage
- **2K — Check-Ins:** Event/station configuration, labels, security codes, location hierarchy
- **2L — Giving:** Fund structure, batch discipline, donor linkage, recurring gift health
- **2M — Calendar:** Event management, resource scheduling, conflicts, approval workflows
- **2N — Registrations:** Event status distribution, people linkage, payment tracking

**Recommendation:** These should be audited in a follow-up pass using authenticated PCO API calls. The People module audit above covers the most impactful data quality areas.

---

## Health Rating Summary

| Audit Area | Rating | Primary Concern |
|------------|--------|-----------------|
| Campus Configuration | NEEDS ATTENTION | ZIP code error |
| Custom Tabs & Fields | AT RISK | Automation tab proliferation, Household Info redundancy |
| Membership Status | AT RISK | 43.8% unassigned |
| Contact Completeness | NEEDS ATTENTION | 26% missing birthdate, 18% missing gender |
| Address Formatting | NEEDS ATTENTION | State field inconsistencies |
| Login Identifiers | NEEDS ATTENTION | 16% phone-based logins |
| Children Data Quality | NEEDS ATTENTION | Null membership, parent contact info on children |
| Lists | NEEDS ATTENTION | 258 lists, proliferation, 3 invalid |
| Workflows | AT RISK | One Month Follow Up critically stalled |
| Forms | NEEDS ATTENTION | Duplication, 17 zero-submission forms |
| Households | NEEDS ATTENTION | 303 adults without households, 46 in multiple |
| Volunteer Info Fields | NEEDS ATTENTION | Dual-tracking with Services |
| Integration Tabs | HEALTHY | MortarStone and Parable well-structured |
| Notes & Categories | HEALTHY | Reasonable structure |

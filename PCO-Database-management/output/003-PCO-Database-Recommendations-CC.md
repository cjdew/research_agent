# PCO Database Recommendations — Mosaic Wadsworth

> **Date:** April 15, 2026
> **Based on:** Phase 1 best practices research + Phase 2 live audit findings
> **Scope:** Planning Center People module (primary), with notes on cross-module concerns
> **Note:** All recommendations are read-only observations. No changes were made to the database.

---

## Priority Tier Definitions

| Tier | Timeframe | Criteria |
|------|-----------|----------|
| **1 — This Week** | 1-5 days | Actively causing harm, blocking operations, or trivially fixable |
| **2 — This Month** | 2-4 weeks | Significant data quality impact, moderate effort |
| **3 — This Quarter** | 1-3 months | Structural improvements, requires coordination |
| **4 — Long-Term** | 3-12 months | Infrastructure changes, policy development, ongoing maintenance |

## Gap Categories

| Type | Definition |
|------|-----------|
| **Quick Win** | Under 30 minutes, low risk, no coordination needed |
| **Project** | Multiple steps, may need planning or coordination |
| **Policy Change** | Requires new SOP, training, or documented standards |
| **Infrastructure** | PCO configuration changes, integration work, or tooling |

---

## Tier 1 — This Week

### 1.1 Fix the "One Month Follow Up" workflow

- **Gap:** 174 overdue cards, 178 unassigned cards. The single step has no assigned person. This represents 174 people who were supposed to receive follow-up and did not.
- **Best practice violated:** Every workflow step should have an assigned owner ([ChurchTechToday — 5 PCO Cleanup Tips](https://churchtechtoday.com/planning-center-clean-up/)).
- **Category:** Quick Win
- **Recommendation:** Assign a staff member to the workflow step immediately. Then triage the 174 overdue cards: bulk-complete those that are stale (6+ months old), and work the recent ones. Consider whether this workflow is still operationally needed or should be consolidated with "Julianna 1st Time Cards, Open House Cards, and one month Letters."
- **Decision owner:** Connections/follow-up staff lead (likely Julianna Palitto or Chris Dewar)

### 1.2 Fix campus ZIP code

- **Gap:** Campus ZIP is 44821 (Attica, OH). Should be 44281 (Wadsworth, OH).
- **Best practice violated:** Accurate organizational data is foundational ([PCO — Organization setup](https://planning.center/)).
- **Category:** Quick Win (30-second fix in PCO Settings)
- **Recommendation:** Update campus ZIP from 44821 to 44281. Also add campus contact email and phone number while editing.
- **Decision owner:** Site Admin (Chris Dewar or Adam Barton)

### 1.3 Delete the "Test automation workflow"

- **Gap:** Empty workflow (0 cards, 0 steps), created Sept 2024, never used.
- **Category:** Quick Win
- **Recommendation:** Delete. It adds noise to the workflow list.
- **Decision owner:** Any Site Admin

### 1.4 Resolve "Old Baptism Workflow" cards

- **Gap:** Archived April 2025 but still has 20 ready cards and 1 overdue card. These represent people in a baptism process.
- **Category:** Quick Win (review 21 cards)
- **Recommendation:** Review the 21 remaining cards. For each: either move the person to the active "Baptism Workflow" or complete the card if the person has already been baptized.
- **Decision owner:** Baptism workflow owner

---

## Tier 2 — This Month

### 2.1 Establish membership status taxonomy and begin cleanup

- **Gap:** 43.8% of active people (895) have no membership type. Additionally, non-standard types like "Easter Registration," "Online Attender," and "Admin Account" are being used as membership types.
- **Best practice violated:** Every person should have a status assigned. Keep taxonomy to 5-7 categories with written definitions ([ChurchTrac](https://www.churchtrac.com/support/people/member-status), [ChurchTechToday](https://churchtechtoday.com/planning-center-clean-up/)).
- **Category:** Policy Change + Project
- **Recommendation:**
  1. **Define the taxonomy.** Recommended: Attender, Partner, Guest, Non-Attender, Community Event Guest, Business. Drop "Easter Registration," "Online Attender," and "Admin Account" as membership types — these are engagement channels/roles, not membership statuses.
  2. **Write one-paragraph definitions** for each status with examples of when to assign each.
  3. **Distribute to all staff** with data entry access.
  4. **Use the existing "Adults No Membership Type" cleanup list** (430 people) to work through in batches of 50-100.
  5. **Create an equivalent list for children** and assign membership types based on parent status.
- **Decision owner:** Chris Dewar (define taxonomy), all staff (execute)

### 2.2 Clean up list proliferation

- **Gap:** 258 lists. Many are one-off queries, duplicates, or reference deleted objects.
- **Best practice violated:** Review and archive/delete unused lists quarterly ([Threefold Solutions](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)).
- **Category:** Project (2-3 hours)
- **Recommendation:**
  1. **Delete the 3 invalid lists** (broken form references).
  2. **Archive or delete one-off query lists** that were clearly ad-hoc (e.g., "Last name starts with 'Dewar' AND First name starts with 'Chris'", "Street Address contains '110'").
  3. **Merge duplicate lists** (two "Age at least 18" lists, two "Membership type is Partner" lists, two "Membership type is Unassigned" lists).
  4. **Disable stale auto-refresh lists** (e.g., the "2024 - Operation Easter Basket" daily refresh list).
  5. **Adopt the naming convention** already partially in use: `[Category] [Description] - [Purpose] - #tag` (e.g., "Adults No Membership Type - Cleanup - #update #monthlyrefresh"). Apply it consistently.
- **Decision owner:** Chris Dewar or database admin

### 2.3 Address the Automation tab field proliferation

- **Gap:** 49 boolean fields that duplicate data already captured via Connections and Volunteer Info checkbox fields. This is the largest tab in the system and represents a form-to-field mapping pattern that doesn't scale well.
- **Best practice violated:** Avoid creating fields that duplicate existing functionality. Use the most specific field type (checkboxes > individual booleans) ([PCO custom field documentation](https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Manage-custom-fields)).
- **Category:** Infrastructure (requires understanding automation dependencies)
- **Recommendation:**
  1. **Audit whether any automations, lists, or workflows depend on these fields** before removing them.
  2. **If no dependencies:** Archive the Automation tab. The data it captures is already in the Connections and Volunteer Info tabs via checkbox fields.
  3. **If dependencies exist:** Document them, then migrate the automations to reference the Connections/Volunteer Info fields instead, then archive the Automation tab.
  4. **Future prevention:** Configure forms to write to existing checkbox fields rather than creating per-option boolean fields.
- **Decision owner:** Chris Dewar (audit dependencies), admin team (migration)

### 2.4 Clean up empty/unused workflows

- **Gap:** "First Time Guests" (0 cards, 4 unassigned steps) and "Missed Family Check-in" (0 cards, 2 steps) have never been used since creation in Feb 2023.
- **Category:** Quick Win
- **Recommendation:** Archive both. If the concepts are still relevant, rebuild with assigned owners when ready to activate.
- **Decision owner:** Any Site Admin

### 2.5 Archive or close zero-submission forms

- **Gap:** 17 forms with 0 submissions, some open since March 2023.
- **Best practice violated:** Close forms after their purpose has ended; review forms with no submissions in 3+ months ([Threefold Solutions](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)).
- **Category:** Quick Win (30 minutes)
- **Recommendation:** Review each of the 17 zero-submission forms. Close or archive those that are clearly obsolete (e.g., "First Step" — 0 submissions since July 2023). Keep only those that are intentionally waiting for their season.
- **Decision owner:** Form owners or admin team

### 2.6 Address children with parent contact info

- **Gap:** Multiple children share parent email addresses and phone numbers (e.g., Cooper/Earley siblings, Henricksen siblings, Harms twins). This causes duplicate communications when messaging by email.
- **Best practice violated:** Avoid copying parent contact info onto children's profiles ([PCO best practices](https://churchtechtoday.com/planning-center-clean-up/)).
- **Category:** Project (requires systematic review)
- **Recommendation:**
  1. Create a list of children with email addresses set.
  2. Review each — remove email/phone from children's profiles where it's clearly the parent's contact info.
  3. Ensure the parent profile has the contact info (it almost certainly does).
  4. Going forward, train check-in and form volunteers not to copy parent info onto child profiles.
- **Decision owner:** Children's ministry director (Lauren DeShon)

---

## Tier 3 — This Quarter

### 3.1 Retire the Household Information tab

- **Gap:** Three custom fields (Household ID, Household Name, Household Primary Contact) duplicate PCO's built-in household management. This creates dual-tracking where custom fields can drift from actual household data.
- **Best practice violated:** Don't create fields that duplicate built-in functionality ([PCO custom field documentation](https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Manage-custom-fields)).
- **Category:** Infrastructure
- **Recommendation:**
  1. Export the current custom field data for reference.
  2. Verify that built-in household assignments match the custom fields (spot-check 20-30 records).
  3. If they match, archive the tab. If significant drift exists, reconcile first.
  4. Remove references to these custom fields from any lists, workflows, or automations.
- **Decision owner:** Chris Dewar

### 3.2 Resolve the volunteer dual-tracking problem

- **Gap:** "Current Teams" checkboxes in the Volunteer Info tab duplicate PCO Services team assignments. When someone joins or leaves a Services team, the custom checkbox must be manually updated.
- **Best practice violated:** Pick one source of truth for volunteer team assignments. Avoid dual-tracking ([Threefold Solutions](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database), [Vanco — Church Volunteer Management](https://www.vancopayments.com/egiving/blog/church-volunteer-management)).
- **Category:** Policy Change + Infrastructure
- **Recommendation:**
  1. **Decide which is the source of truth:** PCO Services team assignments (recommended — it's the live scheduling system) or custom checkboxes.
  2. **If Services is the source of truth:** Use the custom "Current Teams" field only for teams not tracked in Services (e.g., non-Sunday ministry teams). Rename it to something like "Non-Scheduled Teams" to avoid confusion.
  3. **Alternatively:** Keep "Current Teams" as a high-level summary field but acknowledge it requires manual maintenance and build a quarterly review process.
  4. **Reconcile team name inconsistencies** between "Current Teams" and "First Team Served On" (e.g., "Caffeine Bar" vs. "Coffee").
- **Decision owner:** Chris Dewar + team leads

### 3.3 Household cleanup project

- **Gap:** 303 active adults without household assignments, 46 people in multiple households.
- **Best practice violated:** Every person should belong to a household ([PCO Households](https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households)).
- **Category:** Project (multi-session)
- **Recommendation:**
  1. Use the existing "Adults no household" list (303 people).
  2. Work through in batches: create households for singles, add to existing family households where applicable.
  3. Review the 46 people in multiple households — resolve legitimate blended family situations vs. errors.
  4. Set primary contacts on all households.
- **Decision owner:** Admin team

### 3.4 Gender and birthdate data fill

- **Gap:** 487 active people with unspecified gender (24%), 26% of sampled adults missing birthdate.
- **Best practice violated:** Complete demographic data enables accurate reporting, age-appropriate communications, and proper Check-In assignments ([Threefold Solutions](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)).
- **Category:** Project (ongoing)
- **Recommendation:**
  1. Create targeted cleanup lists (if not already existing): "Missing Gender" and "Missing Birthdate" for active adults and children.
  2. Prioritize volunteers and regular attenders — their data has the most operational impact.
  3. Use Church Center self-service: encourage profile updates via the app.
  4. Capture at next check-in or form interaction.
- **Decision owner:** Admin team

### 3.5 Review 33 Degree and Clean My PCO tab status

- **Gap:** Both tabs may be associated with inactive campaigns/subscriptions, but their current status is unclear.
- **Category:** Quick Win (decision only)
- **Recommendation:**
  1. **33 Degree:** Determine if the capital campaign is still active. If not, export the data and archive the tab.
  2. **Clean My PCO:** Check if the subscription is active. If active, verify the "Date of Last Bulk Cleaning" field to confirm it's running. If inactive, archive the tab (the cleanup data has limited ongoing value without the service).
- **Decision owner:** Chris Dewar

### 3.6 Clean up PastorsLine checkbox names

- **Gap:** 41 checkbox options with auto-generated, hard-to-read names including hashtags and workflow step references.
- **Category:** Infrastructure (coordinate with PastorsLine integration)
- **Recommendation:** Review which PastorsLine group mappings are still actively used. Remove stale options. Simplify names if possible. This may require coordination with PastorsLine configuration.
- **Decision owner:** Communications lead

---

## Tier 4 — Long-Term / Ongoing

### 4.1 Establish a quarterly database maintenance cadence

- **Gap:** No documented maintenance schedule exists. Cleanup efforts are ad-hoc.
- **Best practice violated:** Establish a tiered maintenance schedule: weekly (30 min), monthly (2 hrs), quarterly (half day), annually ([Bloomerang](https://bloomerang.com/blog/crm-cleanup-tasks-for-donor-data/), [Threefold Solutions](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)).
- **Category:** Policy Change
- **Recommendation:**
  1. **Weekly (30 min):** Review duplicate detector, process blocked emails, check workflow cards for overdue items.
  2. **Monthly (2 hrs):** Run membership status cleanup list, review new profiles for completeness, check form/list freshness.
  3. **Quarterly (half day):** Archive old forms/lists, audit custom field usage, review household assignments, run this audit prompt.
  4. **Annually:** Full audit, grade promotions, giving statement preparation, staff training refresh.
- **Decision owner:** Chris Dewar (establish), designated PCO Champions (execute)

### 4.2 Designate PCO Champions

- **Gap:** Database maintenance appears centralized to a few admins.
- **Best practice violated:** Designate 2-3 PCO Champions and distribute ownership by ministry area ([Threefold Solutions](https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database)).
- **Category:** Policy Change
- **Recommendation:** Assign ownership:
  - **Children's data:** Lauren DeShon (already admin)
  - **Volunteer data:** Julianna Palitto (already admin)
  - **Overall data quality + Giving:** Chris Dewar
  - Each champion is responsible for their domain's data quality in monthly reviews.
- **Decision owner:** Chris Dewar

### 4.3 Develop data entry standards documentation

- **Gap:** No written data entry standards. State field shows 6 variations of "Ohio."
- **Best practice violated:** Create and enforce standardized data entry procedures ([Humanitru](https://www.humanitru.com/14-data-hygiene-tips-for-nonprofits/), [NPO Info](https://npoinfo.com/nonprofit-data-hygiene/)).
- **Category:** Policy Change
- **Recommendation:** Create a one-page data entry guide covering:
  - Membership type definitions and when to assign each
  - Address formatting standards (USPS abbreviations, state = "OH")
  - When to create vs. search for existing profiles
  - What contact info goes on child profiles vs. parent profiles
  - Login identifier should be email, not phone
  - Share with all staff and volunteers with data entry access.
- **Decision owner:** Chris Dewar

### 4.4 Implement inactive record archival policy

- **Gap:** 3,838 inactive records (65% of database). The "9 Month Auto Inactivate" list (553 people) shows inactivation is happening, but no archival/deletion policy exists for very old inactive records.
- **Best practice violated:** Establish data retention policy with review periods ([VinciWorks — Data Protection for Churches](https://vinciworks.com/blog/data-protection-for-churches/), [Bloomerang](https://bloomerang.com/blog/crm-cleanup-tasks-for-donor-data/)).
- **Category:** Policy Change
- **Recommendation:**
  1. Define retention periods: inactive 1-2 years = keep, inactive 3-5 years = review, inactive 5+ years with no giving history = consider removal.
  2. Preserve giving records per IRS requirements (7 years minimum for tax-deductible donations).
  3. Review annually.
- **Decision owner:** Chris Dewar + legal/compliance consideration

### 4.5 Audit remaining PCO modules

- **Gap:** This audit covered the People module thoroughly but did not audit Groups, Services, Check-Ins, Giving, Calendar, or Registrations modules via their APIs.
- **Category:** Project
- **Recommendation:** Run a follow-up audit covering:
  - Groups (types, tags, leader assignments, attendance freshness)
  - Services (team rosters, scheduling gaps, orphaned records)
  - Check-Ins (event configuration, location hierarchy, label setup)
  - Giving (fund structure, batch discipline, donor linkage, statement readiness)
  - Calendar (resource management, conflicts, event cleanup)
  - Registrations (event status, people linkage, payment tracking)
  - Cross-module integration points (People to all other modules)
- **Decision owner:** Chris Dewar

---

## Cross-Module Integration Gaps (Preliminary)

Based on People module data, several cross-module concerns are visible:

1. **People to Services:** The dual-tracking problem (custom "Current Teams" checkboxes vs. Services team assignments) creates data drift risk. The "Removed from Team" workflow (228 cards) suggests team membership changes are tracked but may not be reflected in custom fields.

2. **People to Check-Ins:** Children without birthdate or grade data (visible in sample) will not be assigned to correct age-group locations in Check-Ins.

3. **People to Giving:** MortarStone integration appears healthy, providing giving analytics directly on People profiles. The "First Time Giver" workflow (228 cards, 8 overdue) connects giving events to People follow-up.

4. **People to Forms:** Several lists reference forms that no longer exist (3 invalid lists), indicating form deletion without list cleanup.

5. **People to Groups:** List data shows group attendance is being tracked (e.g., "Attended at least 3 events since 12 months ago"). The Volunteer Info "Groups (Leaders and Hosts)" team option and the "Interested in Small Groups" workflow suggest groups are actively managed.

---

## Quick Wins Summary (All Under 30 Minutes)

| # | Action | Impact | Time |
|---|--------|--------|------|
| 1 | Fix campus ZIP (44821 to 44281) | Corrects location data | 1 min |
| 2 | Assign owner to "One Month Follow Up" workflow step | Unblocks 178 cards | 2 min |
| 3 | Delete "Test automation workflow" | Reduces clutter | 1 min |
| 4 | Archive "First Time Guests" and "Missed Family Check-in" workflows | Reduces clutter | 2 min |
| 5 | Delete 3 invalid lists | Removes broken objects | 5 min |
| 6 | Disable stale auto-refresh on "2024 Operation Easter Basket" list | Stops unnecessary daily processing | 2 min |
| 7 | Review 21 cards in "Old Baptism Workflow" | Resolves stuck baptism candidates | 15-20 min |
| 8 | Close 5+ zero-submission forms (First Step, How can we help?, Mosaic Group Sign Up, Mosaic Youth Info, Volunteer Info Form) | Reduces form clutter | 10 min |

---

## Implementation Roadmap

```
Week 1:  Quick wins (items 1.1-1.4 + quick wins summary)
Week 2:  Define membership taxonomy, begin cleanup (2.1)
Week 3:  List cleanup (2.2), form cleanup (2.5)
Week 4:  Automation tab audit (2.3), children contact cleanup (2.6)

Month 2: Household cleanup (3.3), Household Info tab retirement (3.1)
Month 3: Volunteer dual-tracking resolution (3.2), gender/birthdate fill (3.4)

Quarter: Tab reviews (3.5, 3.6), maintenance cadence (4.1), data entry standards (4.3)
Ongoing: PCO Champions (4.2), inactive archival policy (4.4), module audits (4.5)
```

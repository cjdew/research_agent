# PCO Database Management — Research & Audit Prompt

> **Purpose:** Drive a comprehensive research + live audit of Planning Center Online database management practices. Produces a best-practices reference document and a gap analysis specific to Mosaic Wadsworth's PCO setup.
>
> **When to run:** Quarterly, or before any major PCO cleanup/migration project.
>
> **Connected tools required:** PCO People MCP (search, lists, workflows, forms, field definitions, households, notes, tabs, organization). Full PCO API access available via Claude Code for all modules (Services, Check-Ins, Giving, Calendar, Groups, Registrations). Web search for external research.

---

## Phase 1: Best Practices Research

Research current, up-to-date best practices for managing all aspects of a Planning Center Online database. Collect guidance from three distinct source categories. For each finding, record the source URL, date published/updated, and a one-sentence summary.

### 1A — PCO Official Resources

Search the following domains and knowledge bases for guidance on database management, data hygiene, and module-specific best practices:

- **planning.center/blog** — Product updates, feature announcements, best practice posts
- **pco.support** (Planning Center support articles) — How-to guides for People, Lists, Workflows, Forms, Households, Merge/Dedup, Check-Ins, Groups, Giving, Services, Calendar, Registrations
- **Planning Center University / YouTube channel** — Training videos and webinars on database management
- **Planning Center API documentation** (developer.planning.center) — Data model documentation that reveals field relationships, constraints, and intended use patterns

For each PCO module, research:
- What data fields exist and which are required vs. optional
- Recommended workflows for data entry, updates, and archival
- Built-in tools for deduplication, merging, and data cleanup
- List and automation features for ongoing data hygiene
- Integration points between modules (how People data flows to Check-Ins, Groups, Giving, Services)

### 1B — Church Technology Consultants & Advisory Sites

Search for best-practice guidance from independent consultants and church technology advisory organizations. Prioritize sources updated within the last 18 months. Target sources include:

- **The Church Co** (thechurch.co) — PCO consulting and implementation
- **Storyteller Creative** — Church tech strategy
- **Ministry Grid / Lifeway Digital** — Church operations training
- **ChurchTechToday** — Church technology reviews and guides
- **Unseminary** — Church leadership and operations
- **Church Juice** — Communications and operations
- **Pro Church Tools** — Digital church strategy
- **The Unstuck Group** — Church consulting (operational systems)
- **Brotherhood Mutual / Church Mutual** — Risk management perspectives on data handling
- **Any PCO-certified consultant or implementation partner** found via search

Research topics from these sources:
- Database cleanup cadence and methodology recommendations
- Membership status taxonomy best practices (Active, Inactive, Visitor, etc.)
- Household management strategies
- Custom field architecture — what to track and what not to track
- Volunteer management database patterns
- Child safety and background check data management
- Giving data hygiene and donor record management
- Multi-campus database strategies (if applicable)
- Staff training on data entry standards

### 1C — Data Integrity & Nonprofit CRM Research

Search for broader data management best practices applicable to church/nonprofit CRM systems:

- **Nonprofit CRM best practices** — data governance, deduplication strategies, merge policies
- **Contact database hygiene** — email validation, address standardization, phone formatting
- **Data lifecycle management** — when to archive vs. delete, retention policies, GDPR/privacy considerations
- **Duplicate detection and resolution** — algorithmic approaches, manual review workflows, prevention strategies
- **Data entry standardization** — naming conventions, abbreviation policies, required field enforcement
- **Reporting and list hygiene** — keeping lists current, automating staleness detection
- **Access control and permissions** — role-based access in shared databases, audit trails
- **Integration data integrity** — maintaining consistency across connected systems (PCO ↔ QuickBooks, PCO ↔ Mailchimp, etc.)

### Phase 1 Deliverable

Compile findings into a structured markdown reference document organized by topic area (not by source). Each section should synthesize across all three source categories, noting where consensus exists and where advice diverges. Save as `PCO-Best-Practices-Reference.md` in the outputs folder.

---

## Phase 2: Live PCO Audit

Using the connected PCO People MCP tools, audit Mosaic Wadsworth's actual database against the best practices compiled in Phase 1. Work through each audit area methodically.

### 2A — Organization & Structure Audit

- Pull organization info and campus configuration
- Inventory all custom tabs on people profiles. Known tabs from staff sample: 33 Degree, Clean My PCO, Connections, Household Information, Military & Work, MortarStone, Mosaic Steps, Parable, PastorsLine.com (Integration), Volunteer Info. Check if there are additional tabs beyond these.
- Inventory all custom field definitions — document name, data type, tab assignment, and whether each appears actively used
- Check for orphaned or redundant custom fields (fields with no data or duplicate-seeming fields). Specific concern: the "Household Information" tab has a "Household Name" string field that may duplicate PCO's built-in household feature.
- Assess field naming consistency and organization
- Identify which tabs are integration-managed (MortarStone, Parable, PastorsLine) vs. manually maintained (Volunteer Info, Mosaic Steps, Connections) — these have different data quality implications
- Check the "Clean My PCO" tab specifically — it contains email verification failure data. Assess whether this tab is being actively used for cleanup or has gone stale.

### 2B — People Data Quality Audit

- Pull a sample of people records (at least 50-100) and assess completeness:
  - What percentage have email addresses?
  - What percentage have phone numbers?
  - What percentage have mailing addresses?
  - What percentage have membership status set? (Staff sample showed ~52% of children had "None")
  - What percentage have a household assignment?
  - What percentage have gender and birthdate set? (Staff sample found 3 missing)
- Check for potential duplicates by searching for common last names and looking for similar entries
- Check for records with no activity indicators (no lists, no form submissions, no workflow cards)
- Identify inactive records — how many exist and when were they last updated?
- Look for data formatting inconsistencies. Known patterns from staff sample:
  - Mixed address abbreviations (Road vs Rd, Drive vs Dr, Street vs St)
  - Inconsistent ZIP+4 usage (some have full ZIP+4, others have ZIP-5 only)
  - Phone numbers used as login identifiers instead of email addresses
  - BLOCKED email addresses that prevent communication
  - Children with parent contact info copied into their profiles (causes duplicate comms)
  - Duplicate phone/address entries on the same person profile
- Check membership status taxonomy usage at scale. Known values: Attender, Partner, Guest, None. Assess whether the taxonomy is sufficient or needs expansion (e.g., Member, Visitor, Inactive).
- Audit the "Guest" status specifically — staff sample showed a staff spouse and some children marked Guest who may warrant Attender status.

### 2C — Lists & Automation Audit

- Pull all lists and assess:
  - Total count of lists
  - How many have automations active vs. paused?
  - How many are starred (actively used)?
  - How many haven't been refreshed recently?
  - Are there lists with overlapping purposes or confusing names?
- Check for invalid lists (lists where the rules no longer work)
- Assess list naming conventions and categorization

### 2D — Workflows Audit

- Pull all workflows (active and archived) and assess:
  - Total count active vs. archived
  - How many have overdue cards?
  - How many have unassigned cards or steps?
  - How many have ready cards that haven't been acted on?
  - What workflow categories exist and are they well-organized?
- Identify workflows that appear stalled (high card counts, many overdue)
- Check for workflows that duplicate each other's purpose

### 2E — Forms Audit

- Pull all forms (open, closed, archived) and assess:
  - Total count by status
  - Which forms have active submissions?
  - Are there forms that should be closed or archived?
  - Do form names clearly indicate their purpose?

### 2F — Households Audit

- Sample households and check:
  - Are people properly grouped into households?
  - Are primary contacts set appropriately?
  - Are there single-person households that should be merged?
  - Are there households with mismatched last names that may indicate data issues? (Note: blended families are common — e.g., Barton household has Hatch, Owensby, Gaeckle last names; Dawson household has Kilkenny, Bowling, Johnson. These are legitimate.)
  - Are there inactive members sitting in active households? (Staff sample: Lawrence Swaney inactive in Swaney household; Baron Bowling and Maggie Kilkenny inactive in Dawson household)
  - Do household member addresses match? (Staff sample found some members with out-of-state addresses, e.g., Maggie Kilkenny with Texas address in Ohio household)

### 2G — Custom Fields & Integration Data Audit

This section goes deeper than the structure audit (2A) to assess actual field data quality:

- **Volunteer Info tab** (highest priority — most populated custom tab):
  - How many people have "Current Teams" populated? Are the team names consistent?
  - Is "Current Leadership or Contractor" set for all team leads/staff?
  - Are orientation dates, shirt sizes, and preferred contact methods current?
  - Are "First time serving date" and "First Team Served On" populated for active volunteers?
  - Is there a gap between PCO Services team assignments and the custom "Current Teams" checkboxes? (This is a potential dual-tracking problem.)

- **MortarStone tab** (giving analytics — auto-populated):
  - How many people have MortarStone data? Is it limited to donors or applied broadly?
  - Are "Last Gift Date" values current or stale?
  - Are giving bands populated consistently?

- **Parable tab** (engagement scoring — auto-populated):
  - What's the distribution of Engagement Tiers across the database? (Staff sample showed: Engaged, Moderate, Low, Disengaged)
  - How many people have "Warning Light" set to something other than Healthy or No Data?
  - Is Parable data being used operationally, or just collected?

- **PastorsLine.com tab**:
  - Assess the group mapping checkboxes — are the group names clean and current?
  - Staff sample showed very long auto-generated names with hashtags. Check if these are still actively used or are legacy mappings.

- **Mosaic Steps tab** (discipleship pathway):
  - What percentage of adults have pathway data (Crash Course, Baptism, New to Mosaic)?
  - Is this tab being maintained or has it gone dormant?

- **33 Degree tab** (capital campaign):
  - Is this campaign still active? If not, should the tab be archived?

### 2H — Notes & Communication Audit

- Inventory note categories. Known categories from staff sample: "Text In Church Activity", "General". Check for additional categories.
- Check if note categories are well-organized and clearly named
- Assess whether sensitive information categories are properly separated
- Check whether PastorsLine text activity notes are cluttering profiles (staff sample showed multiple automated text log entries per person)

### 2I — Groups Audit (via PCO API)

Use the PCO Groups API (`/groups/v2/groups`, `/groups/v2/group_types`, `/groups/v2/tags`) to audit:
- Total group count by type and status (open, closed, archived)
- Group types and whether the taxonomy is well-organized
- Tag usage — are groups consistently tagged for filtering and reporting?
- Enrollment status — how many groups are open for self-signup vs. leader-managed?
- Leader assignments — are all active groups assigned at least one leader?
- Membership freshness — are there groups with no recent attendance or membership changes?
- Location data completeness — do groups that meet in-person have locations set?

### 2J — Services Audit (via PCO API)

Use the PCO Services API (`/services/v2/service_types`, `/services/v2/teams`, `/services/v2/people`) to audit:
- Service type inventory and scheduling patterns
- Team roster completeness — are all serving teams fully populated with current members?
- Blocked-out dates — are team members keeping their availability current?
- Position coverage — are there unfilled positions or teams with chronic gaps?
- Plan frequency — are services being planned consistently or are there gaps?
- People linkage — are Services person records properly linked to People profiles (no orphaned records)?
- Song/media library hygiene — duplicate entries, incomplete metadata

### 2K — Check-Ins Audit (via PCO API)

Use the PCO Check-Ins API (`/check-ins/v2/events`, `/check-ins/v2/stations`, `/check-ins/v2/labels`) to audit:
- Event and station configuration — are check-in events current and well-organized?
- Label templates — are labels configured correctly for each age group/environment?
- Security code settings — are security codes enabled and printing correctly?
- Location structure — does the check-in location hierarchy match physical spaces?
- Historical check-in data — are there events or locations that are no longer used but still active?
- Grade/age group alignment — are grade promotions configured and scheduled?

### 2L — Giving Audit (via PCO API)

Use the PCO Giving API (`/giving/v2/donations`, `/giving/v2/funds`, `/giving/v2/donors`, `/giving/v2/batches`) to audit:
- Fund structure — are funds well-named, active, and not duplicated?
- Batch discipline — are donations consistently batched, or are there unbatched donations?
- Donor record linkage — are giving records properly linked to People profiles?
- Designation accuracy — are donations going to the correct funds?
- Recurring giving health — how many active recurring donors exist? Any stalled recurring gifts?
- Statement readiness — is giving data clean enough for year-end statements?
- Payment source distribution — online vs. cash/check vs. ACH breakdown

### 2M — Calendar Audit (via PCO API)

Use the PCO Calendar API (`/calendar/v2/events`, `/calendar/v2/resources`, `/calendar/v2/event_resource_requests`) to audit:
- Event count and recurrence patterns — are events well-maintained or cluttered?
- Resource management — are rooms/equipment set up and actively used for scheduling?
- Approval workflows — are resource requests being processed or piling up?
- Event ownership — do all events have a responsible contact/team?
- Conflict detection — are there overlapping resource bookings?
- Historical cleanup — are past events being archived appropriately?

### 2N — Registrations Audit (via PCO API)

Use the PCO Registrations API (`/registrations/v2/events`) to audit:
- Event count by status (open, closed, draft, archived)
- Registration completeness — are registrant records linked to People profiles?
- Payment tracking — are paid registrations reconciled?
- Form design — do registration forms collect appropriate information without over-asking?
- Waitlist management — are waitlists being actively managed?
- Historical events — are completed events archived to reduce clutter?

### Phase 2 Deliverable

Compile audit findings into a structured report with quantitative metrics and specific observations. For each area, assign a health rating: HEALTHY (meets best practices), NEEDS ATTENTION (minor gaps), or AT RISK (significant gaps requiring action). Save as `PCO-Audit-Findings.md` in the outputs folder.

---

## Phase 3: Gap Analysis & Recommendations

Compare Phase 1 best practices against Phase 2 audit findings. Produce a prioritized action plan.

### 3A — Gap Identification

For each audit area, identify specific gaps between current state and best practice. Categorize each gap as:
- **Quick Win** — Can be fixed in under 30 minutes, low risk
- **Project** — Requires planning, multiple steps, or coordination
- **Policy Change** — Requires a new standard operating procedure or training
- **Infrastructure** — Requires PCO configuration changes, new integrations, or tool setup

### 3B — Prioritized Action Plan

Rank all identified gaps by impact (how much the gap affects data quality and ministry operations) and effort (how much time and coordination the fix requires). Produce a prioritized list with:
- Gap description
- Best practice it violates (with source)
- Current state observation
- Recommended action
- Priority tier (1 = do this week, 2 = do this month, 3 = do this quarter, 4 = long-term)
- Responsible role (who should own this)

### 3C — Cross-Module Integration Gaps

Since all PCO modules are auditable via the full API, this section focuses on how well data flows between modules:
- **People ↔ Groups:** Are group members synced with People profiles? Are there group members not in the People database?
- **People ↔ Services:** Are serving team members linked to their People records? Are there orphaned Services profiles?
- **People ↔ Check-Ins:** Do check-in records link back to People profiles? Are there unlinked check-in guests?
- **People ↔ Giving:** Are donor records properly linked? Are there anonymous donations that could be matched?
- **People ↔ Registrations:** Are registrants linked to People profiles? Is registration data flowing into People custom fields where appropriate?
- **Calendar ↔ Services/Check-Ins:** Are service times and check-in events reflected in the calendar? Are there conflicts?
- **Overall data consistency:** Are there people who appear in one module but not People (the core record)?

### Phase 3 Deliverable

Compile into a final recommendations document. This is the primary project deliverable. Save as `PCO-Database-Recommendations.md` in the outputs folder.

---

## Output Summary

At the end of the full run, produce three files:
1. `PCO-Best-Practices-Reference.md` — The research compilation (Phase 1)
2. `PCO-Audit-Findings.md` — The live data audit report (Phase 2)
3. `PCO-Database-Recommendations.md` — The gap analysis and action plan (Phase 3)

Also produce a brief executive summary (10-15 bullet points) in the conversation covering:
- Top 5 most impactful findings
- Top 5 quick wins
- Any urgent issues requiring immediate attention
- Recommended next steps for turning this into an ongoing project

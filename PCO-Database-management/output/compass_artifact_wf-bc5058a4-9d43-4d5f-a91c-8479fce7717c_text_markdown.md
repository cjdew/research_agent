# PCO Database Management — Best Practices Reference

**Prepared:** April 15, 2026
**Scope:** Planning Center Online (PCO) — all modules (People, Services, Check-Ins, Giving, Groups, Registrations, Calendar)
**Sources consulted:** 28 distinct sources (19 PCO-specific, 9 general nonprofit/CRM)

---

## 1. Data governance foundations

Good database management begins not with software features but with organizational commitment. Planning Center's modular architecture — where People serves as the central hub feeding Services, Check-Ins, Giving, Groups, and Registrations — makes governance especially important because a single person record propagates across every module [Source: https://www.planningcenter.com/people, Planning Center, current]. Without clear ownership, standards, and accountability, data quality degrades rapidly. Only **16% of nonprofits** report their staff as "completely knowledgeable" about CRM use, underscoring how critical intentional governance is [Source: https://www.ccsfundraising.com/insights/nonprofit-data-management/, CCS Fundraising, 2025].

### Ownership and stewardship roles

A church data governance structure should mirror the nonprofit best-practice model: an **Executive Sponsor** (Senior or Executive Pastor), a **Data Governance Manager** (Church Administrator), a **Governance Committee** (ministry leaders from children's, worship, groups, and finance), and **Data Stewards** (trained staff or volunteers who enter and maintain data daily) [Source: https://www.brightvinesolutions.com/post/data-governance-what-it-is-and-why-you-need-it-part-1, BrightVine Solutions, January 2022]. The NetHope Nonprofit Data Governance Toolkit, based on the Data Management Body of Knowledge (DMBOK), provides template policies, defined roles, and implementation roadmaps adaptable to church contexts [Source: https://nethope.org/toolkits/data-governance-toolkit-a-guide-to-implementing-data-governance-in-nonprofits/, NetHope, April 2022].

Threefold Solutions, a PCO-certified consultancy, recommends training **multiple "PCO Champions"** to avoid single points of failure — one person should not be the sole keeper of database knowledge [Source: https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database, Threefold Solutions, May 2024]. Assign stakeholder ownership by area: a children's ministry director owns grade and allergy data, a finance administrator owns giving records, and a volunteer coordinator owns background check status.

### Data entry standards

Standardization at point of entry prevents most downstream problems. Churches should create a written **PCO Data Entry Guide** covering name formatting, phone number format, address standards, and membership status codes [Source: https://cdsfunds.com/nonprofit-crm-data-best-practices, CDS Funds, 2024]. PCO provides built-in dropdowns for commonly repeated fields (membership types, inactive reasons, schools) — these should always be used over free-text entry to prevent variation [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Customize-fields, Planning Center, current].

Key PCO-specific naming conventions: the **First Name** field holds what the person goes by (e.g., "Tom"), the **Given Name** field holds the legal name for check-writing and Giving matching (e.g., "Thomas"), and the **Nickname** field holds informal names (e.g., "Neo"). All name variations are searchable [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204263114-Profile-overview, Planning Center, current]. The third-party integration **Clean My PCO** can automate name capitalization, USPS address verification, and formatting corrections in real time [Source: https://cleanmypco.com/, Clean My PCO / https://www.planningcenter.com/integrations/clean-my-pco, Planning Center, current].

### Training cadence

NTEN recommends providing training in **small doses (5–10 minutes)** during meetings or via short videos, reinforcing learning at 1-day, 1-week, and 1-month intervals [Source: https://www.nten.org/blog/developing-staff-technology-skills-in-your-nonprofit, NTEN, 2023]. Training should be role-specific: front desk staff learn data entry and check-in, ministry leaders learn group management and attendance, the finance team learns giving records, and pastoral staff learn people notes and workflows [Source: https://www.pairsoft.com/blog/how-to-guarantee-your-nonprofit-crm-data-is-accurate/, PairSoft, 2024]. Niche Academy emphasizes identifying **tech champions** — early adopters who advocate for the system — and providing hands-on sandbox practice [Source: https://www.nicheacademy.com/blog/tech-training-for-nonprofit-staff, Niche Academy, 2025].

---

## 2. People records — core fields and data quality

### Required versus optional fields

Via the PCO API and interface, creating a person record requires only a **first name and last name**. All other fields are optional [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204263114-Profile-overview, Planning Center, current]. The built-in default fields on the Personal tab — which "are included automatically and cannot be deleted" — include: name fields (First, Last, Given, Nickname), birthday, gender, life stage, marital status, anniversary, email, phone, address, social profiles, school details, and membership type [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Customize-fields, Planning Center, current].

### Recommended data collection strategy

Digital Outreach recommends a **progressive data collection** approach aligned to engagement depth. For **first-time guests**, collect only first name, last name, email, and phone — and immediately assign a membership type. For **regular attenders**, add gender, address, household, profile picture, birthday, and marital status. For **members**, add any additional custom fields needed [Source: https://digitaloutreach.com/blog/planning-center-people-cleanup, Digital Outreach, current]. This approach reduces form fatigue while ensuring core data is captured at each stage.

### Data normalization standards

Address formatting should follow USPS conventions. Phone numbers should use a consistent format (PCO does not enforce a format, so a written standard is essential). CCS Fundraising identifies common data quality problems that apply directly to PCO: abbreviation inconsistencies ("St." vs. "Street"), name variations, and using name fields for status indicators (e.g., typing "DECEASED" in the last name field) [Source: https://www.ccsfundraising.com/insights/nonprofit-data-management/, CCS Fundraising, 2025]. Churches should use PCO's built-in Inactive Reasons (including the irremovable "Deceased" label) rather than overloading name fields [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013192194-Manage-membership, Planning Center, current].

---

## 3. Household management

### How PCO structures households

PCO households allow tracking of families within a church. Critically, **people can belong to multiple households** — essential for split families, divorce situations, and children with two homes [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households, Planning Center, current]. Each household member is assigned a role: **Parent/Guardian**, **Child**, or **Other Adult** (for adult children, dependents, or relatives needing some guardian capabilities). A gold star icon (⭐) marks the **primary contact**, whose contact information displays in Check-Ins reports, the church directory, and communications [Source: https://www.planningcenter.com/changelog/people/new-parent-guardian-household-roles, Planning Center, current].

Households are used across modules: Services uses them for family scheduling, Check-Ins enables parents to check in children, and Giving generates joint donor statements for couples sharing an address [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households, Planning Center, current].

### Primary contact and household naming

The primary contact's information represents the household in external communications. PCO automatically derives household names from member names. When three or more adults are in a household, reports display "The [Household Name]" instead of individual names. A practical rule from PCO consultants: **"If a person can legally sign a document, they should be in their own household."** Adult children should be separated into their own household, with the original household containing only the two legal guardians [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households, Planning Center, current].

### Split households and common errors

For children in two homes after divorce, add the child to both parents' households. If a child belongs to two households, reports show two rows with each household's primary contact [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360003006334-Common-lists, Planning Center, current]. A common data error is **children marked as primary contact** in a household — PCO recommends building an auto-refreshing list to catch this [Source: https://churchtechtoday.com/planning-center-clean-up/, ChurchTechToday, February 2022]. Editing a household member's "Home" phone or address triggers an option to update the same field for all household members, preventing inconsistencies [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households, Planning Center, current].

When congregants are enabled to edit household information via Church Center, adults can add or remove household members, but children cannot — providing a natural access control [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households, Planning Center, current].

---

## 4. Membership status and custom fields

### Status taxonomy best practices

PCO ships with customizable default membership types — typically Member, Regular Attender, and Visitor — but churches can fully customize these labels from the Customize Fields page (requires Manager permissions) [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013192194-Manage-membership, Planning Center, current]. Sources consistently recommend a minimum of **three tiers**: Guest/Visitor, Regular Attender, and Member [Source: https://digitaloutreach.com/blog/planning-center-people-cleanup, Digital Outreach, current]. Beyond these, churches may add statuses like "Prospective Member," "Inactive Member," or "Staff."

The single most important cleanup step, according to multiple sources, is **assigning every person a membership type**. This enables proper communication segmentation — irrelevant mass communications erode trust [Source: https://digitaloutreach.com/blog/planning-center-people-cleanup, Digital Outreach, current]. PCO's membership types can restrict access to member-only content on Church Center and drive list-based automations [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013192194-Manage-membership, Planning Center, current].

Inactive Reasons are also customizable (except "Deceased," which cannot be edited or removed). When setting a profile inactive, PCO offers the option to **clear membership status**, preventing the person from appearing on membership-based lists or accessing restricted Church Center pages [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360013192194-Manage-membership, Planning Center, current].

### Custom field design philosophy

Custom fields in PCO are organized into **custom tabs** (e.g., "Volunteer Info," "Medical," "Membership Milestones"). Available field types include text, paragraph, date, yes/no, dropdown, checkbox, number, and heading [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Customize-fields, Planning Center, current]. The general principle from multiple sources: **use built-in fields first** (membership type, gender, birthday, etc.) and add custom fields only for genuinely unique data — baptism dates, spiritual gifts inventories, communication preferences, or membership class completion tracking [Source: https://www.threefold.solutions/blog/from-attenders-to-members-tracking-membership-milestones-in-planning-center-people, Threefold Solutions, 2024].

Each custom tab supports **collaborator-based access control**: non-collaborators see "[hidden content]" instead of field values. This is essential for sensitive information like counseling notes or medical data [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Customize-fields, Planning Center, current]. As of 2025, custom fields can be exposed to congregants on Church Center with granular control: view only, add if blank, or full edit [Source: https://www.planningcenter.com/blog/2025/09/no-more-form-fatigue-let-people-edit-their-own-information-in-church-center, Planning Center, September 2025].

---

## 5. Duplicate record management

### How duplicates form

Duplicates in PCO most commonly occur when a person uses a different email or phone number across different interactions — registering for an event, donating, completing a form, or signing up for a group. Fields must match exactly or PCO creates a new profile [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360051926993-Prevent-duplicate-profiles, Planning Center, current]. The new donation form (2025) added phone-based verification to reduce bot-created and duplicate donor profiles [Source: https://www.planningcenter.com/blog/2025/09/the-all-new-donation-form, Planning Center, 2025].

### PCO's duplicate detector

PCO's built-in **Duplicate Detector** uses machine learning to identify potential duplicates based on exact name matches, similar-sounding names (like John and Jon), and common nicknames. A 2017 algorithm update detected **36% more duplicates while creating 20% fewer false positives**. The system learns from every merge and ignore decision [Source: https://www.planningcenter.com/blog/duplicate-detector, Planning Center, current]. The detector is found on the People Dashboard under "Potential duplicates." A ⚠️ warning sign on a profile's Actions button indicates a flagged potential duplicate [Source: https://pcopeople.zendesk.com/hc/en-us/articles/115000165267-Merge-duplicate-profiles, Planning Center, current].

Smart exclusions prevent false matches: profiles with different genders set, profiles in the same household, and same names with different suffixes (Jr., Sr.) are not flagged [Source: https://pcopeople.zendesk.com/hc/en-us/articles/115000165267-Merge-duplicate-profiles, Planning Center, current].

### Merge process and data implications

Two merge methods exist: (1) from the Dashboard's duplicate suggestions, or (2) from a person's profile via Actions → Merge Profile. Merging requires typing "MERGE THESE PEOPLE" to confirm. **Merging is irreversible** [Source: https://pcopeople.zendesk.com/hc/en-us/articles/115000165267-Merge-duplicate-profiles, Planning Center, current].

What happens during a merge: all contact information and activity across all modules moves from the removed profile to the kept profile. For **checkbox custom fields**, data from both profiles is preserved. For all other custom field types, only the primary profile's data is kept. In Giving, active recurring donations transfer but **saved payment methods do not** — donors must re-add them. The highest permission level between the two profiles is retained. Login methods must match or only one profile can have a login [Source: https://pcopeople.zendesk.com/hc/en-us/articles/115000165267-Merge-duplicate-profiles, Planning Center, current].

There is **no built-in bulk merge** capability. Profiles must be merged one pair at a time. For master record selection, general CRM best practice recommends prioritizing the record with the most recent activity, the most complete data, or the highest-quality source [Source: https://blog.insycle.com/picking-master-record-crm-deduplication, Insycle, 2025].

### Prevention strategies

PCO's official recommendation is to require login on Church Center to prevent duplicates from anonymous interactions. Churches should also: run the Duplicate Detector weekly to prevent pile-up, use the Given Name field correctly to help Giving match donors, and consider Clean My PCO for automated real-time duplicate detection [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360051926993-Prevent-duplicate-profiles, Planning Center, current; https://cleanmypco.com/, Clean My PCO, current].

---

## 6. Inactive and stale record management

### Inactivation versus deletion — the clear consensus

Every source consulted agrees: **always inactivate, never delete**, unless a profile was created accidentally or for testing. PCO's official guidance: "If deleting makes you hesitate, either set the profile to inactive or merge it with another instead of deleting it" [Source: https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile, Planning Center, current]. Deletion is permanent, cannot be undone, disconnects donations from the donor record, and detaches attendance history from any identifiable profile [Source: https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile, Planning Center, current]. Only Organization Administrators can delete profiles.

### What inactivation does

Setting a profile inactive removes the person from groups, declines future service plans, removes team and team leader roles, and removes directory access. However, donation history remains in Giving, payment methods persist, and recurring donations continue (and will automatically reactivate the profile if they process). The exception: deceased profiles have recurring donations set to "On Hold" [Source: https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile, Planning Center, current].

A key feature: **inactive profiles auto-reactivate** if the person completes any Church Center action (giving, registering, checking in), except checking in someone else [Source: https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile, Planning Center, current].

### Defining "inactive" and setting thresholds

Build a "No Recent Activity" auto-refreshing list filtering for profiles with no check-ins, donations, service scheduling, group attendance, or registrations over a defined period [Source: https://churchtechtoday.com/planning-center-clean-up/, ChurchTechToday, February 2022]. The Churchteams help center (principles applicable broadly) suggests **2–3 years of zero activity** as the threshold for archival or inactivation review [Source: https://help.churchteams.com/knowledge/how-do-i-archive-people-and-remove-them-from-the-database, Churchteams, April 2025]. ChurchTechToday suggests **6+ months** for an initial review list, with inactivation after follow-up attempts fail [Source: https://churchtechtoday.com/planning-center-clean-up/, ChurchTechToday, February 2022].

### Data retention considerations

Financial records (giving history) should be retained for a minimum of **7 years** for tax compliance. Children's records should be retained until the child reaches the age of majority plus the applicable statute of limitations. Governing documents should be retained permanently [Source: https://www.councilofnonprofits.org/running-nonprofit/governance-leadership/document-retention-policies-nonprofits, National Council of Nonprofits, current]. For GDPR-subject individuals, PCO allows organization administrators to **permanently delete email addresses, phone numbers, or physical addresses** from the Activity tab while retaining the profile shell for donation and attendance history [Source: https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile, Planning Center, current].

---

## 7. Lists, workflows, and automation for hygiene

### Lists as the backbone of ongoing data quality

PCO Lists filter people based on information and activity **across all Planning Center applications** using rule-based conditions (match all, any, or none). Lists can auto-refresh nightly after 2 AM, ensuring data is always current [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204462530-Lists-overview, Planning Center, current].

PCO officially recommends building a "Profile Cleanup" category of auto-refreshing lists, including: missing gender, no email, no phone number, unknown membership status, no household, unknown grade, children marked as primary contact, blocked email addresses, background checks expiring within 30 days, and no recent activity [Source: https://pcopeople.zendesk.com/hc/en-us/articles/360003006334-Common-lists, Planning Center, current]. Threefold Solutions adds: volunteers in Services who haven't served in 3+ months, and multi-campus profiles without a campus assigned [Source: https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database, Threefold Solutions, May 2024].

### Automation actions from lists

List automations trigger when a list refreshes and a person matches (or stops matching) criteria. Available actions include: send email, add to workflow, set membership type, update custom field values, add Services tags, create a task, and add a background check [Source: https://pcopeople.zendesk.com/hc/en-us/articles/217582148-Automations, Planning Center, current]. Example automations from PCO: "If someone has checked in more than 3 times since January, set their status to 'Member.' When someone donates for the first time, send them to a 'new donors' workflow" [Source: https://www.planningcenter.com/blog/2016/02/list-automations, Planning Center, February 2016].

### Workflows for structured follow-through

A PCO Workflow is a series of user-defined steps that people are walked through — each person's progress is stored in a **card** assigned to a team member. Steps might include "send welcome email," "run background check," or "update membership status." Cards support notes, email sending, overdue notifications, and snoozing for later follow-up [Source: https://www.planningcenter.com/blog/2015/10/introducing-workflows-html, Planning Center, October 2015].

Workflows can be triggered by form submissions, list automations, manual addition, or automations from other PCO apps — PCO supports **22 different automations based on 16 trigger actions** [Source: https://www.planningcenter.com/blog/2018/12/form-automations, Planning Center, December 2018]. For data hygiene specifically, Jared Belcher calls workflows "the most powerful yet overlooked feature of PCO People" and recommends building them for first-time guests, membership applications, new donor thank-yous, and volunteer birthdays [Source: https://www.jared-belcher.com/blog/5-workflow-ideas-for-the-planning-center-people-app, Jared Belcher, 2023–2024].

---

## 8. Cross-module data integrity

### People as the single source of truth

PCO People serves as the **central hub** for the entire Planning Center ecosystem. "All the people you've ever added to any Planning Center app are already in your PCO People account" [Source: https://www.planningcenter.com/people, Planning Center, current]. ChurchTechToday describes this architecture: "Each module integrates with the People module as the central aspect of the overall database. Think of People as the hub and the other modules as the spokes of the wheel" [Source: https://churchtechtoday.com/planning-center-church-management-software-review/, ChurchTechToday, current].

The Activity Feed on each profile aggregates engagement data from every connected module — check-ins, donations, volunteering, event registrations, group membership — into a single chronological timeline [Source: https://www.planningcenter.com/blog/2016/04/activity-feeds-the-story-behind-the-data-html, Planning Center, April 2016].

### Module-specific integration behaviors

**People ↔ Giving:** When a donor gives online for the first time, a new People profile is created automatically. Giving uses name and email to match with existing profiles. If a match fails (different email), a duplicate is created [Source: https://pcogiving.zendesk.com/hc/en-us/articles/360011867633-Manage-donors, Planning Center, current].

**People ↔ Services:** Volunteer/team member profiles in Services link to People records. Scheduling, household scheduling, and permissions all rely on People data [Source: https://pcoservices.zendesk.com/hc/en-us/articles/204261964-Permissions-in-Services, Planning Center, current].

**People ↔ Check-Ins:** Attendance records link to People profiles. Household data enables authorized parent check-in/out of children. Grade and school data drive location assignments [Source: https://www.planningcenter.com/check-ins, Planning Center, current].

**People ↔ Groups:** Group membership and attendance feed back into People. Setting someone inactive in People automatically removes them from all active groups [Source: https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile, Planning Center, current].

### Merge implications across modules

When profiles are merged in People, the merge propagates across every module. Historical data (check-ins, donations, scheduling history) transfers to the surviving record. This makes accurate merging critical — and mistakes irreversible [Source: https://pcopeople.zendesk.com/hc/en-us/articles/115000165267-Merge-duplicate-profiles, Planning Center, current].

### External integration consistency

When integrating PCO with external tools (accounting software, email platforms like Mailchimp, church websites), churches should define which system "wins" for each data field and document data flow maps between PCO modules and external systems. The Church Co's website integration auto-syncs PCO data to church websites, reducing double entry [Source: https://thechurchco.com/planning-center/, The Church Co, November 2024]. PCO provides a unified API covering Calendar, Check-Ins, Giving, Groups, People, and Services [Source: https://developer.planning.center/docs/, Planning Center, current].

---

## 9. Volunteer data management

### The volunteer pipeline in PCO

Planning Center's official blog recommends using **People Workflows combined with Forms** to create a structured volunteer pipeline: each step moves a person from interest expression → screening → training → background check → team assignment in Services [Source: https://www.planningcenter.com/blog/2018/09/volunteer-pipeline, Planning Center, September 2018; https://www.planningcenter.com/blog/2019/04/volunteer-care-and-coordination-for-childrens-ministry, Planning Center, April 2019]. Custom Forms in People collect volunteer applications (contact info, experience, availability), and workflow automations route applicants through the onboarding steps.

At the final workflow step, an automation action can add the person to a Services Team with a specific position (Lead Teacher, Small Group Leader, etc.), completing the pipeline without manual data entry [Source: https://www.planningcenter.com/blog/2018/09/volunteer-pipeline, Planning Center, September 2018].

### Tracking volunteer engagement

Volunteer check-ins — separate from child check-ins — track actual attendance against scheduled status. Threefold Solutions recommends creating a **"Volunteer Check-In"** location in Check-Ins and enabling the Services integration so that when a volunteer checks in and is scheduled in Services for the same date/time, they are automatically marked as "Attended" [Source: https://www.threefold.solutions/blog/maximizing-volunteer-engagement-harnessing-the-power-of-check-ins-in-planning-center, Threefold Solutions, 2024]. A **Services Widget on the People Metrics dashboard** shows scheduled versus attended volunteers over time — consistent or upward trending "attended" data indicates healthy teams [Source: same].

### Inactive volunteer management

Build a PCO list to identify volunteers in Services who haven't served in **3+ months** [Source: https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database, Threefold Solutions, May 2024]. This list can trigger a workflow for pastoral follow-up before removing someone from a team. PCO Services offers a separate archive function that preserves scheduling history, team assignments, and tags while removing the person from active scheduling [Source: https://pcoservices.zendesk.com/hc/en-us/articles/204461040-Archive-remove-and-restore-people, Planning Center, current].

---

## 10. Child safety and background check data

### Integrated background check providers

PCO integrates with three background check providers, each orderable directly from a person's profile:

- **Checkr** — built by PCO; searches databases and courthouse records; returns Clear or Consider results [Source: https://www.planningcenter.com/integrations/checkr, Planning Center, current]
- **Protect My Ministry 2.0** — the newest integration (May 2025) with three default screening packages (Essential, Preferred, Premier), Child Safety Training video add-on, bulk ordering, and automatic security badge updates [Source: https://www.planningcenter.com/blog/2025/05/protect-my-ministry-background-checks-now-in-planning-center, Planning Center, May 2025]
- **MinistrySafe** — training and background checks with enhanced integration as of October 2025 [Source: https://www.planningcenter.com/integrations/ministry-safe, Planning Center, current]

Background check results update the **security badge** on a person's profile (green = clear, red = not clear). A dedicated Background Checks Dashboard in People provides filterable views by status, expiration date, and completion date. For organizations using other providers, manual tracking allows setting status, completion date, expiration date, and notes [Source: https://pcopeople.zendesk.com/hc/en-us/articles/115003728248-Manually-track-background-checks, Planning Center, current].

### Automated expiration and renewal

PCO can **automatically expire background checks** after a configurable age. Build a list with the condition "background check expires within 30 days" and attach an automation to add those people to a renewal workflow [Source: https://www.planningcenter.com/blog/2017/05/better-background-checks-html, Planning Center, May 2017]. In Services, **Secure Teams** only allow people with cleared background checks to be scheduled. People missing checks display a yellow badge in the team's Members tab [Source: https://pcoservices.zendesk.com/hc/en-us/articles/115002760507-Set-up-secure-teams, Planning Center, current].

### Children's data in Check-Ins

Check-Ins tracks child location, authorized pickup via security labels, and attendance by event, grade, and classroom. Custom **name tag labels** can display allergies, medical notes, diaper bag information, birthday, and parent/guardian contact details. Security labels automatically restrict which information appears on parent-facing versus staff-facing labels [Source: https://www.planningcenter.com/check-ins, Planning Center, current]. Grade and school data from People drives automatic classroom/location assignments. Registration requirements can enforce safety form completion and emergency contact entry before a child can check in [Source: same].

### Access controls for child and safety data

Background check access can be granted to specific individuals or permission levels — it is not limited to Organization Administrators [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204462570-Permissions-in-People, Planning Center, current]. Custom field tabs containing sensitive children's data (medical notes, allergy information) should use collaborator-based access control so that only authorized personnel can view the information [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Customize-fields, Planning Center, current].

**Confidence level: High** — all claims in this section come from official PCO documentation.

---

## 11. Giving data hygiene

### Donor record linkage

When a donor gives online for the first time, a People profile is created automatically. For check/cash donations entered via batches, an administrator creates the profile. PCO matches donors to existing People records using name and email — if the email differs, a **duplicate profile is created** [Source: https://pcogiving.zendesk.com/hc/en-us/articles/360011867633-Manage-donors, Planning Center, current]. This makes pre-statement-season duplicate merging essential.

Joint donors receive a single statement when they give jointly and share an address. Only two profiles can be joined. Inactive donors still receive statements for any year they donated, and if a recurring donation processes for an inactive person, their profile auto-reactivates [Source: https://pcogiving.zendesk.com/hc/en-us/articles/360011867633-Manage-donors, Planning Center, current].

### Batch management discipline

Batches track physical donations and external payment sources. The critical workflow rule: **all batches must be committed before generating statements** — uncommitted batches are the most common cause of missing donations on statements [Source: https://www.planningcenter.com/blog/2023/12/giving-statements-tax-receipts-pro-tips-new-updates, Planning Center, December 2023]. Batches should be organized into **Batch Groups** (e.g., "Week of Jan 5 — Cash" and "Week of Jan 5 — Checks"). Uncommitted batches are invisible to donors. System Logs record all committed batch deletions with date, deleting user, and batch name [Source: https://pcogiving.zendesk.com/hc/en-us/articles/205197090-Batches, Planning Center, current].

Permission roles in Giving are specifically designed for financial controls: **Counters** can enter donations to batches but cannot commit them; only **Administrators and Bookkeepers** can commit batches [Source: https://www.planningcenter.com/blog/2020/10/new-permission-levels-in-giving, Planning Center, October 2020].

### Year-end statement preparation checklist

Planning Center's official guidance (January 2025) provides nine essential tips: commit all batches, merge duplicates, verify church name/logo/tax ID in Account Settings, check the deliverability report for donors missing email or mailing addresses, use email statements over print to save costs, verify joint donor linkages, and avoid redundant title wording (e.g., "2024 Giving Statement Statement") [Source: https://www.planningcenter.com/blog/2025/01/year-end-donation-statements-9-essential-tips-for-a-smooth-tax-season, Planning Center, January 2025]. PCO now supports tracking **nondeductible donations** from Donor-Advised Funds and Qualified Charitable Distributions [Source: https://www.planningcenter.com/blog/2024/09/track-nondeductible-donations-in-giving, Planning Center, September 2024].

---

## 12. Permissions, access controls, and audit controls

### PCO's permission hierarchy

**Organization Administrator** is the highest level, with access to all features across all modules including billing, profile deletion, and background check access grants [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204462570-Permissions-in-People, Planning Center, current].

Within People, the hierarchy descends: **Manager** (full editing, field customization, merge access, permissions management) → **Editor** (add/edit people, set inactive, send emails) → **Viewer** (read-only) → **Workflows Only** (can only view and edit assigned workflow cards — designed for volunteers). **Collaborators** have per-resource access to specific lists, workflows, forms, custom field tabs, or note categories [Source: https://pcopeople.zendesk.com/hc/en-us/articles/204462570-Permissions-in-People, Planning Center, current].

Other modules have tailored permission structures. **Giving** uses Administrator, Bookkeeper, and Counter roles — Counters cannot access sensitive donor information [Source: https://www.planningcenter.com/blog/2020/10/new-permission-levels-in-giving, Planning Center, October 2020]. **Groups** includes a Group Type Manager role scoped to specific group types [Source: https://www.planningcenter.com/blog/2021/10/new-permissions-in-groups-group-type-managers, Planning Center, October 2021]. **Services** supports per-folder and per-service-type permissions [Source: https://pcoservices.zendesk.com/hc/en-us/articles/204261964-Permissions-in-Services, Planning Center, current].

### Export controls (new in 2025)

A new granular **"Can export CSVs and reports"** permission setting allows administrators to control which Viewers and Editors can export sensitive data — preventing unauthorized bulk data extraction [Source: https://www.planningcenter.com/blog/2025/02/5-new-features-you-may-have-missed-in-people, Planning Center, February 2025].

### Audit trail capabilities

PCO provides several audit mechanisms, though not a comprehensive field-level change log. **Activity Feeds** on each profile show a chronological timeline of engagement across all modules — check-ins, donations, registrations, group joins, and profile changes [Source: https://www.planningcenter.com/blog/2016/04/activity-feeds-the-story-behind-the-data-html, Planning Center, April 2016]. **Security History** logs every login-related event with user name, IP address, timestamp, email, phone, and operating system data — accessible to Organization Administrators [Source: https://www.planningcenter.com/blog/2023/04/respond-to-potential-data-breaches-with-the-new-account-security-history-page, Planning Center, April 2023]. Giving System Logs record committed batch deletions. Automation traceability (new in 2025) links workflow cards back to their triggering automation [Source: https://www.planningcenter.com/blog/2025/02/5-new-features-you-may-have-missed-in-people, Planning Center, February 2025].

**Confidence level: Medium** — PCO does not appear to offer a comprehensive field-level audit trail logging every change with before/after values. The Activity tab logs some profile modifications, but Planning Center Community forums contain requests for more complete activity logging across modules, suggesting this is a known gap.

---

## 13. Privacy, retention, and legal considerations

### U.S. privacy law landscape for churches

Churches are **generally exempt from CCPA** (California), which applies only to for-profit entities [Source: https://www.churchlawcenter.com/nonprofit/what-nonprofits-need-to-know-about-the-california-consumer-privacy-act-ccpa/, Church Law Center of California, April 2020]. However, the **Colorado Privacy Act does NOT exempt nonprofits** — any legal entity meeting processing thresholds must comply [Source: https://www.whitefordlaw.com/news-events/client-alert-state-privacy-laws-and-non-profit-organizations, Whiteford Law, 2023]. Connecticut exempts 501(c)(3) organizations. State laws vary significantly in their definitions of exempt entities.

Critically, even when a church is exempt, **Planning Center itself (as a for-profit service provider) must comply** with applicable privacy laws [Source: https://www.whitefordlaw.com/news-events/client-alert-state-privacy-laws-and-non-profit-organizations, Whiteford Law, 2023]. Legal commentators unanimously recommend that churches adopt privacy best practices proactively: "It is reasonable to expect members, donors, and consumers to look for more access, control, and transparency into how their data is used, regardless of the nature or type of organization" [Source: same].

### GDPR considerations

Under GDPR, **religious belief is classified as "special category data"** requiring heightened protection. Churches with any EU-resident members must comply. Required measures include: privacy notices, informed consent, written contracts with data processors (like PCO), response to Subject Access Requests within one month, and regular data audits [Source: https://vinciworks.com/blog/data-protection-for-churches/, VinciWorks, 2024]. Faith-based nonprofits are explicitly **not exempt** from GDPR [Source: https://www.lexology.com/library/detail.aspx?g=1f076139-c8e0-496f-afe4-0df39a1d42cc, Lexology / Bradley Arant, current].

### Retention schedule framework

The National Council of Nonprofits notes that IRS Form 990 asks whether the organization has a written record retention policy, and the IRS generally requires financial records for at least **3 years** (many advisors recommend 7) [Source: https://www.councilofnonprofits.org/running-nonprofit/governance-leadership/document-retention-policies-nonprofits, National Council of Nonprofits, current]. Organizations serving minors should retain certain records until the child reaches the age of majority plus the applicable statute of limitations [Source: same].

A practical PCO retention schedule matrix:

- **Giving records:** 7 years minimum (tax compliance)
- **Active member profiles:** Indefinite while active
- **Inactive member profiles:** Archive review after 3–5 years of zero activity
- **Children's records:** Until age 21+ (majority plus buffer)
- **Background check records:** Per state law (typically 5–7 years)
- **Attendance logs:** 3–5 years
- **Governing documents:** Permanent

[Source: Synthesized from https://www.councilofnonprofits.org/running-nonprofit/governance-leadership/document-retention-policies-nonprofits, National Council of Nonprofits, current; https://www.goodunited.io/blog/data-retention-policy-guide, GoodUnited, 2024]

### Data minimization and the stewardship frame

The relationship between church leadership and members is grounded in trust. Members share "some of the most sacred and private details of their lives" — a data privacy policy should be developed as an expression of pastoral care, not just legal compliance [Source: https://www.lexology.com/library/detail.aspx?g=1f076139-c8e0-496f-afe4-0df39a1d42cc, Lexology / Bradley Arant, current]. PCO's GDPR-aware feature allows administrators to permanently delete specific contact information (email, phone, address) from the Activity tab while retaining the profile shell for donation and attendance history [Source: https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile, Planning Center, current].

---

## 14. Staff training and onboarding standards

### Building a training program

CDS Funds identifies the essential components: **hands-on workshops, ongoing support resources, and a knowledge-sharing platform** [Source: https://cdsfunds.com/nonprofit-crm-data-best-practices, CDS Funds, 2024]. NTEN recommends matching the learning environment to the application environment — practice on the real PCO system rather than slides or screenshots — and adapting to various learning styles with multiple modes (watching, reading, practicing, reflecting) [Source: https://www.nten.org/blog/developing-staff-technology-skills-in-your-nonprofit, NTEN, 2023].

Concordia Technology Solutions advises breaking training into **short, topical sessions**: one session for membership and attendance, another for financial tracking, another for check-in procedures [Source: https://www.concordiatechnology.org/blog/how-to-train-staff-on-new-church-management-software, Concordia Technology Solutions, current]. When transitioning from another system, maintain the old system in parallel during migration for data verification, then schedule a firm final migration day on a low-urgency work day [Source: same].

### Role-based training tracks

Training should be segmented by role, not delivered as one-size-fits-all. Recommended tracks for PCO:

- **Front desk/reception staff:** Data entry in People, Check-In operation, new visitor forms
- **Ministry leaders:** Group management, attendance tracking, list creation
- **Finance team:** Giving batches, fund management, statement generation, Counter vs. Bookkeeper roles
- **Pastoral staff:** People notes, workflows, privacy-sensitive custom tabs
- **Volunteer coordinators:** Services scheduling, background check ordering, volunteer pipeline workflows
- **All users:** Duplicate awareness, naming conventions, when to inactivate vs. delete

[Source: Synthesized from https://www.pairsoft.com/blog/how-to-guarantee-your-nonprofit-crm-data-is-accurate/, PairSoft, 2024; https://www.nicheacademy.com/blog/tech-training-for-nonprofit-staff, Niche Academy, 2025]

### Documentation and accountability

Churches should create and maintain a **PCO Data Entry Guide** (a written SOP document). Key question to ask before adding any data field: "Does this information support my congregation's mission?" [Source: https://www.concordiatechnology.org/blog/2016/02/how-to-maintain-a-useful-church-database, Concordia Technology Solutions, February 2016]. Designate one person as the database point person with final decision authority on data-related questions. Avoid the single-point-of-failure problem by cross-training at least two people for every critical function [Source: https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database, Threefold Solutions, May 2024].

As of September 2025, PCO allows congregants to self-update appropriate custom fields via Church Center, shifting some data maintenance burden to members themselves. PCO recommends running **2–3 communication rounds** to encourage profile updates, using direct links to the profile editing page [Source: https://www.planningcenter.com/blog/2025/09/no-more-form-fatigue-let-people-edit-their-own-information-in-church-center, Planning Center, September 2025].

---

## 15. Cleanup cadence and review schedule

### Recommended maintenance calendar

Multiple PCO-certified consultants converge on a tiered maintenance cadence. Threefold Solutions provides the most specific framework [Source: https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database, Threefold Solutions, May 2024]:

**Weekly (15–30 minutes, "Monday morning meeting with your database"):**
- Review and resolve Duplicate Detector suggestions
- Review new profiles created in the past week; verify membership type is assigned
- Check auto-refreshing cleanup lists for incomplete data (missing email, phone, gender)
- Process workflow cards assigned to you

**Monthly (1–3 hours):**
- Deep dive into engagement levels and attendance patterns
- Verify member contact info currency (spot-check a subset)
- Review blocked email addresses list and take corrective action
- Check background check expiration list (30-day window)
- Review inactive volunteer list (3+ months without serving)

**Quarterly:**
- Archive completed or outdated sign-up forms and event registrations
- Update group information (close ended groups, archive inactive ones)
- Review list relevance — delete or update stale lists and saved reports
- Audit custom fields for unused or redundant fields
- Review permissions — remove access for departed staff or rotated volunteers

**Annually:**
- Comprehensive inactive member review — process all profiles with 12+ months of zero activity through a follow-up workflow before inactivating
- Year-end giving statement preparation: commit all batches, merge duplicates, verify organization info, check deliverability report, generate and send statements [Source: https://www.planningcenter.com/blog/2025/01/year-end-donation-statements-9-essential-tips-for-a-smooth-tax-season, Planning Center, January 2025]
- Grade promotion for children's ministry (one-click in PCO Check-Ins, typically August)
- Full database audit: run every cleanup list, review custom field usage, assess data governance policy compliance
- Review and update the written Data Entry Guide and training materials
- Conduct refresher training for all staff with database access

**Seasonal peaks:**
- **Pre-Easter/Pre-Christmas:** Prepare for visitor influx — ensure new visitor workflow and connect card form are functioning; verify Check-In configurations
- **Pre-VBS/Summer:** Update children's grade data, allergy info, emergency contacts; verify background checks for all summer volunteers
- **Back-to-school (August/September):** Grade promotions, update school information, refresh children's ministry teams

Bloomerang's general nonprofit guidance supports this tiered model, recommending weekly quick checks (15 minutes), weekly maintenance (1 hour), and monthly deep cleans (3+ hours) for databases with **10,000+ records** [Source: https://bloomerang.com/blog/crm-cleanup-tasks-for-donor-data/, Bloomerang, 2025].

ChurchTechToday summarizes the overarching philosophy: "There is only one way to eat an elephant: a bite at a time." Break initial cleanup into manageable phases, then establish ongoing maintenance routines [Source: https://churchtechtoday.com/planning-center-clean-up/, ChurchTechToday, February 2022].

---

## Conclusion

Effective PCO database management rests on three pillars. First, **governance before technology**: assign clear ownership roles, write data entry standards, and train staff by role before configuring a single automation. Second, **inactivate, never delete**: every source consulted — official PCO documentation, church-tech consultants, and nonprofit CRM experts — agrees that profile inactivation preserves historical integrity while PCO's auto-reactivation feature handles the return path gracefully. Third, **automate the tedious, humanize the judgment**: use auto-refreshing lists and workflow automations for detection and routing, but reserve merge decisions, pastoral follow-up, and privacy-sensitive actions for trained humans.

The most actionable insight from this research is the power of PCO's Lists-to-Workflows pipeline as a self-healing data quality system. A well-configured set of cleanup lists running nightly, connected to workflows that route issues to the right people, transforms database maintenance from a dreaded quarterly chore into an ambient, continuously-running process. Combined with congregant self-service profile editing (new in 2025), this approach distributes the maintenance burden across the entire church community rather than concentrating it on a single administrator.

Churches operating in Colorado should note they may not be exempt from state privacy laws despite their nonprofit status — a frequently overlooked legal consideration. And every church, regardless of jurisdiction, should develop a data privacy policy framed as an extension of pastoral care and stewardship of trust, not merely legal compliance.

---

## Source index

| # | Source Title | URL | Publisher | Date | Relevance |
|---|---|---|---|---|---|
| 1 | Profile overview | https://pcopeople.zendesk.com/hc/en-us/articles/204263114-Profile-overview | Planning Center | Current | Default fields, name conventions, profile structure |
| 2 | Customize fields | https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Customize-fields | Planning Center | Current | Custom fields, tabs, field types, permissions |
| 3 | Households | https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households | Planning Center | Current | Household structure, roles, primary contacts |
| 4 | Parent and guardian household roles | https://www.planningcenter.com/changelog/people/new-parent-guardian-household-roles | Planning Center | Current | New household role types |
| 5 | Merge duplicate profiles | https://pcopeople.zendesk.com/hc/en-us/articles/115000165267-Merge-duplicate-profiles | Planning Center | Current | Merge process, data handling, irreversibility |
| 6 | Prevent duplicate profiles | https://pcopeople.zendesk.com/hc/en-us/articles/360051926993-Prevent-duplicate-profiles | Planning Center | Current | Duplicate prevention strategies |
| 7 | The New Duplicate Detector | https://www.planningcenter.com/blog/duplicate-detector | Planning Center | Current | ML-based duplicate detection, accuracy improvements |
| 8 | Lists overview | https://pcopeople.zendesk.com/hc/en-us/articles/204462530-Lists-overview | Planning Center | Current | List rules, conditions, auto-refresh |
| 9 | Common lists | https://pcopeople.zendesk.com/hc/en-us/articles/360003006334-Common-lists | Planning Center | Current | Recommended cleanup list examples |
| 10 | Automations | https://pcopeople.zendesk.com/hc/en-us/articles/217582148-Automations | Planning Center | Current | List automation actions and triggers |
| 11 | Introducing Workflows | https://www.planningcenter.com/blog/2015/10/introducing-workflows-html | Planning Center | October 2015 | Workflow structure, cards, steps (older but foundational) |
| 12 | Permissions in People | https://pcopeople.zendesk.com/hc/en-us/articles/204462570-Permissions-in-People | Planning Center | Current | Permission hierarchy and role definitions |
| 13 | Inactivate or delete a profile | https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile | Planning Center | Current | Inactivation effects, deletion consequences, GDPR feature |
| 14 | Manage membership | https://pcopeople.zendesk.com/hc/en-us/articles/360013192194-Manage-membership | Planning Center | Current | Membership types, inactive reasons, customization |
| 15 | Manage donors | https://pcogiving.zendesk.com/hc/en-us/articles/360011867633-Manage-donors | Planning Center | Current | Donor record creation, matching, joint donors |
| 16 | Batches | https://pcogiving.zendesk.com/hc/en-us/articles/205197090-Batches | Planning Center | Current | Batch workflow, commitment, system logs |
| 17 | Giving statements & tax receipts: pro tips | https://www.planningcenter.com/blog/2023/12/giving-statements-tax-receipts-pro-tips-new-updates | Planning Center | December 2023 | Statement preparation best practices |
| 18 | Year-end donation statements: 9 essential tips | https://www.planningcenter.com/blog/2025/01/year-end-donation-statements-9-essential-tips-for-a-smooth-tax-season | Planning Center | January 2025 | Year-end checklist |
| 19 | Protect My Ministry background checks | https://www.planningcenter.com/blog/2025/05/protect-my-ministry-background-checks-now-in-planning-center | Planning Center | May 2025 | PMM 2.0 integration, bulk ordering, security badges |
| 20 | Set up secure teams | https://pcoservices.zendesk.com/hc/en-us/articles/115002760507-Set-up-secure-teams | Planning Center | Current | Background check enforcement for scheduling |
| 21 | Security History page | https://www.planningcenter.com/blog/2023/04/respond-to-potential-data-breaches-with-the-new-account-security-history-page | Planning Center | April 2023 | Login audit trail |
| 22 | 5 new features in People | https://www.planningcenter.com/blog/2025/02/5-new-features-you-may-have-missed-in-people | Planning Center | February 2025 | Export permissions, automation traceability |
| 23 | No more form fatigue | https://www.planningcenter.com/blog/2025/09/no-more-form-fatigue-let-people-edit-their-own-information-in-church-center | Planning Center | September 2025 | Congregant self-service profile editing |
| 24 | The all-new donation form | https://www.planningcenter.com/blog/2025/09/the-all-new-donation-form | Planning Center | 2025 | Phone verification to reduce duplicate donors |
| 25 | New permission levels in Giving | https://www.planningcenter.com/blog/2020/10/new-permission-levels-in-giving | Planning Center | October 2020 | Counter, Bookkeeper, Administrator roles |
| 26 | 5 Planning Center Clean-Up Tips | https://churchtechtoday.com/planning-center-clean-up/ | ChurchTechToday | February 2022 | PCO-specific cleanup strategies |
| 27 | Ultimate Guide to Streamlining Your PCO Database | https://www.threefold.solutions/blog/the-ultimate-guide-to-streamlining-your-planning-center-people-database | Threefold Solutions | May 2024 | Maintenance cadence, cleanup lists, PCO Champions |
| 28 | Planning Center People Cleanup in 3 Easy Steps | https://digitaloutreach.com/blog/planning-center-people-cleanup | Digital Outreach | Current | Progressive data collection, membership tiers |
| 29 | From Attenders to Members: Tracking Milestones | https://www.threefold.solutions/blog/from-attenders-to-members-tracking-membership-milestones-in-planning-center-people | Threefold Solutions | 2024 | Custom fields for membership tracking |
| 30 | Maximize Volunteer Engagement with Check-Ins | https://www.threefold.solutions/blog/maximizing-volunteer-engagement-harnessing-the-power-of-check-ins-in-planning-center | Threefold Solutions | 2024 | Volunteer check-in and engagement tracking |
| 31 | Clean My PCO | https://cleanmypco.com/ | Clean My PCO | Current | Automated real-time data cleaning integration |
| 32 | 10 Workflow Ideas for PCO People | https://www.jared-belcher.com/blog/5-workflow-ideas-for-the-planning-center-people-app | Jared Belcher | 2023–2024 | Workflow use cases for data hygiene |
| 33 | Planning Center integration | https://thechurchco.com/planning-center/ | The Church Co | November 2024 | Website-PCO sync to reduce double entry |
| 34 | CRM Cleanup Tasks | https://bloomerang.com/blog/crm-cleanup-tasks-for-donor-data/ | Bloomerang | 2025 | Tiered cleanup schedule for nonprofits |
| 35 | Nonprofit Data Management | https://www.ccsfundraising.com/insights/nonprofit-data-management/ | CCS Fundraising | 2025 | Data maturity stages, common quality issues |
| 36 | 4 Best Practices for Nonprofit CRM Data | https://cdsfunds.com/nonprofit-crm-data-best-practices | CDS Funds | 2024 | Data audit, standardization, training essentials |
| 37 | Nonprofit CRM Best Practices | https://altrata.com/articles/nonprofit-crm-best-practices | Altrata | 2025 | KPIs, governance policy, interoperability |
| 38 | Nonprofit Data Governance Toolkit | https://nethope.org/toolkits/data-governance-toolkit-a-guide-to-implementing-data-governance-in-nonprofits/ | NetHope | April 2022 | DMBOK-based governance framework for nonprofits |
| 39 | Data Governance: What It Is and Why You Need It | https://www.brightvinesolutions.com/post/data-governance-what-it-is-and-why-you-need-it-part-1 | BrightVine Solutions | January 2022 | Governance roles for nonprofits |
| 40 | CRM Deduplication: Picking the Right Master Record | https://blog.insycle.com/picking-master-record-crm-deduplication | Insycle | 2025 | Master record selection criteria |
| 41 | What Nonprofits Need to Know About CCPA | https://www.churchlawcenter.com/nonprofit/what-nonprofits-need-to-know-about-the-california-consumer-privacy-act-ccpa/ | Church Law Center of California | April 2020 | CCPA nonprofit exemption, children's data |
| 42 | State Privacy Laws and Nonprofit Organizations | https://www.whitefordlaw.com/news-events/client-alert-state-privacy-laws-and-non-profit-organizations | Whiteford Law | 2023 | Colorado non-exemption, state-by-state variations |
| 43 | Data Protection for Churches | https://vinciworks.com/blog/data-protection-for-churches/ | VinciWorks | 2024 | GDPR requirements for churches |
| 44 | Privacy and Faith-Based Institutions | https://www.lexology.com/library/detail.aspx?g=1f076139-c8e0-496f-afe4-0df39a1d42cc | Lexology / Bradley Arant | Current | Stewardship framing of data privacy |
| 45 | Document Retention Policies for Nonprofits | https://www.councilofnonprofits.org/running-nonprofit/governance-leadership/document-retention-policies-nonprofits | National Council of Nonprofits | Current | IRS requirements, retention schedules, minors' data |
| 46 | Data Retention Policy: A Guide for Nonprofits | https://www.goodunited.io/blog/data-retention-policy-guide | GoodUnited | 2024 | Retention schedule design, cross-functional teams |
| 47 | Developing Staff Technology Skills | https://www.nten.org/blog/developing-staff-technology-skills-in-your-nonprofit | NTEN | 2023 | Micro-training, reinforcement intervals |
| 48 | Tech Training for Nonprofit Staff | https://www.nicheacademy.com/blog/tech-training-for-nonprofit-staff | Niche Academy | 2025 | Champions, sandbox practice, role segmentation |
| 49 | How to Maintain a Useful Church Database | https://www.concordiatechnology.org/blog/2016/02/how-to-maintain-a-useful-church-database | Concordia Technology Solutions | February 2016 | Data entry standards, mission-driven field selection (older but authoritative) |
| 50 | How to Train Staff on New Church Management Software | https://www.concordiatechnology.org/blog/how-to-train-staff-on-new-church-management-software | Concordia Technology Solutions | Current | Topical training sessions, parallel systems during migration |
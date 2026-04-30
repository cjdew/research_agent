# PCO-Best-Practices-Reference

## Scope and method
This reference consolidates current best practices for Planning Center Online database management, with emphasis on People as the system-of-record across Planning Center products. It is organized by topic area rather than by source.

**Research date:** 2026-04-15  
**Source priority used:** Official Planning Center sources first, then recent specialist church-tech sources where useful, then broader nonprofit/CRM governance guidance.  
**Important limitation:** This document is a research reference only. It is not a live audit of Mosaic Wadsworth’s Planning Center account.

---

## 1. Core governance model

### Consensus
- Treat **People** as the primary person record because Planning Center positions it as the hub for profile information and cross-product activity.
- Define a **small set of required fields** that must be complete for every active person record.
- Assign clear ownership for:
  - field design,
  - list/workflow maintenance,
  - duplicate review,
  - inactive-profile review,
  - permissions,
  - integration monitoring.
- Prefer **documented rules and controlled vocabularies** over freeform entry.

### What applies directly to PCO
- Planning Center explicitly describes People as the central hub for profile and cross-product information.
- Membership types, inactive reasons, custom tabs/fields, lists, workflows, bulk actions, and automations should be treated as governed system components, not ad hoc admin conveniences.

### PCO-specific practice
- Use built-in fields whenever they fit the need.
- Use custom fields only when the information is truly church-specific and operationally useful.
- Limit who can create or edit custom fields and their permissions.

### General CRM practice
- Create a written data dictionary.
- Define owners for each critical field and process.
- Review governance quarterly.

---

## 2. Minimum viable record design

### Consensus
For active people, the minimum usable profile usually includes:
- preferred/given name structure,
- at least one reliable contact method,
- household linkage when applicable,
- campus or primary congregation context where relevant,
- lifecycle or membership status,
- basic role/engagement markers needed for communication and care.

### What applies directly to PCO
- PCO includes default profile/contact fields and supports membership type, inactive reason, campus, household roles, and custom fields.
- Churches should distinguish between:
  - truly required profile data,
  - nice-to-have enrichment data,
  - restricted pastoral/sensitive data.

### PCO-specific practice
- Keep the required field set small.
- Put optional ministry-specific details in carefully designed custom tabs/fields.
- Expose only selected fields in Church Center for self-service editing.

### General CRM practice
- Avoid over-collecting data that is not used in reporting, care, safety, communication, or compliance.
- Periodically remove unused fields.

---

## 3. Household strategy

### Consensus
- Household design must be intentional because it affects communication, registrations, check-ins, and family visibility.
- Household relationships should reflect real operational needs, not just postal conventions.
- Adults/guardians with household authority should be clearly distinguished from children/dependents.

### What applies directly to PCO
- PCO allows people to belong to multiple households.
- Household roles directly affect Church Center editing, registrations, check-ins, and some scheduling behavior.

### PCO-specific practice
- Standardize when to create, split, merge, or update households.
- Audit for:
  - duplicate households,
  - children without guardians,
  - separated adults still grouped incorrectly,
  - adults incorrectly labeled as children/dependents,
  - households with stale addresses or no common contact pattern.

### General CRM practice
- Define one church-wide rule set for household formation and exceptions.
- Use periodic household review, especially after major events, check-ins, or membership processes.

---

## 4. Membership and lifecycle taxonomy

### Consensus
- Membership status should not be binary unless the church truly operates that way.
- Distinguish:
  - member vs non-member,
  - active vs inactive,
  - attendee/guest/regular/volunteer/leader where useful,
  - inactive reason where relevant.
- Statuses should support actual ministry decisions, not just historical labeling.

### What applies directly to PCO
- PCO supports customizable membership types and inactive reasons.
- PCO recommends setting profiles inactive rather than deleting real people.

### PCO-specific practice
- Create a small, plain-language membership taxonomy.
- Create inactive reasons with operational value, such as moved, deceased, requested removal, duplicate merged, no recent engagement under policy, etc.
- Use bulk actions and list-driven review for status normalization.

### General CRM practice
- Every status should have:
  - a definition,
  - who can assign it,
  - what triggers it,
  - what follow-up it causes.

---

## 5. Duplicate management and merge policy

### Consensus
- Duplicate prevention is better than duplicate cleanup.
- Duplicate candidates must be reviewed, not blindly merged.
- A merge policy should define which profile becomes primary and how conflicts are resolved.

### What applies directly to PCO
- PCO has a duplicate detector and manual merge workflow.
- PCO warns that merges are irreversible.
- PCO preserves many cross-product histories in merges, but for single-value fields the primary record’s value is retained.

### PCO-specific practice
- Review duplicates on a cadence, not only during crises.
- Before merging, compare:
  - login method,
  - primary contact details,
  - household placement,
  - membership status,
  - background checks,
  - donation history context,
  - permissions.
- Use the profile with the most accurate single-value fields as the primary record.

### General CRM practice
- Document exact merge rules.
- Track merge volume and duplicate trends by source.
- Focus prevention on imports, forms, registrations, and donor creation points.

---

## 6. Inactive, archived, and deleted records

### Consensus
- Do not delete real constituent records unless they are obvious errors or test data.
- Preserve history when someone leaves, becomes inactive, or changes role.

### What applies directly to PCO
- PCO explicitly recommends inactivating real people instead of deleting them because deletion removes history across products.
- This matters for giving, attendance, scheduling, registrations, and permissions.

### PCO-specific practice
- Use inactivation as the default action for departed people.
- Only delete:
  - test data,
  - accidental empty shells,
  - immediately-created errors that carry no useful history.
- Review staff-transition implications before inactivating staff/admin users.

### General CRM practice
- Have a written retention and deletion standard.
- Separate “not active in ministry” from “safe to delete.”

---

## 7. Custom field design

### Consensus
- Custom fields are valuable, but field sprawl is one of the fastest ways to degrade trust in the database.
- Each custom field should have a named purpose, owner, allowable values, and downstream use.

### What applies directly to PCO
- PCO supports custom tabs/fields, collaborator permissions, form usage, lists, reports, automations, and Church Center visibility.
- PCO also provides examples of common custom-field uses.

### PCO-specific practice
Before creating a custom field, confirm:
1. A built-in field does not already cover the need.
2. The field supports a real workflow, report, list, or decision.
3. The answer format is controlled where possible.
4. The field has an owner.
5. A retirement plan exists if the field becomes obsolete.

### Strong PCO patterns
- Use dates for milestones.
- Use dropdowns or yes/no for controlled states.
- Use checkboxes only when multi-select is genuinely needed.
- Restrict sensitive tabs to the minimum necessary collaborators.
- Avoid using free-text fields for information that needs reporting.

### General CRM practice
- Review all custom fields at least annually for:
  - usage,
  - completeness,
  - overlap,
  - stale definitions,
  - privacy risk.

---

## 8. Lists, workflows, and automations as hygiene infrastructure

### Consensus
- Database hygiene is not just about cleanup. It requires continuous exception monitoring.
- Dynamic lists, workflows, and automations are central to sustainable database health.

### What applies directly to PCO
- PCO lists can filter on profile data and activity across Planning Center products.
- Lists can auto-refresh.
- Workflows track multi-step processes.
- Automations can update fields, create tasks, send communication, and add people to workflows.

### PCO-specific practice
Create standing hygiene lists for:
- possible duplicates,
- active people missing email and phone,
- households with children but no guardian,
- active volunteers with expired or missing background checks,
- active donors with unmatched/incomplete contact data,
- people with no activity in policy-defined periods,
- stale workflow cards,
- records missing campus or lifecycle status.

### Important PCO caution
- PCO warns against automation setups that depend on auto-refreshing lists built from other lists unless the upstream refresh is controlled.

### General CRM practice
- Turn recurring data exceptions into monitored reports or queues, not one-off projects.

---

## 9. Volunteer and child-safety data

### Consensus
- Volunteer data must support placement, follow-up, and compliance.
- Child/youth-facing roles require especially careful background-check and eligibility tracking.
- Sensitive safety data should be minimized and permissioned tightly.

### What applies directly to PCO
- PCO supports Checkr integration and manual background-check tracking.
- Background checks can be added by bulk action or automation.
- Email is needed for the built-in Checkr request flow.

### PCO-specific practice
Track, at minimum, for safety-sensitive roles:
- background check status,
- completion date,
- expiration date,
- role eligibility / ministry approval state,
- any required training completion markers.

### General CRM practice
- Store only the minimum necessary screening metadata in the main CRM.
- Keep detailed reports or sensitive source documents outside broad-access profile surfaces when possible.
- Review expiration-driven compliance lists on a fixed cadence.

---

## 10. Donor data hygiene

### Consensus
- Donor records should resolve to one person whenever possible.
- Giving history, recurring gifts, receipting contacts, and donor identity should be checked carefully during duplicate review.
- Nickname and preferred-name inconsistencies are a common duplicate source.

### What applies directly to PCO
- PCO Giving can match donor information to existing People profiles.
- PCO’s donor guidance notes nickname handling as a duplicate-prevention issue.
- Merges retain donation history, but contact info on the primary profile affects receipting.

### PCO-specific practice
- Periodically review donor profiles that are:
  - missing People linkage,
  - missing reliable email,
  - likely duplicates,
  - attached to inactive people without a known reason,
  - using inconsistent naming conventions.

### General CRM practice
- Treat receipting/contact data as high-trust data.
- Audit recurring-gift records after donor merges or email changes.

---

## 11. Permissions, privacy, and least privilege

### Consensus
- Churches should default to least privilege.
- Sensitive pastoral, child-safety, financial, and administrative information should be segmented.
- Audit controls should include both who can see data and who can change structure.

### What applies directly to PCO
- PCO allows collaborator controls on custom tabs/fields and role-based permissions across products.
- Some custom-field content can be hidden in lists/forms/notifications for non-collaborators.

### PCO-specific practice
- Separate permission to edit data from permission to design fields/processes.
- Review who can:
  - manage custom fields,
  - run bulk actions,
  - merge profiles,
  - manage lists/automations,
  - access background checks,
  - access donor data.

### General CRM practice
- Run permission reviews after staffing changes and at least semiannually.
- Avoid storing highly sensitive notes broadly unless clearly justified and protected.

---

## 12. Data entry normalization

### Consensus
- Standardization is essential for trusted reporting.
- Picklists beat free text whenever reporting or segmentation matters.

### Recommended normalization areas
- campus names,
- membership statuses,
- inactive reasons,
- school names/grades,
- phone/email formatting,
- household role patterns,
- volunteer approval states,
- donor naming conventions,
- training completion states.

### What applies directly to PCO
- PCO supports customizable default-field options, custom field types, bulk actions, and imports with specific formatting requirements.

### General CRM practice
- Publish a short admin entry standard.
- Train staff and key volunteers who touch records.
- Use imports carefully and validate before/after.

---

## 13. Cleanup cadence

### Consensus
A recurring cadence outperforms occasional large cleanup projects.

### Suggested cadence
**Weekly**
- review duplicate detector,
- review failed or stalled workflows,
- review urgent background-check exceptions,
- review automation failures or odd outputs.

**Monthly**
- review incomplete active profiles,
- review new custom fields and new lists created,
- review stale volunteers / stale groups of records,
- review donor matching exceptions.

**Quarterly**
- review inactive logic and archive candidates,
- review permission assignments,
- review household anomalies,
- review integrations and sync assumptions.

**Annually**
- review custom-field inventory,
- review lifecycle taxonomy,
- review retention/deletion policy,
- review staff training and SOPs.

---

## 14. Sampling and audit design for a live PCO audit

When a full-database analysis is not practical, use a stratified sample rather than convenience sampling.

### Recommended people-record sample strata
- adults and children,
- active and inactive,
- volunteers and non-volunteers,
- donors and non-donors,
- recently updated and stale records.

### Recommended object categories for targeted review
- custom fields,
- lists,
- workflows,
- automations,
- households,
- background check records,
- donor match exceptions,
- permissions by product.

---

## 15. Meaningful disagreement in sources

### Where agreement is strong
- avoid deleting real records,
- use People as the hub,
- review duplicates routinely,
- standardize fields and statuses,
- use dynamic segmentation/lists,
- keep field design disciplined,
- train staff.

### Where disagreement or variation exists
- exact membership taxonomy,
- how granular custom fields should become,
- how much volunteer/process state should be stored in fields versus workflows,
- how aggressively to expose self-service editing in Church Center.

### Practical conclusion
These are local governance decisions, not universal technical truths. Mosaic should decide them explicitly and document them.

---

## 16. Source register

| Source | Publisher | Date published/updated | Accessed | Relevance |
|---|---|---:|---:|---|
| https://www.planningcenter.com/people | Planning Center | crawled 2026 | 2026-04-15 | Confirms People as the central hub, plus lists, workflows, automations, background checks, and cross-product activity. |
| https://pcopeople.zendesk.com/hc/en-us/articles/360019525293-People-The-Planning-Center-Hub | Planning Center | Updated 2025-10-02 | 2026-04-15 | States that People is the hub for all Planning Center products. |
| https://pcopeople.zendesk.com/hc/en-us/articles/360013192194-Manage-membership | Planning Center | Updated 2025-10-02 | 2026-04-15 | Official guidance on membership types and inactive reasons. |
| https://pcopeople.zendesk.com/hc/en-us/articles/115000165267-Merge-duplicate-profiles | Planning Center | Updated 2025-12-16 | 2026-04-15 | Official duplicate and merge behavior, including cross-product effects and irreversible merge warning. |
| https://pcopeople.zendesk.com/hc/en-us/articles/360051926993-Prevent-duplicate-profiles | Planning Center | Updated 2025-12-04 | 2026-04-15 | Official duplicate-prevention guidance across forms, groups, registrations, and giving. |
| https://pcopeople.zendesk.com/hc/en-us/articles/360013131054-Households | Planning Center | Updated 2026-01-26 | 2026-04-15 | Official household model and role implications. |
| https://pcopeople.zendesk.com/hc/en-us/articles/227840007-Inactivate-or-delete-a-profile | Planning Center | Updated 2026-01-06 | 2026-04-15 | Official guidance to inactivate rather than delete real people. |
| https://pcopeople.zendesk.com/hc/en-us/articles/204263134-Customize-fields | Planning Center | Updated 2025-12-17 | 2026-04-15 | Official custom field design, permissions, bulk update, and import formatting guidance. |
| https://pcopeople.zendesk.com/hc/en-us/articles/21774202414747-Common-uses-for-custom-fields | Planning Center | Updated 2025-10-02 | 2026-04-15 | Examples of productive custom-field use cases. |
| https://pcopeople.zendesk.com/hc/en-us/articles/204462530-Lists-overview | Planning Center | Updated 2026-01-22 | 2026-04-15 | Official list behavior, sharing, refresh, and automation context. |
| https://pcopeople.zendesk.com/hc/en-us/articles/217582148-Automations | Planning Center | Updated 2026-02-11 | 2026-04-15 | Official automation behavior and dependency caution. |
| https://pcopeople.zendesk.com/hc/en-us/articles/212268708-Workflow-overview | Planning Center | Updated 2025-09-05 | 2026-04-15 | Official workflow structure and permissions. |
| https://pcopeople.zendesk.com/hc/en-us/articles/216711507-Update-People-with-Bulk-Actions | Planning Center | Updated 2025-10-09 | 2026-04-15 | Official bulk action capabilities for normalization and cleanup. |
| https://pcopeople.zendesk.com/hc/en-us/articles/115003300627-Using-Checkr-for-background-checks | Planning Center | Updated 2025-10-02 | 2026-04-15 | Official integrated background-check workflow guidance. |
| https://pcopeople.zendesk.com/hc/en-us/articles/115003728248-Manually-Track-Background-Checks | Planning Center | Updated 2025-10-02 | 2026-04-15 | Official manual background-check tracking guidance, including bulk action and automation applicability. |
| https://pcogiving.zendesk.com/hc/en-us/articles/360011867633-Manage-donors | Planning Center | Updated 2025-10-03 | 2026-04-15 | Official donor-profile handling, matching, merge, and inactive guidance in Giving. |
| https://support.planningcenteronline.com/hc/en-us/articles/4694905331867-The-Planning-Center-API | Planning Center | Updated 2025-04-30 | 2026-04-15 | Confirms current API coverage across Calendar, Check-Ins, Giving, Groups, People, and Services. |
| https://www.planningcenter.com/blog/2025/09/no-more-form-fatigue-let-people-edit-their-own-information-in-church-center | Planning Center | 2025-09-03 | 2026-04-15 | Recent official guidance on profile self-service editing in Church Center. |
| https://www.planningcenter.com/changelog/people/40152030166427-new-include-custom-fields-membership-type-and-campus-on-church-center-profiles | Planning Center | 2025-08-19 | 2026-04-15 | Product update showing expanded self-service profile editing options. |
| https://churchtechtoday.com/planning-center-clean-up/ | ChurchTechToday | 2022-02-25 | 2026-04-15 | Church-specific cleanup guidance reinforcing regular duplicate review and cleanup cadence. |
| https://churchtechtoday.com/why-churches-need-to-segment-databases/ | ChurchTechToday | 2020-05-06 | 2026-04-15 | Older but useful church-specific reasoning for segmentation and dynamic grouping. |
| https://www.ccsfundraising.com/insights/nonprofit-data-management/ | CCS Fundraising | 2025-03-31 | 2026-04-15 | Nonprofit data-quality guidance on consistency, accuracy, and staff capability. |
| https://www.donordock.com/articles/data-hygiene | DonorDock | 2025-06-xx or approx. 10 months before access | 2026-04-15 | Nonprofit donor database hygiene guidance emphasizing recurring maintenance and duplicate control. |
| https://www.foundant.com/blog/nonprofit-database-management/ | Foundant | 2025-01-15 | 2026-04-15 | Nonprofit database hygiene guidance supporting audit cadence and data-quality discipline. |

---

## 17. Direct application to Mosaic’s future live audit

The live audit should test whether Mosaic’s PCO account:
1. reflects the governance choices above consistently,
2. uses PCO-native capabilities well,
3. avoids unnecessary complexity,
4. protects sensitive data appropriately, and
5. supports ministry execution, communication, safety, and reporting with high-trust data.

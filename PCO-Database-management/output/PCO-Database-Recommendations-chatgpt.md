# PCO-Database-Recommendations

## Scope note
These recommendations are **evidence-based from current best-practice research**, but they are **not yet validated against Mosaic’s live PCO account** in this environment. They should be treated as a prioritized action plan for the next phase.

---

## Executive recommendation
Run the work in two tracks:

1. **Track A: Governance and audit readiness**
   - define standards,
   - define owners,
   - prepare audit queries,
   - lock down sensitive structures.

2. **Track B: Live-system audit and remediation**
   - measure the current state,
   - fix high-risk issues first,
   - then clean structure and process debt,
   - then automate recurring hygiene.

---

## Priority 0: Access and audit readiness

### Recommendation 0.1
**Observation:** A live audit requires authenticated PCO access that was not available here.  
**Why it matters:** Without direct account evidence, no honest Mosaic-specific system claims can be made.  
**Recommendation:** Run the audit from an environment that has authenticated access to:
- People,
- Services,
- Check-Ins,
- Giving,
- Calendar,
- Groups,
- Registrations,
- and, ideally, object metadata for lists/workflows/automations/custom fields/permissions.
**Decision owner:** Executive Pastor / systems lead

### Recommendation 0.2
**Observation:** Best-practice decisions need to be explicit before cleanup starts.  
**Why it matters:** Cleanup without standards recreates mess with more confidence.  
**Recommendation:** Approve a short governance packet before live remediation:
- required person fields,
- household rules,
- membership taxonomy,
- inactive reasons,
- custom field approval rules,
- merge policy,
- delete/inactivate policy,
- permission review cadence.
**Decision owner:** Executive Pastor + ministry ops/data owner

---

## Priority 1: High-value quick wins once access exists

### Recommendation 1.1
**Observation:** Duplicate prevention and review are high-leverage in PCO.  
**Why it matters:** Duplicates corrupt communication, care, giving, attendance, volunteer history, and reporting.  
**Recommendation:** Establish a duplicate-control program:
- review duplicate detector weekly,
- document merge-primary rules,
- audit form/registration/giving creation paths,
- promote Church Center login/self-service to reduce duplicate creation.
**Decision owner:** Database owner / admin lead

### Recommendation 1.2
**Observation:** PCO recommends inactivation rather than deletion for real people.  
**Why it matters:** Deletion destroys cross-product history.  
**Recommendation:** Adopt a formal rule:
- **delete only** test records or accidental empty shells,
- **inactive by default** for real people no longer active.
Add and normalize inactive reasons.
**Decision owner:** Systems owner

### Recommendation 1.3
**Observation:** Custom fields often become ungoverned sprawl.  
**Why it matters:** Field sprawl reduces reporting trust and increases admin burden.  
**Recommendation:** Freeze new custom fields until review is complete. Then inventory every field by:
- purpose,
- owner,
- data type,
- who can see it,
- where it is used,
- keep / revise / merge / retire decision.
**Decision owner:** Systems owner + ministry stakeholders

### Recommendation 1.4
**Observation:** Lists, workflows, and automations should be the standing hygiene engine.  
**Why it matters:** Manual cleanup decays quickly.  
**Recommendation:** Create permanent hygiene lists for:
- missing contact data,
- missing campus/lifecycle state,
- possible duplicates,
- stale active records,
- expired/missing background checks,
- donor matching exceptions,
- stale workflow cards.
**Decision owner:** Database/process owner

### Recommendation 1.5
**Observation:** Volunteer and child-safety data deserves first-pass review.  
**Why it matters:** This is the most likely area to carry safety and liability risk.  
**Recommendation:** First live audit pass should include:
- volunteers in child/youth roles,
- background check status,
- expiration dates,
- ministry approval state,
- training markers if used.
**Decision owner:** Executive Pastor + relevant ministry directors

---

## Priority 2: Structural recommendations

### Recommendation 2.1
**Observation:** Household design has downstream effects across Church Center, registrations, check-ins, and services.  
**Why it matters:** Poor household structure creates operational confusion and bad self-service behavior.  
**Recommendation:** Write household rules covering:
- when to create households,
- who is guardian/other adult/child,
- when adults remain or leave a household,
- how split families and blended-family realities are handled,
- how multiple-household cases are handled.
**Decision owner:** Ministry ops lead

### Recommendation 2.2
**Observation:** Membership and lifecycle labels often drift over time.  
**Why it matters:** Communication and reporting become unreliable.  
**Recommendation:** Reduce to a short, operational taxonomy with written definitions and assignment rules. Use inactive reasons separately from membership status.
**Decision owner:** Executive leadership

### Recommendation 2.3
**Observation:** Permissions in church systems often stay broad after role changes.  
**Why it matters:** This increases privacy and accidental-change risk.  
**Recommendation:** Review who can:
- merge records,
- bulk update records,
- manage custom fields,
- manage lists/workflows/automations,
- access background checks,
- access Giving data.
Then tighten to least privilege.
**Decision owner:** Executive Pastor / systems admin

### Recommendation 2.4
**Observation:** Data entry inconsistency is usually a process problem before it is a database problem.  
**Why it matters:** Cleanup will fail unless entry rules improve.  
**Recommendation:** Publish a short admin standard for:
- names,
- contact methods,
- campus,
- membership/lifecycle assignment,
- custom field use,
- household edits,
- merge requests,
- inactive decisions.
**Decision owner:** Systems owner

---

## Priority 3: Module-specific review actions

### People
- Audit missing required fields.
- Audit stale active profiles.
- Audit duplicate candidates and merge backlog.
- Audit household anomalies.

### Giving
- Audit donors not matched to People.
- Audit donor duplicates and inconsistent name/email patterns.
- Audit inactive people with current giving activity.
- Validate receipting contact assumptions after merges.

### Check-Ins
- Use attendance history as one input to active/inactive review.
- Review child/guardian household correctness where check-in depends on it.

### Services
- Review whether volunteer/service state is tracked in too many places.
- Prefer one clear source of truth for readiness/approval states.

### Groups
- Review whether group participation is being duplicated into unnecessary custom fields.
- Keep only the extra data needed for reporting or workflows.

### Calendar / Registrations
- Review creation flows that may generate duplicate people.
- Confirm owner and participant mappings that should point back to the correct person record.

---

## Recommended project sequence

### Phase 1: Approve standards
Deliverables:
- governance one-pager,
- merge policy,
- inactive/delete policy,
- custom field approval standard,
- permission review matrix.

### Phase 2: Baseline audit
Deliverables:
- counts and percentages,
- top-risk findings,
- object inventories,
- stratified sample review,
- remediation backlog.

### Phase 3: Critical remediation
Order:
1. child-safety / background-check issues,
2. permission issues,
3. duplicate backlog,
4. inactive/delete corrections,
5. donor identity issues.

### Phase 4: Structure cleanup
Order:
1. custom field rationalization,
2. lifecycle taxonomy normalization,
3. household cleanup,
4. stale lists/workflows/automations review.

### Phase 5: Ongoing hygiene
Deliverables:
- standing hygiene lists,
- monthly owner review,
- quarterly governance review,
- annual field/process review.

---

## Suggested KPIs for the live project

Track at least:
- duplicate candidates open,
- active records missing required contact data,
- active records missing lifecycle/campus fields,
- volunteer safety records missing or expired background checks,
- donor records unmatched to People,
- stale workflow cards older than policy threshold,
- number of custom fields retired/merged,
- permission exceptions corrected.

---

## Decision log items Mosaic should resolve explicitly
1. What fields are required for every active person?
2. What are the authoritative membership and lifecycle statuses?
3. What constitutes inactive, and after how long?
4. Which fields may be editable by congregants in Church Center?
5. Which sensitive data belongs in PCO at all?
6. Which ministry states belong in custom fields versus workflows versus product-native activity?
7. Who owns each part of database hygiene operationally?

---

## Immediate next project steps
1. Secure authenticated live PCO access in the audit environment.
2. Export or query object inventories for People, lists, workflows, automations, custom fields, permissions, donors, and background checks.
3. Run the baseline metrics listed in `PCO-Audit-Findings.md`.
4. Produce a true Mosaic-specific findings report with counts, examples, and confidence ratings.
5. Prioritize remediation by safety/privacy first, then reporting/communication trust, then admin efficiency.

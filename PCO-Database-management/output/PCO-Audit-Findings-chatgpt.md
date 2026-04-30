# PCO-Audit-Findings

## Audit status
**Status:** Incomplete in this environment.  
**Reason:** I do not have direct access here to Mosaic Wadsworth’s live Planning Center account, PCO MCP tools, or a Claude Code environment with authenticated PCO API credentials. Because of that, I cannot truthfully claim a live-system audit was performed.

This file therefore contains:
1. the findings I can support right now,
2. the exact evidence standard and audit framework to use once access is available,
3. a findings template ready to populate with live results.

---

## Evidence standard for every live finding
For each material finding, capture:
- **Source of evidence**
- **Date accessed**
- **Query / object examined**
- **Count or percentage**
- **Confidence level**: High / Medium / Low

---

## Findings currently supportable

### Finding 1
**Observation:** No live Planning Center audit was executed from this environment.  
**Why this matters:** Any claim about Mosaic’s actual duplicates, stale data, field sprawl, donor linkage, workflow debt, or permissions would be speculative.  
**Evidence source:** Current working environment capabilities only.  
**Date accessed:** 2026-04-15  
**Query / object examined:** Available tooling and connectors in-session.  
**Count or percentage:** 0 live PCO objects examined.  
**Confidence:** High

### Finding 2
**Observation:** The best-practice reference is strong enough to drive a rigorous live audit once authenticated PCO access is available.  
**Why this matters:** Mosaic can move directly into an evidence-based audit rather than starting discovery from scratch.  
**Evidence source:** Official Planning Center documentation and related best-practice research summarized in `PCO-Best-Practices-Reference.md`.  
**Date accessed:** 2026-04-15  
**Query / object examined:** Official PCO support/blog/API sources and supporting nonprofit/church-tech sources.  
**Count or percentage:** 20+ research sources reviewed.  
**Confidence:** High

---

## Live-audit workplan to populate this file

### A. People / record quality
Measure:
- total people,
- active vs inactive counts,
- profiles missing email,
- profiles missing phone,
- profiles missing both email and phone,
- profiles missing campus,
- profiles missing membership type where policy expects one,
- profiles updated recently vs stale,
- likely duplicates,
- household anomalies.

### B. Households
Measure:
- total households,
- households with duplicate or suspiciously similar names/addresses,
- children with no guardian,
- adults incorrectly labeled as child/dependent,
- people in multiple households where that may be expected vs anomalous.

### C. Custom fields
Measure:
- number of custom tabs,
- number of custom fields,
- fields with low completion,
- fields not referenced by any list/workflow/report/form where determinable,
- duplicate or overlapping fields,
- free-text fields used where controlled values would be better,
- sensitive fields with broad visibility.

### D. Lists
Measure:
- total lists,
- lists by owner,
- lists without clear purpose/category,
- stale lists,
- lists with auto-refresh,
- lists feeding automations,
- dependency chains likely to create refresh ambiguity.

### E. Workflows
Measure:
- total workflows,
- active vs archived,
- cards by workflow,
- stale cards,
- workflows with no current owner/manager,
- workflows duplicating field-based state unnecessarily.

### F. Automations
Measure:
- total automations,
- automations by trigger type,
- automations updating fields,
- automations adding tasks/cards,
- possible circular or brittle logic,
- automations dependent on list refresh behavior.

### G. Volunteer / safety
Measure:
- active volunteers,
- active volunteers in child/youth-sensitive roles,
- missing/expired background checks,
- missing training markers if tracked,
- role approval state inconsistencies.

### H. Giving
Measure:
- donors linked vs unlinked to People,
- donors with incomplete contact data,
- likely donor duplicates,
- inactive people with current giving activity,
- recurring gift records needing identity review after merges.

### I. Permissions
Measure:
- who can merge profiles,
- who can run bulk actions,
- who can manage custom fields,
- who can access donor data,
- who can access background checks,
- who can manage lists/workflows/automations,
- broad-access tabs containing sensitive information.

---

## Required sampling method if full extraction is impractical

Use a stratified people-record sample covering:
- adults,
- children,
- active,
- inactive,
- volunteers,
- non-volunteers,
- donors,
- non-donors,
- recently updated records,
- stale records.

For each sampled record, inspect:
- identity consistency,
- household correctness,
- lifecycle status,
- contact completeness,
- custom field quality,
- sensitive-data placement,
- cross-module activity fit.

---

## Findings template for live population

### Finding [ID]
**Type:** Factual observation / Inferred risk / Recommendation / Unresolved question  
**Observation:**  
**Why it matters:**  
**Evidence source:**  
**Date accessed:**  
**Query / object examined:**  
**Count / percentage:**  
**Confidence:** High / Medium / Low  
**Privacy note:** Aggregate / minimal example / sensitive review required  
**Recommendation:**  
**Decision owner:**  

---

## Priority rating model for future findings
- **Critical:** Safety, legal/compliance, financial receipting, major privacy exposure, or systemic data-loss risk.
- **High:** Strong impact on communication accuracy, ministry follow-up, reporting trust, or duplicate/stale-data accumulation.
- **Medium:** Process friction, moderate reporting distortion, or avoidable admin burden.
- **Low:** Cleanup or optimization issues with limited operational impact.

---

## Unresolved questions pending live access
1. What is Mosaic’s actual membership/lifecycle taxonomy today?
2. Which custom fields are actively used versus legacy?
3. How many duplicate candidates exist, and from which creation paths?
4. How healthy is donor matching between Giving and People?
5. Are volunteer safety fields/background checks complete and current?
6. Are there list, workflow, or automation structures that create hidden maintenance debt?
7. Are permissions tighter than necessary, appropriate, or over-broad?

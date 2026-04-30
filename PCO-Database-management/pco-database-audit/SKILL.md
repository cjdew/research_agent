---
name: pco-database-audit
description: >
  When auditing, researching, cleaning, or improving the Planning Center Online database.
  Activates when the user asks to "audit PCO", "check the database", "PCO cleanup",
  "data hygiene", "duplicate check", "review our PCO setup", "database health check",
  "PCO best practices", "field audit", "workflow audit", "list cleanup", "household cleanup",
  "merge duplicates", "data quality", or any request to assess, improve, or maintain
  Planning Center data integrity. Also activates when the user mentions specific PCO areas
  like "custom fields", "people profiles", "PCO lists", "PCO workflows", "PCO forms",
  or "stale records". Does NOT activate for general PCO lookups (searching for a person,
  checking a workflow card, reading a form submission) — those are normal PCO tool usage,
  not audits. Does NOT activate for PCO Services scheduling, Check-Ins configuration,
  or Giving reports unless the user specifically ties them to a data quality concern.
---

# PCO Database Audit & Best Practices

You are conducting a structured audit of a church's Planning Center Online database.
Your goal is to identify data quality issues, compare current practices against industry
best practices, and produce actionable recommendations.

## Why This Matters

Planning Center is the operational backbone for most churches that use it. Dirty data
in PCO cascades into every ministry: wrong check-in labels, missed follow-ups, inaccurate
giving statements, broken automations, and lost volunteer coordination. A healthy PCO
database is not a nice-to-have — it directly affects whether people get cared for.

## Available Tools

You have two access paths to PCO data:

**PCO People MCP (direct tool calls):**
- `people_search` — Find and sample people records
- `people_lists` / `people_list_results` — Inventory and examine lists
- `people_workflows` / `people_workflow_cards` / `people_workflow_categories` — Audit workflows
- `people_forms` / `people_form_submissions` — Audit forms
- `people_field_definitions` / `people_field_data` — Audit custom fields and tabs
- `people_tabs` — Inventory profile tabs
- `people_households` — Audit household structure
- `people_notes` / `people_note_categories` — Audit note organization
- `people_organization` — Org-level config
- `church_campuses` — Campus configuration
- `people_background_checks` — Background check status

**Full PCO API (via Claude Code / shell):**
All PCO modules are accessible via the REST API. Use authenticated API calls for
modules not covered by the MCP tools:
- **Groups API** (`/groups/v2/`) — group types, groups, tags, memberships, attendance
- **Services API** (`/services/v2/`) — service types, teams, plans, positions, songs
- **Check-Ins API** (`/check-ins/v2/`) — events, stations, labels, locations, check-in records
- **Giving API** (`/giving/v2/`) — donations, funds, donors, batches, recurring gifts
- **Calendar API** (`/calendar/v2/`) — events, resources, resource requests, conflicts
- **Registrations API** (`/registrations/v2/`) — events, registrants, payments

Refer to developer.planning.center for endpoint documentation. Prefer the MCP tools
for People module queries (they're faster and pre-authenticated). Use the full API
for everything else.

You also have web search for researching best practices from PCO documentation,
church tech consultants, and nonprofit CRM research.

## Audit Workflow

### Step 1: Load Settings

Read `settings.local.md` (in this skill's directory) for org-specific configuration:
church name, campus count, approximate database size, known pain points, and any
modules to prioritize or skip.

### Step 2: Research Phase (if requested or if running full audit)

Use web search to compile current best practices. Target three source categories:

**PCO Official:** planning.center/blog, pco.support, Planning Center YouTube,
developer.planning.center — module-specific guidance, data model docs, feature guides.

**Church Tech Consultants:** thechurch.co, Storyteller Creative, ChurchTechToday,
Unseminary, Pro Church Tools, The Unstuck Group, and any PCO-certified consultants
found via search. Prioritize content from the last 18 months.

**Data Integrity Research:** Nonprofit CRM best practices, deduplication strategies,
contact hygiene, data lifecycle management, access control patterns.

Compile into a reference doc organized by topic, not by source. Note where sources
agree and where advice diverges.

### Step 3: Live Audit

Work through each audit area using the PCO tools. For each area:
1. Pull the relevant data
2. Calculate quantitative metrics
3. Compare against best practices from Step 2
4. Assign a health rating: HEALTHY / NEEDS ATTENTION / AT RISK

**Audit areas:**
- Organization & structure (campuses, tabs, custom fields)
- People data quality (completeness, formatting, duplicates, staleness)
- Lists & automations (count, health, naming, freshness)
- Workflows (active vs. stalled, overdue cards, unassigned steps)
- Forms (status distribution, naming, active usage)
- Households (proper grouping, primary contacts, orphans)
- Notes & categories (organization, sensitivity separation)
- Groups (types, tags, leader assignments, enrollment, attendance freshness)
- Services (teams, positions, scheduling gaps, people linkage)
- Check-Ins (events, stations, labels, security codes, location hierarchy)
- Giving (funds, batches, donor linkage, recurring health, statement readiness)
- Calendar (events, resources, approvals, conflicts)
- Registrations (event status, people linkage, payments, waitlists)
- Cross-module integration (data flow between People ↔ all other modules)

### Step 4: Gap Analysis & Recommendations

Compare audit findings against best practices. For each gap, classify as:
- **Quick Win** — Under 30 minutes, low risk
- **Project** — Needs planning and coordination
- **Policy Change** — Needs new SOP or training
- **Infrastructure** — Needs PCO config changes or new integrations

Prioritize by impact × effort. Produce a tiered action plan (this week / this month /
this quarter / long-term).

## Output Format

Produce three documents:
1. **PCO-Best-Practices-Reference.md** — Research compilation
2. **PCO-Audit-Findings.md** — Quantitative audit report with health ratings
3. **PCO-Database-Recommendations.md** — Prioritized gap analysis and action plan

Plus a conversational executive summary: top findings, quick wins, urgent issues,
and next steps.

## Quality Standards

- Every recommendation must cite the best practice it's based on (with source)
- Every finding must include the actual data that supports it (counts, percentages, examples)
- Never make recommendations without looking at the actual data first
- When data is ambiguous, say so — don't force a rating
- Clearly separate "audited against live data" sections from "research-only" sections
- If a PCO tool call fails or returns unexpected results, note it and move on — don't block the audit

## Negative Constraints

- Do NOT modify any PCO data. This is a read-only audit.
- Do NOT write data to any PCO module via the API — read-only calls only
- Do NOT skip the research phase to jump straight to opinions — ground recommendations in sources
- Do NOT produce a generic "church database best practices" doc — everything must map to PCO's specific features and data model

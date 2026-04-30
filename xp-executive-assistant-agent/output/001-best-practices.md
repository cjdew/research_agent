# Building an Agentic Executive Assistant: Architecture, Capabilities, and Best Practices

## Executive Summary

The evidence strongly favors a **simple, tool-augmented single-agent architecture** over multi-agent frameworks for an executive assistant agent --- particularly one built by a small team on a TypeScript stack. Anthropic's own guidance and multiple survey papers converge on the same principle: start with the simplest pattern that works, add complexity only when it delivers measurable value. The best framework choice for your stack is the **Claude Agent SDK (TypeScript)**, which provides a production-ready agentic loop with built-in tool execution, MCP integration, session management, and hooks --- all natively in TypeScript. Academic research (notably the Harvard/BCG "jagged frontier" study, n=758) confirms that AI augmentation of knowledge work produces real productivity gains (12-25% on suitable tasks) but introduces overreliance risks that require deliberate human-in-the-loop design. The most common failure modes in production agent systems are not architectural --- they are scoping failures, context mismanagement, and poor tool design.

**Confidence:** High for architecture and capability recommendations. Medium for framework comparison (field is moving fast). High for safety/HITL principles. Medium-High for academic evidence on productivity effects.

---

## Finding 1: Architecture --- Start Simple, Stay Simple

### The Pattern Hierarchy

Anthropic's "Building Effective Agents" guide (December 2024, updated through 2025) identifies a progression of seven patterns, ordered from simple to complex [1]:

1. **Augmented LLM** --- A single LLM with retrieval, tools, and memory. The foundation.
2. **Prompt Chaining** --- Sequential LLM calls with programmatic gates between steps.
3. **Routing** --- Classify input, direct to specialized handlers.
4. **Parallelization** --- Run independent subtasks concurrently.
5. **Orchestrator-Workers** --- A central LLM decomposes tasks and delegates to worker LLMs.
6. **Evaluator-Optimizer** --- One LLM generates, another evaluates and refines.
7. **Autonomous Agent** --- LLM uses tools in a feedback loop with minimal constraints.

The key insight from Anthropic, corroborated by the arxiv survey of 90+ studies [2]: **the majority of successful production deployments use patterns 1-4, not 5-7.** Multi-agent systems add communication overhead, debugging complexity, and cost without proportional benefit for most use cases.

### Recommended Architecture for Your Executive Assistant

**Pattern: Augmented LLM (pattern 1) with Routing (pattern 3)**

A single Claude-powered agent with:
- A **system prompt** that defines the executive assistant role, capabilities, and constraints
- A **tool set** for calendar, email, tasks, and information retrieval (via MCP servers)
- A **routing layer** that classifies incoming requests and applies different tool permissions and prompt augmentations based on request type (e.g., "schedule meeting" vs. "draft email" vs. "generate briefing")
- **Session memory** for maintaining context across multi-turn interactions

This avoids the "multi-agent overkill" anti-pattern identified in multiple sources [3][4], where unnecessary agent-to-agent coordination introduces latency, token cost, and failure points.

**When to consider multi-agent:** Only if you later find that a single agent's context window is consistently overwhelmed by the breadth of tools/instructions, or if you need truly parallel long-running tasks (e.g., researching three topics simultaneously). Even then, use subagents (supported by the Claude Agent SDK) rather than a full multi-agent framework.

**Confidence:** High. Multiple independent sources converge on this recommendation.

---

## Finding 2: Capabilities --- What the Agent Should Do

Based on analysis of existing AI executive assistant products, the Anthropic patterns guide, and your specific role context, here is a capability map organized by implementation priority.

### Tier 1: Core (Build First)

| Capability | Description | Implementation Path |
|---|---|---|
| **Morning Briefing** | Daily digest of calendar, unread priority email, open tasks, pending delegations | Scheduled agent run via cron trigger; pull from M365 MCP |
| **Email Triage** | Classify, prioritize, summarize inbox; draft replies for review | M365 MCP email tools; human approval before sending |
| **Calendar Management** | Check availability, propose meeting times, create/modify events | M365 MCP calendar tools; confirmation required for changes |
| **Task Tracking** | Surface overdue items, upcoming deadlines, blocked tasks | M365 Planner/To-Do MCP tools |
| **Quick Q&A** | Answer questions about schedule, contacts, recent communications | Read-only queries against M365 data |

### Tier 2: High Value (Build Second)

| Capability | Description | Implementation Path |
|---|---|---|
| **Meeting Prep** | Assemble attendee context, relevant documents, agenda items before meetings | Calendar event triggers; document retrieval from SharePoint |
| **Delegation Tracking** | Track items assigned to direct reports; flag overdue/stalled items | Planner integration; periodic status checks |
| **Weekly Summary** | Executive summary of the week: decisions made, items completed, items carried forward | Aggregation of calendar, email, and task data |
| **Communication Drafting** | Draft staff communications, meeting follow-ups, announcements | Human review required before sending |

### Tier 3: Aspirational (Build When Tier 1-2 Are Solid)

| Capability | Description |
|---|---|
| **Proactive Scheduling** | Detect scheduling conflicts, suggest rescheduling, auto-block focus time |
| **Information Retrieval** | Search across SharePoint, OneDrive, and church management systems |
| **Decision Support** | Pull relevant data for decisions (budget numbers, attendance trends, etc.) |
| **Cross-Platform Coordination** | Bridge between Outlook, Slack, Planning Center, and other systems |

### What NOT to Build

- **Autonomous email sending** without human review. The risk/reward ratio is terrible for an executive's outbound communications.
- **Financial transaction execution.** Read-only access to financial data is fine; never let the agent move money.
- **HR-sensitive actions.** The agent can surface information but should never make personnel-related decisions or communications without explicit human approval.

**Confidence:** High for Tier 1 priorities. Medium for Tier 2-3 (dependent on your specific workflow patterns).

---

## Finding 3: Trust, Safety, and Human-in-the-Loop Design

### The Core Principle

The EU AI Act (Article 14) and NIST AI Risk Management Framework both require demonstrable human oversight that is trained, measurable, and provable [5]. Even without regulatory compliance pressure, the research is clear: human oversight is not optional for agentic systems that take real-world actions.

### Action Classification Model

Classify every agent action into one of three tiers:

| Tier | Description | Examples | Approval Model |
|---|---|---|---|
| **Read** | Information retrieval only | Check calendar, read email, search documents | No approval needed |
| **Draft** | Prepares output for human review | Draft email, generate briefing, propose schedule | Review before execution |
| **Act** | Takes real-world action | Send email, create meeting, modify task | Explicit approval required |

This maps directly to the Claude Agent SDK's permission system, which supports `allowedTools` lists and `PreToolUse` hooks for gating specific actions.

### Guardrail Implementation

Based on the Microsoft failure mode taxonomy [6] and multiple practitioner sources:

1. **Identity and access control.** The agent should authenticate as a specific service principal with scoped permissions --- not the user's full credentials. Every action should be traceable to the agent identity.

2. **Maximum iteration limits.** Set hard caps on the number of tool calls per session (the Claude Agent SDK supports this). An agent stuck in a loop will burn tokens and potentially take unintended actions.

3. **Scope boundaries.** Define explicit boundaries on what data the agent can access and what actions it can take. Use MCP server permissions to enforce this at the infrastructure level, not just in the prompt.

4. **Audit logging.** Log every tool call, every decision, every human approval/rejection. The Claude Agent SDK's `PostToolUse` hooks make this straightforward.

5. **Graceful degradation.** When the agent is uncertain, it should surface the uncertainty and ask for guidance rather than guessing. Build this into the system prompt.

6. **Reversibility preference.** Prefer reversible actions (create draft) over irreversible ones (send email). When an irreversible action is needed, require confirmation.

### The Overreliance Problem

The Harvard/BCG "jagged frontier" study [7] and a 2025 Nature Human Behaviour paper both document a real risk: repeated interaction with AI systems reduces independent critical evaluation. For an executive pastor making operational decisions, this means:

- The briefing agent should present information, not make recommendations, until you have high confidence in its judgment calibration.
- Periodically spot-check the agent's email triage accuracy. Automation complacency degrades over time.
- Never let the agent become the sole source of truth for any critical workflow.

**Confidence:** High. Supported by peer-reviewed research, regulatory frameworks, and industry practice.

---

## Finding 4: Framework Comparison

### The Contenders for TypeScript-Based Agentic Assistants

| Framework | Language | Architecture Model | Maturity | M365 Integration | Best For |
|---|---|---|---|---|---|
| **Claude Agent SDK** | TypeScript, Python | Single-agent agentic loop with subagents | Production (GA 2025) | Via MCP servers | Production agents with Claude; tool-heavy workflows |
| **Mastra** | TypeScript | Agent + workflow orchestration | Production (1.0 Jan 2026) | Via integrations | TypeScript-native teams; multi-model support |
| **Strands Agents (AWS)** | TypeScript (preview), Python | Model-driven agent loop | Experimental TS; Production Python | Via tools | AWS-heavy stacks; multi-model support |
| **LangGraph** | Python (primary), JS | Graph-based state machines | Production | Via integrations | Complex conditional workflows; Python teams |
| **CrewAI** | Python | Role-based multi-agent | Production | Limited | Multi-agent role specialization; Python teams |
| **AutoGen** | Python | Conversation-based multi-agent | Maintenance mode | Limited | Research/prototyping; declining investment |
| **OpenAI Agents SDK** | Python | Multi-agent with handoffs | Production | Via tools | OpenAI model lock-in; multi-agent handoffs |

### Recommendation: Claude Agent SDK

For your specific context (TypeScript stack, Azure deployment, single developer, Microsoft 365 integration needs), the Claude Agent SDK is the strongest fit:

1. **Native TypeScript.** First-class TypeScript support with `@anthropic-ai/claude-agent-sdk`. No Python bridge needed.

2. **Built-in agentic loop.** The SDK handles the reason-act-observe cycle. You define tools and prompts; it handles orchestration.

3. **MCP integration.** You already have MCP servers configured for Microsoft 365 in your Claude setup. The Agent SDK connects to MCP servers with a single config line. This gives you calendar, email, tasks, and SharePoint access immediately.

4. **Hooks system.** `PreToolUse`, `PostToolUse`, `Stop`, `SessionStart`, `SessionEnd` hooks provide the control points needed for audit logging, approval gates, and guardrails.

5. **Subagents.** If you later need task decomposition (e.g., a "research" subagent and a "drafting" subagent), the SDK supports this without moving to a multi-agent framework.

6. **Sessions.** Built-in session management with resume and fork capabilities. This matters for an executive assistant that needs to maintain context across a workday.

7. **Bedrock/Foundry support.** If you want to run through Azure AI Foundry instead of the Anthropic API directly, the SDK supports this.

### Mastra as a Credible Alternative

Mastra deserves mention as the other strong TypeScript-native option [8]. It offers multi-model support (3,300+ models), a visual playground for testing, built-in evals, and strong community traction (1.8M monthly downloads). The trade-off: it is model-agnostic rather than Claude-optimized, so you lose Claude-specific features like the built-in tool set and MCP-native integration. Consider Mastra if you want model flexibility or if the Claude Agent SDK's pricing model does not work for your volume.

### What to Avoid

- **AutoGen** is in maintenance mode. Microsoft's investment has shifted to the broader Microsoft Agent Framework. Not recommended for new projects.
- **CrewAI** consumed nearly 2x the tokens and took 3x as long as alternatives in benchmark testing [9]. Its role-based model adds overhead that is not justified for a single-user executive assistant.
- **LangGraph** is powerful but Python-first. The JavaScript version is less mature and the graph-based abstraction adds complexity that is unnecessary for your use case.

**Confidence:** Medium-High. The Claude Agent SDK is new (GA 2025) and the ecosystem is still forming. Mastra is also young. Both are production-viable but expect API changes. The negative assessments of AutoGen and CrewAI are high-confidence.

---

## Finding 5: What the Research Says About AI-Augmented Executive Work

### The Harvard/BCG Study (n=758, Peer-Reviewed)

"Navigating the Jagged Technological Frontier" (Dell'Acqua et al., 2023, published in Organization Science 2025) [7] is the most rigorous study available on AI augmentation of knowledge work. Key findings:

- **Inside the frontier:** Consultants using GPT-4 completed 12.2% more tasks, 25.1% faster, with significantly higher quality.
- **Outside the frontier:** Consultants using AI were 19% less likely to produce correct solutions on tasks beyond AI capability boundaries.
- **The jagged frontier problem:** Workers cannot reliably distinguish tasks inside vs. outside the AI capability boundary. This is directly relevant to an executive assistant agent --- some requests will be well within its capability (calendar scheduling), while others will be at or beyond the boundary (nuanced communication drafting).

### MIT Sloan / Stanford Research

Multiple studies from MIT Sloan and Stanford Digital Economy Lab confirm [10][11]:
- AI augmentation produces the largest gains for **conceptualization tasks** (generating ideas, framing problems) rather than execution tasks.
- Workers who use AI as a **thinking partner** (testing assumptions, generating alternatives) outperform those who use it as a task executor.
- Frequent AI tool usage was associated with **greater knowledge gain** but also **information overload** that impaired end-of-day recovery.

### Implications for Your Executive Assistant

1. **Design for augmentation, not automation.** The agent should surface information and options, not make decisions. This aligns with both the research and your role as an executive.

2. **The briefing use case is ideal.** Morning briefings and meeting prep are classic "inside the frontier" tasks where AI reliably outperforms manual effort.

3. **Communication drafting is on the frontier.** Email drafting will sometimes produce excellent results and sometimes produce inappropriate tone or missed context. Always require human review.

4. **Build in cognitive load management.** The information overload finding matters for someone with ADHD. The agent should present structured, prioritized information --- not raw data dumps.

**Confidence:** High. Based on peer-reviewed research with large sample sizes and rigorous methodology.

---

## Finding 6: Failure Modes and Anti-Patterns

### The Microsoft Taxonomy

Microsoft's AI Red Team published a taxonomy of 27 failure modes in agentic AI systems (April 2025) [6]. The most relevant ones for an executive assistant agent:

| Failure Mode | Description | Mitigation |
|---|---|---|
| **Memory Poisoning** | Malicious or corrupted data stored in agent memory gets recalled and acted upon | Trust boundaries for memory; validate recalled context |
| **Goal Misalignment** | Agent optimizes for wrong objectives or interprets instructions unintendedly | Explicit objective statements; regular calibration checks |
| **Boundary Violation** | Agent exceeds intended scope, accessing systems or taking actions beyond authorization | Least-privilege permissions; MCP server scoping |
| **Cascading Errors** | Initial error compounds through multi-step execution | Maximum iteration limits; checkpoint validation |
| **Context Window Overflow** | Long sessions degrade performance as context fills | Context compaction; session resets; just-in-time data loading |

### Practitioner-Identified Anti-Patterns

From multiple production experience reports [3][4][12]:

1. **Multi-agent overkill.** Launching multiple agents for tasks a single agent handles fine. Each agent adds latency, cost, and coordination failure risk.

2. **Monolithic context loading.** Pre-loading all possible information into the context window. Instead, use just-in-time retrieval --- load data only when needed for the current task.

3. **Insufficient tool documentation.** Anthropic's own guidance states: "Tool definitions and specifications should be given just as much prompt engineering attention as your overall prompts." Vague tool descriptions cause incorrect tool selection.

4. **Missing error boundaries.** When a tool call fails, the agent should handle the error gracefully, not retry indefinitely or hallucinate a result.

5. **Skipping guardrails.** Deploying without approval workflows, scope limits, or audit logging. The speed advantage of skipping these evaporates at the first production incident.

6. **The "bag of agents" trap.** Adding agents to solve problems that are actually prompt engineering or tool design issues. From a Towards Data Science analysis: multi-agent systems produce 17x more errors than well-designed single agents on equivalent tasks [4].

### Context Engineering

Anthropic's context engineering guide (2025) [13] identifies the core challenge for long-running agents: **context rot.** As the context window fills, model performance degrades because:
- Transformer attention is spread across more tokens
- Models are less well-trained on very long contexts
- Every additional token depletes the "attention budget"

Mitigations:
- **Compaction:** Periodically summarize conversation history, preserving key decisions and discarding verbose tool outputs
- **Structured note-taking:** The agent maintains a running scratchpad file outside the context window
- **Just-in-time loading:** Use lightweight identifiers (file paths, URLs, IDs) and load full data only when needed

**Confidence:** High. The Microsoft taxonomy is from a credible research team. Practitioner reports are consistent across multiple independent sources.

---

## Conflicting Evidence and Open Questions

### Areas of Disagreement

1. **Framework maturity.** Some sources position the Claude Agent SDK as production-ready; others note it is still new with a forming ecosystem. The SDK was renamed from "Claude Code SDK" recently, suggesting rapid iteration. Treat it as production-viable but expect API changes.

2. **Multi-agent vs. single-agent.** The academic survey [2] identifies benefits of multi-agent architectures (robustness, parallel execution, specialization), while Anthropic and practitioners strongly recommend starting single-agent. The resolution: single-agent is the right starting point, with multi-agent as an escalation path when specific problems demand it.

3. **Autonomy level.** Some commercial products (Lindy, Fyxer) market fully autonomous email and calendar management. The research evidence suggests this is premature --- the "jagged frontier" problem means autonomous action on edge cases produces worse outcomes than human judgment.

### Unresolved Questions

1. **Long-term memory architecture.** How to implement effective cross-session memory for an executive assistant is an active research area. Vector databases, structured knowledge graphs, and hybrid approaches all have advocates. No clear winner has emerged for the agent-assistant use case specifically.

2. **Cost at scale.** Running an always-available executive assistant agent involves continuous API costs. The economics of running multiple briefings, email triage cycles, and ad-hoc queries per day are not well-documented in the literature.

3. **Evaluation methodology.** How to measure whether the agent is actually saving executive time (vs. creating a new category of work --- managing the agent) lacks established frameworks.

---

## Practical Implementation Roadmap

Based on the evidence, here is a phased approach:

### Phase 1: Foundation (Weeks 1-2)
- Set up the operations repo with the Claude Agent SDK (TypeScript)
- Connect your existing M365 MCP servers (calendar, email, tasks)
- Build a read-only "morning briefing" agent that pulls today's calendar, priority emails, and open tasks
- Implement audit logging via PostToolUse hooks
- No write actions in this phase

### Phase 2: Draft Capabilities (Weeks 3-4)
- Add email draft generation (human review required before sending)
- Add meeting prep document assembly
- Implement the Read/Draft/Act permission tiers
- Add a scheduled trigger for the morning briefing (cron or Azure Function timer)

### Phase 3: Managed Actions (Weeks 5-8)
- Enable calendar event creation with confirmation
- Add delegation tracking against Planner/To-Do
- Implement context compaction for long sessions
- Build the weekly summary aggregation

### Phase 4: Refinement (Ongoing)
- Calibrate based on actual usage patterns
- Add capabilities from Tier 2-3 based on demonstrated need
- Evaluate whether subagents would help for specific workflows
- Monitor for overreliance patterns

---

## Methodology

**Search strategy:** 15 targeted web searches across academic databases, framework documentation, practitioner blogs, and industry reports. Key sources fetched in full for detailed analysis. Independent searches run in parallel.

**Source quality:** Primary reliance on peer-reviewed research (Harvard/BCG study, arxiv surveys), official framework documentation (Anthropic, AWS, Mastra), and the Microsoft AI Red Team taxonomy. Secondary sources from established tech publications. General web summaries used only for landscape mapping.

**What I could not access:** The Microsoft failure mode taxonomy PDF was not fully extractable via web fetch. The Concentrix 12-failure-patterns article rendered without body content. Findings from these sources are based on secondary coverage and search result summaries.

**Limitations:** Framework comparison is inherently time-sensitive. The Claude Agent SDK, Mastra, and Strands are all rapidly evolving. This assessment reflects the state as of April 2026.

---

## Sources

1. Anthropic. "Building Effective Agents." https://www.anthropic.com/research/building-effective-agents
2. Masterman, T. et al. "The Landscape of Emerging AI Agent Architectures for Reasoning, Planning, and Tool Calling: A Survey." arXiv:2404.11584 (2024). https://arxiv.org/html/2404.11584v1
3. "Anti-Pattern Multi-Agent Overkill." Agent Patterns. https://www.agentpatterns.tech/en/anti-patterns/multi-agent-overkill
4. "Why Your Multi-Agent System is Failing: Escaping the 17x Error Trap." Towards Data Science. https://towardsdatascience.com/why-your-multi-agent-system-is-failing-escaping-the-17x-error-trap-of-the-bag-of-agents/
5. "Human-in-the-Loop: A 2026 Guide to AI Oversight." Strata. https://www.strata.io/blog/agentic-identity/practicing-the-human-in-the-loop/
6. Microsoft AI Red Team. "Taxonomy of Failure Modes in Agentic AI Systems." (April 2025). https://www.microsoft.com/en-us/security/blog/2025/04/24/new-whitepaper-outlines-the-taxonomy-of-failure-modes-in-ai-agents/
7. Dell'Acqua, F. et al. "Navigating the Jagged Technological Frontier: Field Experimental Evidence of the Effects of AI on Knowledge Worker Productivity and Quality." Organization Science (2025). https://www.hbs.edu/faculty/Pages/item.aspx?num=64700
8. Mastra AI. Official documentation. https://mastra.ai/
9. DataCamp. "CrewAI vs LangGraph vs AutoGen." https://www.datacamp.com/tutorial/crewai-vs-langgraph-vs-autogen
10. MIT Sloan. "How generative AI can boost highly skilled workers' productivity." https://mitsloan.mit.edu/ideas-made-to-matter/how-generative-ai-can-boost-highly-skilled-workers-productivity
11. Stanford Digital Economy Lab. "The Effects of AI on Productivity and Work Practices." https://digitaleconomy.stanford.edu/project/augmenting-intelligence-the-effects-of-ai-on-productivity-and-work-practices/
12. Chan, A. "AI Agent Anti-Patterns (Part 1): Architectural Pitfalls That Break Enterprise Agents." Medium (2026). https://achan2013.medium.com/ai-agent-anti-patterns-part-1-architectural-pitfalls-that-break-enterprise-agents-before-they-32d211dded43
13. Anthropic. "Effective Context Engineering for AI Agents." https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
14. Anthropic. "Claude Agent SDK Overview." https://code.claude.com/docs/en/agent-sdk/overview
15. Anthropic. "Writing Effective Tools for AI Agents." https://www.anthropic.com/engineering/writing-tools-for-agents
16. Singh, A. et al. "Agentic AI: A Comprehensive Survey of Architectures, Applications, and Future Directions." Artificial Intelligence Review, Springer (2025). https://link.springer.com/article/10.1007/s10462-025-11422-4
17. Google Cloud. "Choose a Design Pattern for Your Agentic AI System." https://docs.cloud.google.com/architecture/choose-design-pattern-agentic-ai-system
18. Shao, Y. et al. "Using Augmentation-Based AI Tool at Work: A Daily Investigation." Journal of Management (2025). https://journals.sagepub.com/doi/10.1177/01492063241266503
19. "Three Challenges for AI-Assisted Decision-Making." PMC (2024). https://pmc.ncbi.nlm.nih.gov/articles/PMC11373149/
20. AWS. "Introducing Strands Agents." https://aws.amazon.com/blogs/opensource/introducing-strands-agents-an-open-source-ai-agents-sdk/

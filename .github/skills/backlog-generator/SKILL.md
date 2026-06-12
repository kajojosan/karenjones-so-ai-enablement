---
name: backlog-generator
description: Transforms a completed PRD into a structured engineering backlog —
  epics and user stories — using a conversational, iterative workflow. Identifies
  capability areas from the PRD, generates epics with OKRs and acceptance criteria,
  then decomposes each epic into sprint-sized user stories with Gherkin acceptance
  criteria, compliance notes, and traceability back to the source document.
  Use when a PM has a completed PRD and needs to create an engineering backlog
  with epics and stories that are grounded in the requirements document.
---

# Backlog Generator — PRD to Epics & Stories

## Overview

This skill transforms a completed Product Requirements Document (PRD) into a
structured engineering backlog. It works conversationally — identifying capability
areas, drafting epics one at a time, then decomposing each epic into sprint-sized
user stories. Every artifact traces back to the source PRD.

**Key Features:**
- ✅ PRD analysis and capability area identification
- ✅ Epic generation with OKRs, acceptance criteria, and compliance notes
- ✅ Story decomposition with Gherkin acceptance criteria
- ✅ Full traceability (story → epic → PRD section)
- ✅ Regulatory/compliance awareness (adapts to domain)
- ✅ Iterative refinement at each level
- ✅ Progress tracking across the backlog

## Workflow Pattern

### Phase 1: PRD Analysis

When triggered with a PRD:

**DO:**
- Read the full PRD
- Identify key elements:
  - Capability areas / functional groupings (map to epics)
  - Personas (PRD §1.2 or equivalent)
  - Success metrics and OKRs (PRD §1.6 or equivalent)
  - Non-functional requirements (performance, security, compliance)
  - Regulatory constraints (HIPAA, FDA, SOC2, etc.)
  - Integration points and dependencies
- Present a summary of what you found
- Propose 4-8 capability areas that map to epics
- Ask the user to confirm, merge, split, or reorder

**DON'T:**
- Generate epics immediately (get confirmation first)
- Invent metrics not in the PRD
- Assume priority order without asking

**Example opening:**
```
I've analyzed the PRD. Here's what I found:

**Personas:** 5 (3 primary, 2 secondary)
**Capability Areas:** 6 potential epics identified
**Success Metrics:** 12 measurable targets
**Compliance:** HIPAA, FDA 21 CFR Part 11, ISO 13485
**Integrations:** 4 external systems

Proposed epics (by priority):
1. Natural Language Information Retrieval (RAG) — FR-1 through FR-4
2. Safety, Compliance & Audit Logging — FR-5, NFR-3
3. Escalation & Dynamics 365 Integration — FR-6
4. Multi-Channel Access — FR-7
5. Context Management & Conversation State — FR-8
6. Analytics & Knowledge Gap Reporting — FR-9

Does this grouping make sense? Should I merge, split, or reorder any?
```

### Phase 2: Epic Generation (Core Loop)

For each confirmed capability area, generate a complete epic.

#### Generation Phase

**DO:**
- Generate ONLY the epic the user selected
- Include all sections:
  - YAML frontmatter (title, summary, owner, priority, phase, personas, OKRs,
    business_value, success_metrics, regulatory_requirements,
    security_considerations, dependencies, estimated_effort,
    monitoring_metrics, acceptance_criteria, out_of_scope, stakeholders, links)
  - Summary (2-3 sentences)
  - OKRs table (objective + 3-5 key results with PRD references)
  - Objective and Business Value
  - Personas Impacted
  - Acceptance Criteria (testable, with PRD section citations)
  - Validation / QA Plan
  - Monitoring and Metrics
  - Out of Scope
  - Dependencies
  - Stakeholders / Reviewers
  - Notes and Links
- Cite specific PRD sections for every metric and requirement (e.g., "per PRD §2.1.1 FR-3")
- Make acceptance criteria testable — a QA engineer should be able to verify each one
  without asking follow-up questions

**DON'T:**
- Invent metrics not in the PRD (if a number isn't in the source, say so)
- Skip the out-of-scope section (especially for regulated domains)
- Generate other epics yet
- Use vague acceptance criteria ("system performs well")

#### Refinement Phase

**DO:**
- Ask: "Would you like to adjust anything before we move on?"
- Listen for:
  - Scope changes ("move FR-8 to a separate epic")
  - Metric adjustments ("that target seems aggressive")
  - Missing acceptance criteria
  - Compliance gaps
- Iterate based on feedback

**DON'T:**
- Defend your draft
- Move on before user confirms

#### Transition Phase

**DO:**
- Save the epic to file: `output/epics/epic-{slug}.md`
- Show progress:
  ```
  Epics completed: ✓ Information Retrieval (RAG)
  Remaining: ○ Safety & Compliance, ○ Escalation, ○ Multi-Channel,
             ○ Context Management, ○ Analytics
  ```
- Offer next options:
  - Generate stories for this epic
  - Move to the next epic
  - Let user choose

**DON'T:**
- Force story generation before all epics are done (user directs)
- Assume linear order

### Phase 3: Story Decomposition

When user wants stories for an epic:

**DO:**
- Read the confirmed epic
- Identify 3-5 sprint-sized stories that implement the epic's acceptance criteria
- For each story, generate:
  - YAML frontmatter (title, parent_epic, summary, owner, priority, sprint,
    story_points, personas, dependencies, acceptance_criteria, tasks, links)
  - User story: "As a <persona>, I can <action> so that <benefit>"
  - Trigger scenario (what the user is doing)
  - Acceptance Criteria (Gherkin table: Given/When/Then with PRD references)
  - Non-Functional / Compliance Notes
  - Telemetry and Reporting
  - Dependencies
  - Risks and Mitigations
  - Rollout / Validation Checklist
  - Source References
- Present stories one at a time, confirm each before moving to next

**Story sizing guidelines:**
- Each story should be completable in a single sprint (1-2 weeks)
- If a story has more than 5 acceptance criteria, consider splitting
- If a story requires 3+ other stories to be done first, it's probably an epic
- Prefer vertical slices (thin end-to-end) over horizontal layers

**DON'T:**
- Generate all stories at once without checking in
- Create stories that aren't independently deliverable
- Use personas not defined in the PRD
- Skip compliance notes for stories touching data, auth, or safety

### Phase 4: Traceability Check

After generating stories for an epic:

**DO:**
- Show a traceability matrix:
  ```
  Epic AC → Story mapping:
  ✓ AC-1 (p90 < 5s) → story-natural-language-query
  ✓ AC-2 (citations) → story-natural-language-query
  ✓ AC-3 (mobile) → story-mobile-field-rep
  ✓ AC-4 (context) → story-multi-turn-conversation
  ⚠ AC-5 (index freshness) → no story yet — add one?
  ```
- Flag any epic acceptance criteria not covered by a story
- Ask if gaps should be filled or are intentional (deferred to later sprint)

**DON'T:**
- Skip the traceability check
- Assume all ACs need stories in this sprint (some may be deferred)

## Domain Adaptation

This skill adapts to the compliance domain of the PRD:

**Healthcare / Medical Device:**
- Include audit logging requirements in every story touching data
- Note PHI handling (or absence of PHI) explicitly
- Reference FDA, HIPAA, ISO standards where applicable
- Out-of-scope must explicitly state "no clinical advice" type guardrails

**Financial Services:**
- PCI-DSS and SOX compliance notes
- Data residency and encryption requirements
- Audit trail and retention policies

**General SaaS:**
- SOC 2 alignment
- GDPR/privacy considerations
- Performance SLAs

**Nonprofit / Social Services:**
- Privacy for vulnerable populations
- Accessibility (WCAG 2.1 AA)
- Multilingual requirements
- Trauma-informed design considerations

## Key Instructions

### DO:
- ✅ Cite PRD sections for every metric and acceptance criterion
- ✅ Make acceptance criteria atomic and testable
- ✅ Keep stories sprint-sized (independently deliverable)
- ✅ Track progress across the backlog
- ✅ Adapt compliance depth to the domain
- ✅ Save each artifact to file immediately after confirmation
- ✅ Show traceability (story → epic → PRD)
- ✅ Ask before moving on — user directs the workflow

### DON'T:
- ❌ Invent metrics not found in the PRD
- ❌ Generate the entire backlog at once
- ❌ Skip the confirmation step between artifacts
- ❌ Create stories with implicit dependencies that aren't tracked
- ❌ Use vague acceptance criteria ("system is fast")
- ❌ Forget out-of-scope (especially for regulated systems)
- ❌ Move on without user confirmation

## Output Structure

```
output/
  epics/
    epic-template.md
    epic-{capability-1}.md
    epic-{capability-2}.md
    ...
  stories/
    story-template.md
    story-{name-1}.md
    story-{name-2}.md
    ...
```

## Quality Standards

**Epics should have:**
- 3-5 measurable OKRs with PRD-traced targets
- 8-15 testable acceptance criteria
- Explicit out-of-scope section
- Monitoring metrics with alert thresholds

**Stories should have:**
- Single persona per story
- 3-5 Gherkin acceptance criteria
- Compliance notes (even if "N/A — no PHI involved")
- Estimated story points (2, 3, 5, or 8)
- Clear parent_epic linkage

**Traceability:**
- Every story links to its parent epic
- Every acceptance criterion cites a PRD section
- Every metric traces to PRD §1.6 or equivalent
- Gap analysis after each epic's stories are generated

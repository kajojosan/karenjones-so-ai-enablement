---
title: "<fill me>"
summary: "<fill me — 1-3 sentence human-readable summary>"
owner: "<fill me — primary owner or team>"
priority: "<fill me — P0 / P1 / P2>"
phase: "<fill me — e.g., Phase 1 (Pilot), Phase 2 (Scale)>"
personas:
  - "<fill me — e.g., Clinical Support Specialist>"
  - "<fill me>"
okrs:
  objective: "<fill me — single-sentence objective tied to business value>"
  key_results:
    - description: "<fill me — measurable key result>"
      target: "<fill me — numeric or qualitative target>"
      timeframe: "<fill me — e.g., 12 weeks>"
    - description: "<fill me>"
      target: "<fill me>"
      timeframe: "<fill me>"
    - description: "<fill me>"
      target: "<fill me>"
      timeframe: "<fill me>"
business_value: "<fill me — one-line description of business value>"
success_metrics:
  - "<fill me — e.g., response time < 5 min>"
  - "<fill me — e.g., first-contact resolution >= 70%>"
regulatory_requirements:
  - "<fill me — e.g., FDA 21 CFR Part 11 audit trail retention 7 years>"
  - "<fill me — e.g., no PHI stored or processed>"
  - "<fill me — e.g., ISO 13485 alignment>"
security_considerations:
  - "<fill me — e.g., Azure AD SSO, RBAC>"
  - "<fill me — e.g., TLS 1.3 in transit, AES-256 at rest>"
  - "<fill me — e.g., HIPAA compliance>"
dependencies:
  - "<fill me — external system, team, or document required>"
  - "<fill me>"
estimated_effort: "<fill me — e.g., 3-5 sprints>"
monitoring_metrics:
  - "<fill me — e.g., response time p90>"
  - "<fill me — e.g., answer accuracy %>"
  - "<fill me — e.g., hallucination rate>"
acceptance_criteria:
  - "<fill me — testable criterion>"
  - "<fill me>"
out_of_scope:
  - "<fill me — e.g., no clinical advice or diagnoses>"
  - "<fill me>"
stakeholders:
  - "<fill me — e.g., Product Manager>"
  - "<fill me — e.g., Regulatory Affairs>"
links:
  - "input/PRDs/<source-prd-filename>.md"
---

> **Reminder:** Cite the source PRD for all metrics, requirements, and acceptance criteria used in this epic. Traceability back to the PRD ensures alignment during reviews and audits.

---

## Summary

<fill me — 2-3 sentences describing the epic's intent, who it benefits, and the user problem it solves. Name the primary persona and the expected outcome.>

Example: "Enable support reps to retrieve concise, citation-backed device guidance from SharePoint within 5 minutes, reducing search time and increasing first-contact resolution. Primary persona: Clinical Support Specialist."

---

## OKRs

**Objective:** <fill me — single-sentence objective linking to business value and phase goals>

**Key Results:**

| # | Description | Target | Timeframe | PRD Reference |
|---|-------------|--------|-----------|---------------|
| KR-1 | <fill me> | <fill me> | <fill me> | PRD §<fill me> |
| KR-2 | <fill me> | <fill me> | <fill me> | PRD §<fill me> |
| KR-3 | <fill me> | <fill me> | <fill me> | PRD §<fill me> |
| KR-4 | <fill me — optional> | <fill me> | <fill me> | PRD §<fill me> |
| KR-5 | <fill me — optional> | <fill me> | <fill me> | PRD §<fill me> |

---

## Objective and Business Value

<fill me — describe how this epic advances the product goals stated in the PRD. Reference specific PRD outcomes (e.g., pilot readiness, regulatory compliance, adoption targets, cost savings). Quantify value where possible.>

---

## Personas Impacted

| Persona | Role | Primary Benefit |
|---------|------|-----------------|
| <fill me> | <fill me> | <fill me> |
| <fill me> | <fill me> | <fill me> |

---

## Acceptance Criteria

Provide clear, testable criteria. Keep each criterion atomic.

- [ ] <fill me — e.g., system returns a citation-backed response within 5 seconds (p90)>
- [ ] <fill me — e.g., response includes document name, section, and version date>
- [ ] <fill me — e.g., low-confidence responses (< 70%) trigger automatic escalation>
- [ ] <fill me — e.g., all queries and responses logged immutably for audit>
- [ ] <fill me>

> Cite PRD section for each criterion (e.g., "per PRD §2.1.1 FR-4").

---

## Validation / QA Plan

<fill me — describe test approaches:>

- **Unit / Integration Tests:** <fill me>
- **Sample Query Testing:** <fill me — e.g., 200-query test set with expected citations>
- **Manual Spot-Checks:** <fill me — e.g., weekly review against source documents>
- **Regulatory Review:** <fill me — e.g., compliance team sign-off before release>
- **User Acceptance Testing:** <fill me — e.g., pilot group of 5-10 users for 2 weeks>

---

## Monitoring and Metrics

| Metric | Target / Threshold | Alert Condition | Dashboard |
|--------|-------------------|-----------------|-----------|
| <fill me — e.g., Response time (p90)> | <fill me — e.g., < 5 seconds> | <fill me — e.g., > 8 seconds for 5 min> | <fill me> |
| <fill me — e.g., Answer accuracy> | <fill me — e.g., >= 95%> | <fill me — e.g., drops below 90%> | <fill me> |
| <fill me — e.g., Hallucination rate> | <fill me — e.g., < 2%> | <fill me — e.g., exceeds 3%> | <fill me> |
| <fill me — e.g., Escalation rate> | <fill me — e.g., < 10%> | <fill me — e.g., exceeds 15%> | <fill me> |
| <fill me — e.g., User satisfaction> | <fill me — e.g., > 4.2/5.0> | <fill me — e.g., drops below 3.5> | <fill me> |

---

## Out of Scope

- <fill me — e.g., no clinical advice or medical diagnoses>
- <fill me — e.g., no PHI storage or processing>
- <fill me — e.g., no off-label usage guidance>
- <fill me>

---

## Dependencies

| Dependency | Type | Owner | Status |
|------------|------|-------|--------|
| <fill me — e.g., SharePoint document libraries indexed> | System | <fill me> | <fill me> |
| <fill me — e.g., Azure AD tenant configuration> | Infrastructure | <fill me> | <fill me> |
| <fill me — e.g., Regulatory sign-off on guardrails> | Approval | <fill me> | <fill me> |
| <fill me — e.g., Dynamics 365 escalation API> | Integration | <fill me> | <fill me> |

---

## Stakeholders / Reviewers

| Name / Role | Responsibility |
|-------------|---------------|
| <fill me — e.g., Product Manager> | Epic owner, prioritization |
| <fill me — e.g., Regulatory Affairs> | Compliance review and sign-off |
| <fill me — e.g., QA Lead> | Validation plan approval |
| <fill me — e.g., IT Security> | Security review |
| <fill me — e.g., Field Support Lead> | User acceptance feedback |

---

## Notes and Links

- **Source PRD:** [<fill me — PRD title>](input/PRDs/<fill me>.md)
- **Architecture Diagram:** <fill me — link or path>
- **Related Epics:** <fill me>
- **Design Artifacts:** <fill me>
- **Meeting Notes / Decisions:** <fill me>

---

*Template version 1.0 — adapted for AI-Powered Medical Device Support Agent initiative.*

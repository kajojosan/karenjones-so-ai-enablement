---
title: "<fill me — short, descriptive story title>"
parent_epic: "<fill me — path to parent epic, e.g., output/epics/epic-natural-language-information-retrieval-rag.md>"
summary: "<fill me — one-line summary of what this story delivers>"
owner: "<fill me — assignee or team>"
priority: "<fill me — P0 / P1 / P2>"
sprint: "<fill me — sprint name or number>"
story_points: "<fill me — e.g., 2, 3, 5, 8>"
personas:
  - "<fill me — primary persona impacted>"
dependencies:
  - "<fill me — systems, APIs, or other stories that must be in place>"
acceptance_criteria:
  - "<fill me — atomic, testable criterion>"
  - "<fill me>"
  - "<fill me>"
tasks:
  - "<fill me — implementation task (dev)>"
  - "<fill me — test task>"
  - "<fill me — documentation task>"
links:
  - "<fill me — parent epic path>"
  - "input/PRDs/<source-prd-filename>.md"
---

> **Reminder:** Every story must link to its parent epic via the `parent_epic` field. Cite the originating PRD section (e.g., "per PRD §2.1.1 FR-3") for each acceptance criterion to maintain traceability from story → epic → PRD.

> **Compliance reminder:** For any story that touches query/response data, note the audit logging and PHI handling requirements relevant to this story. If the story introduces a new data flow, confirm no PHI is stored or exposed (per PRD §2.7). If the story surfaces content to users, confirm responses align with approved IFU labeling (per PRD §2.1.1 FR-5).

**Guidance:**
- Keep the user story to a single sentence following the format below.
- Include the parent epic path in `parent_epic` to link work to its epic.
- Put atomic, testable acceptance criteria in the Gherkin table (one scenario per row).
- Use `tasks` in the frontmatter to track implementation steps for sprint planning.
- Prefer numeric targets in acceptance criteria where possible.

---

## User Story

**As a** <fill me — persona from PRD §1.2>,  
**I can** <fill me — specific action the user performs>,  
**so that** <fill me — measurable benefit or outcome>.

---

## Acceptance Criteria

Use Gherkin-style scenarios. Each criterion must be independently testable.

| # | Given | When | Then | PRD Ref |
|---|-------|------|------|---------|
| AC-1 | <fill me — precondition/context> | <fill me — action/trigger> | <fill me — expected outcome> | PRD §<fill me> |
| AC-2 | <fill me> | <fill me> | <fill me> | PRD §<fill me> |
| AC-3 | <fill me> | <fill me> | <fill me> | PRD §<fill me> |
| AC-4 | <fill me — optional> | <fill me> | <fill me> | PRD §<fill me> |

**Performance criteria:**
- <fill me — e.g., p90 response time < 5 seconds (per PRD §2.1.2 NFR-1)>

**Failure / edge-case criteria:**
- <fill me — e.g., when no results found, system responds with "Information not found" and logs the gap>

---

## Non-Functional / Compliance Notes

> For a regulated medical device support system, document any audit logging, PHI handling, or safety constraints relevant to this story.

- **Audit Logging:** <fill me — e.g., all queries and responses logged immutably with timestamp and user ID; 7-year retention (per PRD §2.7)>
- **PHI Handling:** <fill me — e.g., no PHI stored or processed; sanitize user queries for analytics (per PRD §2.7)>
- **Regulatory Alignment:** <fill me — e.g., responses must align with approved IFU labeling; no medical advice (per PRD §2.1.1 FR-5)>
- **Security:** <fill me — e.g., RBAC enforced; SharePoint permissions respected (per PRD §2.1.1 FR-2, §2.1.2 NFR-2)>
- **Accessibility:** <fill me — e.g., WCAG 2.1 AA compliance (per PRD §2.1.2 NFR-6)>

---

## Telemetry and Reporting

| Signal | Description | Dashboard / Sink |
|--------|-------------|-----------------|
| <fill me — e.g., query_latency_p90> | <fill me — e.g., time from query submission to response render> | <fill me — e.g., Azure Application Insights> |
| <fill me — e.g., citation_present> | <fill me — e.g., boolean: response includes at least one citation> | <fill me> |
| <fill me — e.g., user_feedback> | <fill me — e.g., thumbs up/down rating on response> | <fill me> |

**Alerting:**
- <fill me — e.g., alert if p90 latency exceeds 8 seconds for 5 consecutive minutes>

---

## Dependencies

| Dependency | Type | Status | Blocking? |
|------------|------|--------|-----------|
| <fill me — e.g., Azure AI Search index populated> | Infrastructure | <fill me> | Yes / No |
| <fill me — e.g., Parent epic AC #3 delivered> | Story | <fill me> | Yes / No |
| <fill me — e.g., Graph API permissions approved> | Approval | <fill me> | Yes / No |

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| <fill me — e.g., retrieval returns outdated documents> | <fill me — Low/Med/High> | <fill me — Low/Med/High> | <fill me — e.g., display document version date; alert if doc > 2 years old> |
| <fill me — e.g., response includes ungrounded claim> | <fill me> | <fill me> | <fill me — e.g., strict grounding policy; hallucination detection pipeline> |
| <fill me> | <fill me> | <fill me> | <fill me> |

---

## Rollout / Validation Checklist

- [ ] Unit tests pass (coverage ≥ 80%)
- [ ] Integration tests pass against staging environment
- [ ] Manual QA spot-check completed (minimum <fill me> test queries)
- [ ] Performance validated under load (p90 < <fill me> seconds)
- [ ] Compliance review: audit logging confirmed operational
- [ ] Compliance review: no PHI exposed in logs or responses
- [ ] Regulatory sign-off obtained (if applicable to this story)
- [ ] User acceptance: <fill me> pilot users validated for <fill me> days
- [ ] Telemetry confirmed flowing to dashboards
- [ ] Rollback plan documented and tested
- [ ] Release notes updated

---

## Source References

- **PRD:** [Medical Device Support Agent PRD](input/PRDs/<fill me>.md)
- **PRD Sections:** §<fill me> (cite all sections referenced in acceptance criteria)
- **Parent Epic:** [<fill me — epic title>](<fill me — epic path>)
- **Design / Architecture:** <fill me — link to relevant diagrams or specs>
- **Related Stories:** <fill me — sibling stories in this epic>

---

*Template version 1.0 — AI-Powered Medical Device Support Agent program.*

---

## Example Story (Filled)

For reference, here is a completed story using this template:

```yaml
title: "Search by product name returns citation-backed results"
parent_epic: "output/epics/epic-natural-language-information-retrieval-rag.md"
summary: "Enable product-name queries to return concise answers with citations."
owner: "frontend-team"
priority: "P0"
sprint: "Sprint 3"
story_points: 3
personas:
  - "Clinical Support Specialist"
dependencies:
  - "Azure AI Search index populated with product documentation"
acceptance_criteria:
  - "Search returns results with 1-3 citations showing document name, section, and date"
  - "Results load in UI within p90 processing time <5s"
  - "If no results, system responds 'Information not found' and logs the gap"
tasks:
  - "Implement search API call to retrieval service"
  - "Render citations in response UI component"
  - "Add unit and integration tests"
  - "Verify audit logging captures query and response"
links:
  - "output/epics/epic-natural-language-information-retrieval-rag.md"
  - "input/PRDs/medical-device-support-agent-prd.md §2.1.1 FR-1, FR-3, FR-4"
```

**User Story:** As a Clinical Support Specialist, I can search by product name so that I quickly find device specs without manually searching multiple SharePoint libraries.

**Acceptance Criteria:**

| # | Given | When | Then | PRD Ref |
|---|-------|------|------|---------|
| AC-1 | User is authenticated via Azure AD | User types a product name in the search box | System returns a concise answer with 1–3 citations within 5 seconds (p90) | PRD §2.1.1 FR-1, NFR-1 |
| AC-2 | Results are displayed | User views the response | Each citation shows document name, section/page, and version date as clickable links | PRD §2.1.1 FR-4 |
| AC-3 | No relevant documents exist for the query | User submits a product name search | System returns "Information not found in available documentation" and logs the gap | PRD §2.4 |

**Non-Functional / Compliance Notes:**
- Audit Logging: Query and response logged with timestamp and user ID; 7-year retention (per PRD §2.7)
- PHI Handling: No PHI stored; product name queries do not contain patient data
- Security: SharePoint permissions enforced — user only sees results from authorized libraries (per PRD §2.1.1 FR-2)

---
title: "Information-not-found response with documentation gap logging"
parent_epic: "output/epics/epic-natural-language-information-retrieval-rag.md"
summary: "When the agent cannot find relevant content, it responds clearly to the user and logs the query as a documentation gap for Product Management review."
owner: "backend-team"
priority: "P0"
sprint: "Sprint 2"
story_points: 3
personas:
  - "Clinical Support Specialist"
  - "Product Manager"
dependencies:
  - "Azure AI Search index operational"
  - "Audit logging infrastructure in place"
acceptance_criteria:
  - "When no relevant documents are found (confidence below threshold), agent responds with 'I don't have information on that in the available documentation'"
  - "Query is logged as a documentation gap with topic classification"
  - "Agent never fabricates an answer when confidence is below threshold"
  - "Response offers alternative actions (escalate to human, try rephrasing)"
tasks:
  - "Implement confidence threshold logic (< 0.70 = no relevant content)"
  - "Design and implement 'information not found' response template with alternative actions"
  - "Implement documentation gap logging (query, timestamp, topic, user context)"
  - "Create gap log schema in analytics database"
  - "Write unit tests for threshold boundary cases"
  - "Write integration test: query with no matching documents"
links:
  - "output/epics/epic-natural-language-information-retrieval-rag.md"
  - "input/PRDs/medical-device-support-agent-prd.md"
---

## User Story

**As a** Clinical Support Specialist,  
**I can** receive a clear "information not found" response when the agent has no relevant documentation,  
**so that** I know immediately to escalate rather than receiving a fabricated answer that could mislead a healthcare professional.

**As a** Product Manager,  
**I can** review logged documentation gaps to see which questions the agent cannot answer,  
**so that** I can prioritize documentation improvements and close knowledge gaps.

**Trigger scenario:** A specialist asks about a newly launched product whose documentation has not yet been indexed. Instead of hallucinating an answer, the agent clearly states it has no information and logs the gap.

---

## Acceptance Criteria

| # | Given | When | Then | PRD Ref |
|---|-------|------|------|---------|
| AC-1 | Retrieval returns no chunks above the confidence threshold (0.70) | Response is generated | Agent responds: "I don't have information on that in the available documentation" (not a fabricated answer) | §2.4 Grounding Strategy |
| AC-2 | Agent returns "information not found" | Response is displayed to user | Response includes alternative actions: "Talk to Human" button and suggestion to rephrase | §2.1.1 FR-6 |
| AC-3 | An "information not found" event occurs | System processes the event | Query is logged to the documentation gap table with: query text, timestamp, user role, attempted topic classification | §2.1.1 FR-9 |
| AC-4 | Retrieval returns chunks but all below 0.70 confidence | Response is generated | Agent does NOT attempt to answer from low-confidence chunks; treats as "not found" | §2.4 |
| AC-5 | Gap log accumulates entries | Product Manager accesses gap report | Gaps are viewable, filterable by topic/frequency, and exportable | §2.1.1 FR-9 |

**Performance criteria:**
- "Information not found" response renders within p90 < 3 seconds (faster than a full generation cycle)

**Failure / edge-case criteria:**
- Agent never returns an empty response — always provides the "not found" message with next steps
- Hallucination rate maintained < 2% (this story is a key guardrail) (per PRD §1.6)

---

## Non-Functional / Compliance Notes

- **Audit Logging:** "Information not found" events logged alongside all other queries; 7-year retention (per PRD §2.7)
- **PHI Handling:** Gap log stores query text — ensure no PHI is present; sanitize customer identifiers before writing to gap analytics (per PRD §2.7)
- **Regulatory Alignment:** This story directly supports the strict grounding policy — agent must never fabricate information about medical devices (per PRD §2.4, §2.1.1 FR-5)
- **Safety:** "Not found" response is a critical safety guardrail; a false positive (answering when it shouldn't) is more dangerous than a false negative (saying "not found" when an answer exists)

---

## Telemetry and Reporting

| Signal | Description | Dashboard / Sink |
|--------|-------------|-----------------|
| not_found_rate | Percentage of queries resulting in "information not found" | QA Dashboard |
| gap_log_entries_daily | Count of new documentation gaps logged per day | Product Analytics |
| gap_topic_distribution | Topic classification breakdown of gaps | Product Analytics |
| hallucination_rate | Responses without valid source (should trend toward 0%) | QA Dashboard |
| not_found_to_escalation | % of "not found" events followed by "Talk to Human" click | Support Analytics |

**Alerting:**
- Alert if not_found_rate exceeds 20% (rolling 1-day) — may indicate index issue or missing content
- Alert if any response is generated when all chunks are below 0.70 confidence (grounding violation)

---

## Dependencies

| Dependency | Type | Status | Blocking? |
|------------|------|--------|-----------|
| Azure AI Search index operational with confidence scoring | Infrastructure | Required | Yes |
| Audit logging infrastructure (same as core query story) | Infrastructure | Required | Yes |
| Gap analytics database table/schema | Infrastructure | Required | No (can log to flat file initially) |
| Escalation button available in UI (can be stubbed) | Story | Nice-to-have | No |

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Confidence threshold too high — too many false "not found" responses | Medium | Medium | Tune threshold using the 200-query test set; start at 0.70, adjust based on precision/recall analysis |
| Confidence threshold too low — agent answers with poor-quality sources | Medium | High | Default to conservative (0.70); monitor hallucination rate; regulatory review of borderline cases |
| Gap log fills with noise (vague or off-topic queries) | Medium | Low | Add topic classification; filter out non-actionable queries in reporting layer |
| Product Manager never reviews gap log | Low | Medium | Weekly automated gap report emailed to PM; dashboard with top-10 unanswered topics |

---

## Rollout / Validation Checklist

- [ ] Unit tests pass for confidence threshold logic (boundary: 0.69 → not found; 0.70 → not found; 0.71 → attempt answer)
- [ ] Integration test: query with zero matching documents returns "information not found" message
- [ ] Integration test: query with only low-confidence chunks (< 0.70) returns "information not found"
- [ ] Verify "not found" response includes "Talk to Human" button and rephrase suggestion
- [ ] Verify gap log captures query text, timestamp, user role, and topic classification
- [ ] Hallucination rate on 200-query test set remains < 2%
- [ ] Compliance review: confirm no fabricated medical device information in any "borderline" case
- [ ] Product Manager confirms gap report is accessible and actionable
- [ ] Telemetry confirmed: not_found_rate and gap_log signals flowing
- [ ] Rollback plan: if threshold causes excessive "not found" responses, lower to 0.60 temporarily while investigating

---

## Source References

- **PRD:** [Medical Device Support Agent PRD](input/PRDs/medical-device-support-agent-prd.md)
- **PRD Sections:** §2.4 (Grounding Strategy — "I don't know" when no relevant docs), §2.1.1 FR-5 (clearly state when info unavailable), §2.1.1 FR-9 (flag documentation gaps), §1.6 (hallucination rate < 2%)
- **Parent Epic:** [Natural Language Information Retrieval (RAG)](output/epics/epic-natural-language-information-retrieval-rag.md)
- **Related Stories:** story-natural-language-query-with-citations (shares retrieval pipeline), story-dashboard-low-confidence (downstream consumer of gap log)

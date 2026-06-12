---
title: "Natural language query returns citation-backed answer"
parent_epic: "output/epics/epic-natural-language-information-retrieval-rag.md"
summary: "Clinical Support Specialists submit plain-English queries and receive concise, grounded answers with document citations within 5 seconds."
owner: "backend-team"
priority: "P0"
sprint: "Sprint 2"
story_points: 5
personas:
  - "Clinical Support Specialist"
dependencies:
  - "Azure AI Search index populated with SharePoint documents"
  - "Azure OpenAI Service (text-embedding-3-large + GPT-4o) provisioned"
  - "Microsoft Graph API permissions approved (Sites.Read.All)"
acceptance_criteria:
  - "User submits a natural language query and receives a concise answer within p90 < 5 seconds"
  - "Response includes 1-3 citations with document name, section/page, and version date"
  - "Response displays confidence level (High/Medium/Low)"
  - "Citations are clickable links that open the source document"
  - "All queries and responses logged immutably with timestamp and user ID"
tasks:
  - "Implement query endpoint accepting natural language input"
  - "Integrate hybrid retrieval (vector + keyword) via Azure AI Search"
  - "Implement response generation with strict grounding and citation formatting"
  - "Add confidence scoring based on retrieval relevance scores"
  - "Implement immutable audit logging for all queries/responses"
  - "Write unit tests for retrieval, generation, and citation formatting"
  - "Write integration tests against staging index"
links:
  - "output/epics/epic-natural-language-information-retrieval-rag.md"
  - "input/PRDs/medical-device-support-agent-prd.md"
---

## User Story

**As a** Clinical Support Specialist,  
**I can** ask a question in plain English about a medical device and receive a concise, citation-backed answer,  
**so that** I can resolve customer inquiries in under 5 minutes instead of spending 25 minutes searching multiple SharePoint libraries.

**Trigger scenario:** A healthcare facility calls asking about sterilization options for a specific device. The specialist types the question into the agent interface rather than manually searching 15+ document libraries.

---

## Acceptance Criteria

| # | Given | When | Then | PRD Ref |
|---|-------|------|------|---------|
| AC-1 | User is authenticated via Azure AD | User submits a plain-English query (e.g., "What are the sterilization options for Product X?") | System returns a concise answer within p90 < 5 seconds | §2.1.1 FR-1, §2.1.2 NFR-1 |
| AC-2 | System has retrieved relevant document chunks | Response is rendered | Response includes 1–3 citations with document name, section/page number, and version date | §2.1.1 FR-4 |
| AC-3 | Citations are displayed | User clicks a citation link | Source document opens in a new tab at the referenced section | §2.1.1 FR-4 |
| AC-4 | Retrieval returns results with varying relevance scores | Response is rendered | Confidence badge shows High (≥0.85), Medium (0.70–0.84), or Low (<0.70) | §2.1.1 FR-4 |
| AC-5 | Query contains medical terminology or layman's terms | User submits query | System handles both equivalently (e.g., "autoclave" and "sterilization machine") | §2.1.1 FR-1 |

**Performance criteria:**
- p90 processing time < 5 seconds (per PRD §2.1.2 NFR-1)
- Support 100 concurrent users without degradation (per PRD §2.1.2 NFR-1)

**Failure / edge-case criteria:**
- Multi-part questions are decomposed and each part addressed (per PRD §2.1.1 FR-1)
- Responses formatted with bullet points/numbered steps where appropriate (per PRD §2.1.1 FR-4)

---

## Non-Functional / Compliance Notes

- **Audit Logging:** Every query and response logged immutably with timestamp, user identity, session ID, and confidence score; 7-year retention (per PRD §2.7, §2.1.2 NFR-3)
- **PHI Handling:** No PHI stored. User queries may contain customer identifiers — sanitize before analytics aggregation (per PRD §2.7)
- **Regulatory Alignment:** Responses grounded strictly in source documents; no medical advice or clinical diagnoses; citations required for all factual claims (per PRD §2.1.1 FR-5, §2.4)
- **Security:** Azure AD SSO required; TLS 1.3 in transit; AES-256 at rest (per PRD §2.1.2 NFR-2)
- **FDA 21 CFR Part 11:** Audit trail must be tamper-evident and include user identity (per PRD §2.1.2 NFR-3)

---

## Telemetry and Reporting

| Signal | Description | Dashboard / Sink |
|--------|-------------|-----------------|
| query_latency_p90 | Time from query submission to response render | Azure Application Insights |
| citation_count | Number of citations returned per response | Azure Application Insights |
| confidence_level | Distribution of High/Medium/Low confidence responses | QA Dashboard |
| retrieval_relevance_avg | Average cosine similarity of top-5 retrieved chunks | Azure AI Search metrics |
| audit_log_write_success | Confirmation that query/response pair was logged | Azure Monitor |

**Alerting:**
- Alert if p90 latency exceeds 8 seconds for 5 consecutive minutes
- Alert if citation_count = 0 for any response (grounding violation)

---

## Dependencies

| Dependency | Type | Status | Blocking? |
|------------|------|--------|-----------|
| Azure AI Search index populated with chunked/embedded SharePoint docs | Infrastructure | Required | Yes |
| Azure OpenAI Service (GPT-4o + text-embedding-3-large) | Infrastructure | Required | Yes |
| Graph API permissions (Sites.Read.All) approved | Approval | Required | Yes |
| Azure AD SSO configured | Infrastructure | Required | Yes |
| Immutable audit log sink (Azure Monitor / CosmosDB) | Infrastructure | Required | Yes |

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Retrieval returns irrelevant chunks, producing low-quality answer | Medium | High | Hybrid search (vector + keyword) with semantic ranking; confidence threshold triggers "information not found" |
| Response includes ungrounded claim (hallucination) | Low | Critical | Strict grounding prompt; citation required for all claims; automated hallucination detection pipeline |
| Latency exceeds 5s under load | Medium | Medium | Load testing early; optimize chunk size; cache frequent queries |
| Audit log write fails silently | Low | High | Synchronous write with retry; alert on failure; circuit breaker |

---

## Rollout / Validation Checklist

- [ ] Unit tests pass (coverage ≥ 80% on retrieval and generation modules)
- [ ] Integration tests pass against staging Azure AI Search index
- [ ] 200-query test set: ≥ 95% accuracy against ground-truth answers
- [ ] Hallucination rate < 2% on test set
- [ ] Performance validated: p90 < 5 seconds at 100 concurrent users
- [ ] Compliance review: audit logging confirmed operational and tamper-evident
- [ ] Compliance review: no PHI exposed in logs or responses
- [ ] Regulatory Affairs confirms sample responses align with approved IFU
- [ ] Telemetry confirmed flowing to Application Insights dashboards
- [ ] Rollback plan documented (revert to previous API version)

---

## Source References

- **PRD:** [Medical Device Support Agent PRD](input/PRDs/medical-device-support-agent-prd.md)
- **PRD Sections:** §1.1, §1.6, §2.1.1 FR-1/FR-3/FR-4, §2.1.2 NFR-1/NFR-2/NFR-3, §2.4, §2.7
- **Parent Epic:** [Natural Language Information Retrieval (RAG)](output/epics/epic-natural-language-information-retrieval-rag.md)
- **Related Stories:** story-mobile-field-rep-search, story-multi-turn-conversation, story-information-not-found-gap-logging

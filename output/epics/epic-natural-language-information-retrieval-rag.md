---
title: "Natural Language Information Retrieval (RAG over SharePoint)"
summary: "Enable support users to ask plain-English questions and receive concise, citation-backed answers sourced from SharePoint technical documentation via vector retrieval and generation."
owner: "Product Manager, Support Intelligence Agent"
priority: "P0"
phase: "Phase 1 (Pilot)"
personas:
  - "Clinical Support Specialist"
  - "Field Sales Representative"
  - "Healthcare Professional (Surgeon/OR Staff)"
okrs:
  objective: "Reduce time-to-answer and improve answer quality for device support queries during the pilot."
  key_results:
    - description: "Reduce average response time for support queries"
      target: "<5 minutes (from current 25-minute baseline)"
      timeframe: "12 weeks"
    - description: "Citation-backed answer accuracy on validated test set"
      target: ">=95%"
      timeframe: "12 weeks"
    - description: "Hallucination rate (responses without valid source)"
      target: "<2%"
      timeframe: "12 weeks"
    - description: "First-contact resolution rate"
      target: ">=70% (from current 42%)"
      timeframe: "12 weeks"
    - description: "Processing response time (p90)"
      target: "<5 seconds"
      timeframe: "12 weeks"
business_value: "Dramatically reduce the 25-minute average search time per inquiry, increase first-contact resolution from 42% to 70%, and enable 24/7 support availability — allowing the existing 12 FTE team to absorb 300+ additional inquiries/month without headcount growth."
success_metrics:
  - "avg_response_time < 5 minutes end-to-end (PRD §1.6)"
  - "processing_time_p90 < 5 seconds (PRD §2.1.2 NFR-1)"
  - "answer_accuracy >= 95% against source documents (PRD §1.6)"
  - "hallucination_rate < 2% (PRD §1.6)"
  - "first_contact_resolution >= 70% (PRD §1.6)"
  - "user_satisfaction > 4.2/5.0 (PRD §1.6)"
regulatory_requirements:
  - "All responses must cite source documents — strict grounding policy (PRD §2.4)"
  - "Audit log retention: 7 years for all queries and responses (PRD §2.7)"
  - "FDA 21 CFR Part 11 compliance for audit trails (PRD §2.1.2 NFR-3)"
  - "ISO 13485 quality management system alignment (PRD §2.1.2 NFR-3)"
  - "No PHI stored or processed (PRD §2.7)"
  - "Responses must align with approved IFU labeling (PRD §1.4)"
security_considerations:
  - "Azure AD SSO authentication (PRD §2.1.2 NFR-2)"
  - "TLS 1.3 in transit, AES-256 at rest (PRD §2.1.2 NFR-2)"
  - "Respect SharePoint permission boundaries — users see only authorized content (PRD §2.1.1 FR-2)"
  - "RBAC enforced across all channels (PRD §2.1.2 NFR-2)"
  - "No PHI storage; sanitize user queries containing customer identifiers (PRD §2.7)"
  - "Data residency: US Azure regions only (PRD §2.7)"
dependencies:
  - "SharePoint Online document libraries (15+ libraries, ~2,000 documents)"
  - "Azure AI Search (vector index provisioning)"
  - "Azure OpenAI Service (embeddings: text-embedding-3-large; generation: GPT-4o)"
  - "Microsoft Graph API (SharePoint access, change notifications)"
  - "Azure AD tenant (SSO, RBAC configuration)"
  - "Azure Cosmos DB (conversation state)"
  - "Regulatory Affairs sign-off on guardrails and disclaimers"
estimated_effort: "4-6 sprints"
monitoring_metrics:
  - "response_time_p90 (processing)"
  - "end_to_end_resolution_time"
  - "answer_accuracy (weekly sample audit)"
  - "hallucination_rate"
  - "citation_coverage_rate"
  - "first_contact_resolution_rate"
  - "escalation_rate"
  - "user_satisfaction_score"
  - "index_freshness (time since last SharePoint sync)"
acceptance_criteria:
  - "User submits a natural language query and receives a concise answer within p90 processing time < 5 seconds (per PRD §2.1.2 NFR-1)"
  - "Every response includes 1-3 citations with document name, section, and version date (per PRD §2.1.1 FR-4, §2.5)"
  - "Response displays a confidence indicator (High/Medium/Low) derived from retrieval relevance scores (per PRD §2.1.1 FR-4)"
  - "System retrieves top 3-5 most relevant document chunks using hybrid vector + keyword search (per PRD §2.1.1 FR-3)"
  - "When no relevant content exists, agent returns 'Information not found in available documentation' and logs the gap (per PRD §2.4 Grounding Strategy)"
  - "Follow-up questions preserve conversation context for up to 20 turns (per PRD §2.1.1 FR-8)"
  - "SharePoint document permission boundaries are enforced — user never sees content they lack access to (per PRD §2.1.1 FR-2)"
  - "Document index updates within 1 hour of SharePoint modification via webhook subscription (per PRD §2.6)"
  - "All queries and responses are logged immutably with timestamp and user identity for 7-year retention (per PRD §2.7)"
  - "System supports 100 concurrent users without degradation (per PRD §2.1.2 NFR-1)"
out_of_scope:
  - "Clinical advice or medical diagnoses (per PRD §2.1.1 FR-5)"
  - "Off-label usage guidance (per PRD §2.1.1 FR-5)"
  - "PHI storage or processing (per PRD §2.7)"
  - "Voice input (deferred to future phase per PRD §2.1.1 FR-1)"
  - "Multilingual query support (English only for pilot)"
  - "Dynamics 365 escalation workflow (separate epic)"
  - "Analytics and knowledge gap reporting (separate epic)"
  - "Administration interface and configuration management (separate epic)"
stakeholders:
  - "Product Manager — epic owner, prioritization"
  - "Director of Customer Service — success metrics validation"
  - "VP of Quality & Regulatory — compliance review and sign-off"
  - "CISO — security review"
  - "Senior Product Manager — documentation gap insights"
  - "IT / Azure Platform Team — infrastructure provisioning"
links:
  - "context (ingestion)/medical-device-support-agent-prd.md"
---

## Summary

This epic delivers the core RAG (Retrieval-Augmented Generation) capability that allows Clinical Support Specialists, Field Sales Representatives, and Healthcare Professionals to ask natural language questions and receive concise, citation-backed answers sourced from SharePoint technical documentation. It addresses the current 25-minute average search time across 15+ fragmented document libraries by implementing hybrid vector and keyword retrieval over ~2,000 indexed documents, reducing response time to under 5 seconds (p90) while maintaining ≥95% answer accuracy against source materials. This is the foundational capability for the Phase 1 pilot.

---

## OKRs

**Objective:** Reduce time-to-answer and improve answer quality for medical device support queries, enabling the existing support team to resolve more inquiries at first contact during the 12-week pilot.

**Key Results:**

| # | Description | Target | Timeframe | PRD Reference |
|---|-------------|--------|-----------|---------------|
| KR-1 | Reduce average end-to-end response time | < 5 minutes (from 25-min baseline) | 12 weeks | PRD §1.6 Business Outcomes |
| KR-2 | Answer accuracy validated against source documents | ≥ 95% on 200-query test set | 12 weeks | PRD §1.6 Quality Metrics |
| KR-3 | Hallucination rate (responses without valid source) | < 2% | 12 weeks | PRD §1.6 Quality Metrics |
| KR-4 | First-contact resolution rate | ≥ 70% (from 42% baseline) | 12 weeks | PRD §1.6 Business Outcomes |
| KR-5 | Processing response time (p90) | < 5 seconds | 12 weeks | PRD §2.1.2 NFR-1 |

---

## Objective and Business Value

Customer support representatives currently spend 15–30 minutes per inquiry searching fragmented documentation across 15+ SharePoint libraries (PRD §1.1). This results in a 42% first-contact resolution rate, 1,200 tickets/month with 180 after-hours inquiries going unanswered, and an 8-week training ramp for new hires (PRD §1.3).

This epic delivers the foundational information retrieval capability that:

- **Reduces handle time by 80%** — from 25 minutes to under 5 minutes per inquiry, freeing capacity equivalent to 300+ additional inquiries/month without new headcount (PRD §1.6)
- **Increases first-contact resolution from 42% to 70%** — by surfacing accurate, citation-backed answers instantly rather than requiring multi-document manual search (PRD §1.6)
- **Enables 24/7 availability** — after-hours inquiries (180/month) receive immediate responses rather than waiting until next business day (PRD §1.6)
- **Reduces new-hire ramp** — from 8 weeks to 4 weeks by providing an always-available knowledge assistant (PRD §1.6)
- **Supports pilot readiness** — this is the core capability required for Phase 1 validation with real users

---

## Personas Impacted

| Persona | Role | Primary Benefit |
|---------|------|-----------------|
| Clinical Support Specialist | First-line customer support for healthcare facilities | Immediate access to device specs, troubleshooting, and surgical technique guidance without searching 15+ libraries manually |
| Field Sales Representative | On-site product specialist supporting surgeons | Real-time answers from mobile device during procedures and customer visits |
| Healthcare Professional (Surgeon/OR Staff) | End user of medical devices | Quick reference for device usage, troubleshooting, and compatibility in time-sensitive clinical situations |
| Regulatory Affairs Specialist (secondary) | Ensures compliance with FDA/ISO standards | Verifiable citations and audit trails demonstrating responses align with approved IFU |
| Product Manager (secondary) | Oversees product lifecycle | Visibility into documentation gaps via "information not found" logging |

---

## Acceptance Criteria

- [ ] User submits a natural language query in plain English (including medical terminology and layman's terms) and receives a concise answer within p90 processing time < 5 seconds (per PRD §2.1.1 FR-1, NFR-1)
- [ ] Every response includes 1–3 citations with: document name, section/page number, version date, and clickable link to source (per PRD §2.1.1 FR-4, §2.5 wireframe example)
- [ ] Response displays confidence level (High / Medium / Low) based on retrieval relevance scores (per PRD §2.1.1 FR-4)
- [ ] Retrieval uses hybrid search (vector similarity + keyword matching) with semantic ranking, returning top-5 relevant chunks prioritized by recency and relevance (per PRD §2.1.1 FR-3, §2.4)
- [ ] Multi-part questions are handled — system decomposes and addresses each part (per PRD §2.1.1 FR-1)
- [ ] Follow-up questions maintain conversation context for up to 20 turns; user can clear context to start a new topic (per PRD §2.1.1 FR-8)
- [ ] When no relevant content is found, agent responds with "I don't have information on that in the available documentation" and logs the gap for analytics (per PRD §2.4 Grounding Strategy)
- [ ] SharePoint permission boundaries are enforced — retrieval never surfaces content the authenticated user lacks access to (per PRD §2.1.1 FR-2)
- [ ] Document index updates within 1 hour of a SharePoint modification via Graph API webhook subscription (per PRD §2.6)
- [ ] System handles 100 concurrent users without degradation (per PRD §2.1.2 NFR-1)
- [ ] Uptime ≥ 99.5% during business hours (6am–8pm ET); ≥ 99.0% outside business hours (per PRD §2.1.2 NFR-1)
- [ ] All queries and responses are logged immutably with timestamp, user identity, and session ID; retained for 7 years (per PRD §2.7, §2.1.2 NFR-3)
- [ ] Agent never provides medical advice, clinical diagnoses, or off-label usage guidance; politely declines with alternative (per PRD §2.1.1 FR-5)
- [ ] Responses formatted for readability: bullet points, numbered steps, highlighted key information where appropriate (per PRD §2.1.1 FR-4)
- [ ] Mobile-responsive web interface functional on iOS and Android without zooming (per PRD §2.1.1 FR-7)

---

## Validation / QA Plan

- **200-Query Test Set:** Curated queries spanning device compatibility (28%), troubleshooting (24%), specifications (18%), and other categories. Each query has a validated ground-truth answer with expected source citations. Run weekly against the live system.
- **Accuracy Audit:** Weekly random sample of 50 production queries reviewed by a Clinical Support Specialist for factual correctness against source documents. Target: ≥95% accuracy.
- **Hallucination Detection:** Automated pipeline flags responses where cited documents do not contain the claimed information. Manual review of all flagged items. Target: <2%.
- **Permission Boundary Testing:** Verify with test accounts at different RBAC levels that retrieval never surfaces unauthorized content. Include negative test cases.
- **Performance Load Testing:** Simulate 100 concurrent users; measure p90 response time remains <5 seconds under load.
- **Index Freshness Verification:** Modify a SharePoint document and confirm the index reflects the change within 1 hour.
- **Regulatory Review:** Compliance team reviews 100 sample responses for alignment with approved IFU labeling and absence of medical advice before pilot launch.
- **User Acceptance Testing:** 5–10 Clinical Support Specialists use the system for 2 weeks during pilot; collect satisfaction scores and qualitative feedback.
- **Conversation Context Testing:** Validate multi-turn scenarios (up to 20 turns) maintain coherent context and do not leak information across sessions.

---

## Monitoring and Metrics

| Metric | Target / Threshold | Alert Condition | Dashboard |
|--------|-------------------|-----------------|-----------|
| Processing response time (p90) | < 5 seconds | > 8 seconds for 5 consecutive minutes | Azure Application Insights |
| End-to-end resolution time | < 5 minutes | > 10 minutes average (rolling 1-hour) | Support Analytics |
| Answer accuracy (weekly audit) | ≥ 95% | Drops below 90% in any weekly sample | QA Dashboard |
| Hallucination rate | < 2% | Exceeds 3% in any weekly sample | QA Dashboard |
| Citation coverage | 100% of factual claims cited | Any response without citation (auto-flagged) | Azure Monitor |
| First-contact resolution | ≥ 70% | Drops below 60% (rolling 1-week) | Dynamics 365 Reports |
| Index freshness | < 1 hour lag | > 2 hours since last successful sync | Azure Monitor |
| Concurrent users supported | 100 | Degradation detected at < 100 users | Load Monitor |
| Uptime (business hours) | ≥ 99.5% | Any unplanned downtime > 5 minutes | Azure Monitor |
| User satisfaction | > 4.2 / 5.0 | Drops below 3.5 (rolling 1-week) | Feedback Dashboard |
| Escalation rate | < 10% | Exceeds 15% (rolling 1-week) | Support Analytics |

---

## Out of Scope

- **Clinical advice or medical diagnoses** — agent will not interpret symptoms or recommend treatments (per PRD §2.1.1 FR-5)
- **Off-label usage guidance** — agent refuses and flags these requests (per PRD §2.1.1 FR-5)
- **PHI storage or processing** — no protected health information stored; queries sanitized for analytics (per PRD §2.7)
- **Voice input** — deferred to future phase (per PRD §2.1.1 FR-1)
- **Multilingual queries** — English only for Phase 1 pilot
- **Escalation workflow and Dynamics 365 ticket creation** — covered in separate epic
- **Analytics dashboards and knowledge gap reporting** — covered in separate epic
- **Administration interface** — covered in separate epic
- **Teams bot integration** — may be included in Phase 1 but scoped as a separate story set
- **Salesforce embedded integration** — Phase 2

---

## Dependencies

| Dependency | Type | Owner | Status |
|------------|------|-------|--------|
| SharePoint Online document libraries (15+ sites, ~2,000 docs) | Content | Product Documentation Team | Available |
| Azure AI Search instance provisioned | Infrastructure | IT / Azure Platform Team | Required |
| Azure OpenAI Service (text-embedding-3-large + GPT-4o) | Infrastructure | IT / Azure Platform Team | Required |
| Microsoft Graph API access (Sites.Read.All, Files.Read.All) | Integration | IT Security | Approval needed |
| Azure AD tenant configuration (SSO, RBAC) | Infrastructure | IT Security | Required |
| Azure Cosmos DB (conversation state storage) | Infrastructure | IT / Azure Platform Team | Required |
| Document processing pipeline (chunking, embedding) | Engineering | Development Team | To build |
| Regulatory Affairs sign-off on system prompts and guardrails | Approval | VP Quality & Regulatory | Required before pilot |
| 200-query test set with validated ground-truth answers | QA | QA Lead + Support SMEs | To create |
| SharePoint webhook subscriptions for change notifications | Integration | IT / Azure Platform Team | Required |

---

## Stakeholders / Reviewers

| Name / Role | Responsibility |
|-------------|---------------|
| Product Manager | Epic owner, prioritization, success criteria validation |
| Director of Customer Service | User acceptance, operational readiness, pilot coordination |
| VP of Quality & Regulatory | Compliance review, guardrail sign-off, audit trail verification |
| CISO | Security architecture review, permission boundary validation |
| Senior Product Manager | Documentation gap insights, content completeness |
| IT / Azure Platform Team Lead | Infrastructure provisioning, performance validation |
| QA Lead | Test set creation, accuracy auditing, validation plan execution |
| Field Sales Leadership (VP of Sales) | Mobile experience feedback, field user acceptance |

---

## Notes and Links

- **Source PRD:** [Medical Device Support Agent PRD](context%20(ingestion)/medical-device-support-agent-prd.md) — all metrics, requirements, and thresholds in this epic trace to this document
- **Key PRD Sections Referenced:**
  - §1.1 Problem Statement (search time, fragmentation)
  - §1.3 Current State Analysis (baseline metrics)
  - §1.6 Success Criteria (targets)
  - §2.1.1 Functional Requirements FR-1 through FR-4, FR-8
  - §2.1.2 Non-Functional Requirements NFR-1 through NFR-3
  - §2.4 Technical Specifications (retrieval strategy, grounding)
  - §2.6 Integration Points (Graph API, SharePoint)
  - §2.7 Data Management (retention, privacy)
- **Architecture:** Azure Foundry AI → Azure AI Search (hybrid retrieval) → Azure OpenAI (generation) → Web/Mobile/Teams channels
- **Related Epics:** Safety & Compliance, Escalation & Dynamics 365, Analytics & Knowledge Gaps, Context Management

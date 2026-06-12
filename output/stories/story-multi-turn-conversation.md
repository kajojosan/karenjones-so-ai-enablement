---
title: "Multi-turn conversation preserves context up to 20 turns"
parent_epic: "output/epics/epic-natural-language-information-retrieval-rag.md"
summary: "Support follow-up questions within a session, maintaining conversation context for up to 20 turns without requiring the user to repeat information."
owner: "backend-team"
priority: "P1"
sprint: "Sprint 3"
story_points: 5
personas:
  - "Clinical Support Specialist"
dependencies:
  - "story-natural-language-query-with-citations (core query endpoint)"
  - "Azure Cosmos DB provisioned for conversation state"
acceptance_criteria:
  - "Follow-up questions resolve correctly using prior conversation context for up to 20 turns"
  - "User can clear context and start a new topic without logging out"
  - "Context does not leak between separate user sessions"
  - "Session state stored securely in Cosmos DB with encryption at rest"
tasks:
  - "Implement session state persistence in Azure Cosmos DB"
  - "Add conversation history to retrieval/generation prompt (sliding window)"
  - "Implement 'Start New Topic' action that clears session context"
  - "Add session isolation tests (no cross-session leakage)"
  - "Write integration tests for 20-turn conversations"
  - "Implement audit logging for session lifecycle events"
links:
  - "output/epics/epic-natural-language-information-retrieval-rag.md"
  - "input/PRDs/medical-device-support-agent-prd.md"
---

## User Story

**As a** Clinical Support Specialist,  
**I can** ask follow-up questions that build on my previous queries within the same session,  
**so that** I can drill into a topic naturally without re-stating context each time.

**Trigger scenario:** A specialist asks "What are the sterilization options for Product X?" and then follows up with "What about shelf life after sterilization?" — the agent understands "sterilization" and "Product X" carry over from the first question.

---

## Acceptance Criteria

| # | Given | When | Then | PRD Ref |
|---|-------|------|------|---------|
| AC-1 | User asked a question in turn N | User asks a follow-up in turn N+1 that references prior context (e.g., "What about the shelf life?") | System resolves the follow-up using prior conversation context and returns a relevant answer | §2.1.1 FR-8 |
| AC-2 | User is at turn 20 of a conversation | User submits turn 21 | System gracefully handles by dropping the oldest turn(s) from context; response is still coherent | §2.1.1 FR-8 |
| AC-3 | User is mid-conversation | User clicks "Start New Topic" | Context is cleared; next query is treated as a fresh conversation | §2.1.1 FR-8 |
| AC-4 | Two users are active concurrently | User A asks a follow-up | User A's context contains only their own prior turns; no data from User B's session | §2.1.2 NFR-2 |
| AC-5 | Conversation state is stored | System writes to Cosmos DB | Data is encrypted at rest (AES-256) and associated with authenticated user ID | §2.1.2 NFR-2, §2.7 |

**Performance criteria:**
- Follow-up queries still return within p90 < 5 seconds (context injection does not degrade latency) (per PRD §2.1.2 NFR-1)

**Failure / edge-case criteria:**
- If Cosmos DB is temporarily unavailable, system degrades gracefully to single-turn mode and informs the user ("I can't access our conversation history right now — please include full context in your question")

---

## Non-Functional / Compliance Notes

- **Audit Logging:** Session creation, each turn, and session termination logged with timestamps; conversation history retained 7 years (per PRD §2.7, §2.1.2 NFR-3)
- **PHI Handling:** No PHI stored in conversation state; if user inadvertently includes patient identifiers, these are not persisted beyond the audit log (sanitized from analytics) (per PRD §2.7)
- **Security:** Session state encrypted at rest (AES-256); session tokens scoped to authenticated user; no cross-session data access possible (per PRD §2.1.2 NFR-2)
- **Data Retention:** Conversation summaries stored only with user opt-in; default is session-scoped (cleared on logout or timeout) (per PRD §2.1.1 FR-8)
- **Privacy:** Opt-in required for storing conversation summaries beyond session; GDPR right-to-erasure supported (per PRD §2.7)

---

## Telemetry and Reporting

| Signal | Description | Dashboard / Sink |
|--------|-------------|-----------------|
| session_turn_count | Number of turns per session (histogram) | Azure Application Insights |
| context_resolution_success | Whether follow-up correctly resolved prior context (sampled) | QA Dashboard |
| session_duration | Time from first to last turn in a session | Analytics Dashboard |
| clear_context_events | Count of "Start New Topic" actions per day | Azure Application Insights |
| cosmos_write_latency | Time to persist session state | Azure Monitor |

**Alerting:**
- Alert if cosmos_write_latency p90 exceeds 500ms (risk of degrading overall response time)
- Alert if cross-session leakage detected in automated test suite (critical)

---

## Dependencies

| Dependency | Type | Status | Blocking? |
|------------|------|--------|-----------|
| Core query endpoint operational (story-natural-language-query-with-citations) | Story | Required | Yes |
| Azure Cosmos DB provisioned and configured | Infrastructure | Required | Yes |
| Session token / Azure AD integration | Infrastructure | Required | Yes |

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Context injection increases latency beyond 5s threshold | Medium | Medium | Use sliding window (last 5 turns) rather than full history; summarize older turns |
| Cross-session data leakage | Low | Critical | Partition keys scoped to user+session; integration tests with concurrent sessions; security review |
| Cosmos DB unavailability degrades experience | Low | Medium | Graceful fallback to single-turn mode; user notification; retry logic |
| Long conversations drift off-topic, degrading retrieval quality | Medium | Low | "Start New Topic" prominently available; system suggests clearing context after 10+ turns if relevance drops |

---

## Rollout / Validation Checklist

- [ ] Unit tests pass for session state serialization/deserialization
- [ ] Integration test: 20-turn conversation maintains coherent context
- [ ] Integration test: "Start New Topic" fully clears context
- [ ] Security test: no cross-session leakage with 10 concurrent users
- [ ] Performance test: p90 < 5 seconds maintained at turn 20
- [ ] Cosmos DB encryption at rest verified
- [ ] Audit logging captures session lifecycle (create, turn, clear, terminate)
- [ ] Compliance review: opt-in mechanism for conversation summaries confirmed
- [ ] Graceful degradation tested (Cosmos DB unavailable scenario)
- [ ] Rollback plan: disable multi-turn, revert to stateless single-turn mode

---

## Source References

- **PRD:** [Medical Device Support Agent PRD](input/PRDs/medical-device-support-agent-prd.md)
- **PRD Sections:** §2.1.1 FR-8 (context management, 20 turns, clear context, opt-in summaries), §2.1.2 NFR-1 (performance), §2.1.2 NFR-2 (security/encryption), §2.7 (data retention, privacy)
- **Parent Epic:** [Natural Language Information Retrieval (RAG)](output/epics/epic-natural-language-information-retrieval-rag.md)
- **Related Stories:** story-natural-language-query-with-citations (prerequisite)

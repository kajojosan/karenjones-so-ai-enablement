---
title: "Mobile-responsive search for field representatives"
parent_epic: "output/epics/epic-natural-language-information-retrieval-rag.md"
summary: "Field Sales Representatives access the RAG agent from mobile browsers on-site and receive answers formatted for small screens."
owner: "frontend-team"
priority: "P0"
sprint: "Sprint 3"
story_points: 3
personas:
  - "Field Sales Representative"
dependencies:
  - "story-natural-language-query-with-citations (core query endpoint operational)"
  - "Azure AD SSO accessible from mobile browsers"
acceptance_criteria:
  - "Agent web interface is fully functional on iOS Safari and Android Chrome without horizontal scrolling or zooming"
  - "Citations and action buttons are tap-friendly (minimum 44x44px touch targets)"
  - "Response text is readable at default font size on devices ≥ 375px wide"
  - "Performance: p90 < 5 seconds on 4G cellular connection"
tasks:
  - "Implement responsive CSS (mobile-first breakpoints)"
  - "Optimize citation and confidence badge layout for small screens"
  - "Cross-device QA on iPhone 14/15, Samsung Galaxy S23, iPad"
  - "Run Lighthouse accessibility audit and resolve issues"
  - "Verify Azure AD SSO flow works on mobile browsers"
links:
  - "output/epics/epic-natural-language-information-retrieval-rag.md"
  - "input/PRDs/medical-device-support-agent-prd.md"
---

## User Story

**As a** Field Sales Representative,  
**I can** access the support agent from my mobile phone's browser and get answers formatted for a small screen,  
**so that** I can retrieve device specifications and competitive positioning while on-site with surgeons without needing a laptop.

**Trigger scenario:** A field rep is in an OR prep room and a surgeon asks about compatibility between two devices. The rep opens the agent on their phone and types the question, receiving a readable, citation-backed answer in seconds.

---

## Acceptance Criteria

| # | Given | When | Then | PRD Ref |
|---|-------|------|------|---------|
| AC-1 | User opens agent URL on iPhone (Safari) or Android (Chrome) | Page loads | Interface is fully usable without horizontal scroll or pinch-to-zoom | §2.1.1 FR-7 |
| AC-2 | User is on a mobile device | User submits a query | Response renders with readable text, tap-friendly citations, and confidence badge within 5 seconds | §2.1.1 FR-4, §2.1.2 NFR-1 |
| AC-3 | Response is displayed on mobile | User taps a citation link | Source document opens in a new tab/window | §2.1.1 FR-4 |
| AC-4 | User is on mobile | User views interface elements | All interactive elements meet WCAG 2.1 AA touch target minimums (44x44px) | §2.1.2 NFR-6 |
| AC-5 | User is on cellular (4G) connection | User submits a query | Response returns within p90 < 5 seconds | §2.1.2 NFR-1 |

**Performance criteria:**
- p90 response time < 5 seconds on 4G cellular (per PRD §2.1.2 NFR-1)
- Page weight optimized for mobile networks (< 500KB initial load)

**Failure / edge-case criteria:**
- If network drops mid-request, user sees a clear error message with retry option (not a blank screen)

---

## Non-Functional / Compliance Notes

- **Audit Logging:** Same as desktop — all mobile queries/responses logged with timestamp and user ID; 7-year retention (per PRD §2.7)
- **PHI Handling:** No PHI stored; mobile sessions do not cache sensitive data locally (per PRD §2.7)
- **Security:** Azure AD SSO enforced on mobile; no credential caching outside secure session cookies; TLS 1.3 (per PRD §2.1.2 NFR-2)
- **Accessibility:** WCAG 2.1 AA — screen reader compatible, sufficient color contrast, touch targets ≥ 44px (per PRD §2.1.2 NFR-6)

---

## Telemetry and Reporting

| Signal | Description | Dashboard / Sink |
|--------|-------------|-----------------|
| device_type | Mobile vs. desktop classification per session | Azure Application Insights |
| mobile_latency_p90 | Response time for mobile-classified sessions | Azure Application Insights |
| mobile_error_rate | Failed requests from mobile sessions | Azure Monitor |
| viewport_width | Screen width distribution for responsive breakpoint tuning | Analytics Dashboard |

**Alerting:**
- Alert if mobile_latency_p90 exceeds 8 seconds for 10 consecutive minutes
- Alert if mobile_error_rate exceeds 5% (rolling 1-hour)

---

## Dependencies

| Dependency | Type | Status | Blocking? |
|------------|------|--------|-----------|
| Core query endpoint operational (story-natural-language-query-with-citations) | Story | Required | Yes |
| Azure AD SSO works on mobile browsers (Safari, Chrome) | Infrastructure | Verify | Yes |
| Test devices available (iPhone, Android, iPad) | QA | Required | No (can use emulators initially) |

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Mobile latency higher than desktop due to network conditions | Medium | Medium | Optimize payload size; lazy-load non-critical elements; test on throttled connections |
| Azure AD SSO redirect fails on certain mobile browsers | Low | High | Test SSO flow on all target browsers early; provide fallback auth if needed |
| Small screen truncates long citations | Medium | Low | Implement collapsible citation cards with "show more" pattern |

---

## Rollout / Validation Checklist

- [ ] Responsive layout tested on iPhone 14/15 (Safari), Samsung Galaxy S23 (Chrome), iPad (Safari)
- [ ] Lighthouse accessibility score ≥ 90
- [ ] WCAG 2.1 AA manual audit passed (touch targets, contrast, screen reader)
- [ ] p90 latency < 5 seconds on simulated 4G connection
- [ ] Azure AD SSO confirmed working on all target mobile browsers
- [ ] Audit logging captures device_type metadata for mobile sessions
- [ ] No local caching of sensitive query/response data on device
- [ ] Field rep pilot: 3–5 reps use mobile agent on-site for 1 week; satisfaction ≥ 4.0/5.0
- [ ] Rollback plan: revert CSS changes without affecting desktop

---

## Source References

- **PRD:** [Medical Device Support Agent PRD](input/PRDs/medical-device-support-agent-prd.md)
- **PRD Sections:** §1.2 (Field Sales Representative persona), §2.1.1 FR-7 (multi-channel/mobile), §2.1.2 NFR-1 (performance), §2.1.2 NFR-6 (accessibility)
- **Parent Epic:** [Natural Language Information Retrieval (RAG)](output/epics/epic-natural-language-information-retrieval-rag.md)
- **Related Stories:** story-natural-language-query-with-citations (prerequisite)

# Product Requirements Document: Mary's Place Family Services Platform

**Organization:** Mary's Place Seattle  
**Product Name:** Family Services Platform (Virtual Shelter Advocate + Inventory & Goods Management)  
**Document Version:** 3.0  
**Date:** May 2026  
**Authors:** Solution Owner, Product Team

---

## Executive Summary

This document outlines requirements for a two-part technology platform to serve Mary's Place, a nonprofit operating family shelters and housing-stability programs in Seattle/King County. The platform comprises:

1. **Virtual Shelter Advocate** — An AI-powered intake and journey-mapping tool that guides families through assessments, prioritizes steps, estimates timelines, and supports multilingual, trauma-informed communication.

2. **Inventory & Goods Management System** — A real-time inventory tracking and distribution system that connects supply (warehouse/donations) to demand (families across shelter, outreach, and prevention programs), enables targeted corporate donations, and facilitates redistribution of excess goods to community partners.

Together, these solutions address Mary's Place's core operational challenges: increasing shelter throughput by streamlining the family journey, and maximizing the social impact of donated goods through better information flow.

---

## 1. Discovery

### 1.1 Problem Statement

Mary's Place ensures no child sleeps outside by providing emergency shelter, mobile outreach, and prevention services across King County. However, operational inefficiencies limit the organization's ability to serve families at scale:

**Shelter Throughput:**
- Length of stay is increasing due to housing affordability pressures in King County
- Manual intake process requires multiple separate team assessments (health, housing, youth services) conducted one-on-one with different staff members
- No centralized journey mapping — families cannot see a timeline, sequence of steps, or overall progress
- Staff cannot efficiently prioritize complex, multi-step pathways for each unique family
- No way to estimate journey duration or identify which long-lead processes (e.g., 3-month credit repair) should start on day one

**Goods Management & Distribution:**
- Only 15–20% of donated items are usable by Mary's Place families
- No inventory management system — tracking relies on manual bin counts, not SKU-level detail
- Inefficient information flow between supply (warehouse) and demand (families across all service areas)
- Unable to target corporate donations due to lack of real-time needs data
- Outreach and prevention families have no access to the distribution system available to shelter guests
- Excess unusable inventory accumulates with no redistribution path to other community organizations
- Ad hoc ordering — outreach specialists call the warehouse with no visibility into stock

**Technology Gaps:**
- Outdated 1990s-era SQL database system requiring significant in-house customization
- Double data entry — information manually entered into both internal system and county-wide HMIS
- No integration between internal database and county HMIS
- No cloud infrastructure currently deployed

### 1.2 User Personas

#### Primary Users

**Persona 1: Family in Shelter (Guest)**
- Context: Families experiencing homelessness, staying in Mary's Place emergency shelter
- Needs: Understand their journey, know what steps to take next, communicate in their native language, feel empowered and informed
- Pain Points: Overwhelmed by complexity, language barriers (12–15 languages at any time), trauma, multiple assessments with different teams
- Technical Proficiency: Variable; many have smartphones but limited digital literacy
- Languages: Multilingual population spanning 12–15 languages at any given time

**Persona 2: Housing Specialist (Navigator)**
- Role: Primary case manager and central point of contact for families
- Needs: See complete family picture, prioritize steps efficiently, coordinate across teams, track progress
- Pain Points: Manual coordination, double data entry, no centralized view of family journey
- Technical Proficiency: Medium; comfortable with basic systems

**Persona 3: Outreach Specialist**
- Role: Serves families in mobile outreach (living in cars/tents) transitioning to housing
- Needs: Request goods for families with short lead times, view available inventory, coordinate delivery
- Pain Points: No visibility into warehouse inventory, ad hoc ordering, hit-or-miss fulfillment
- Technical Proficiency: Medium; mobile-first workflows

**Persona 4: Warehouse/Goods Staff**
- Role: Receives, sorts, stores, and distributes donated goods
- Needs: Track inventory accurately, fulfill requests efficiently, identify redistribution opportunities
- Pain Points: Manual bin counts, no item-level tracking, overwhelmed with unusable donations
- Technical Proficiency: Low-medium; needs simple, clear interface

#### Secondary Users

**Persona 5: Development/Fundraising Team**
- Role: Manages corporate donor relationships and donation drives
- Needs: Real-time data on family needs to guide corporate donations, demonstrate impact
- Pain Points: Generic Amazon wish lists instead of targeted asks, unable to show donors precise impact

**Persona 6: Health Team / Youth Services Staff**
- Role: Conduct specialized assessments (health insurance, behavioral health, school enrollment)
- Needs: Access to family information gathered by other teams, schedule assessments at the right time in the journey
- Pain Points: Redundant questioning, poor sequencing of assessments

**Persona 7: IT Director / Data Team**
- Role: Manages technology infrastructure, maintains legacy database, runs reports
- Needs: Maintainable systems, data integrity, integration with county HMIS
- Pain Points: Legacy system burden, manual reporting, no automation

### 1.3 Current State Analysis

**Existing Systems:**
- Legacy SQL database (1990s-era, open-source, heavily customized in-house)
- County-wide Homelessness Management Information System (HMIS) — separate manual entry
- Microsoft Office suite (Windows infrastructure)
- Microsoft Copilot (early AI experiments — HR chatbot for benefits/handbook)
- Amazon wish lists (donation coordination)
- No cloud infrastructure (AWS or Azure)
- No inventory management system

**Current Process — Intake:**
1. Family enters shelter
2. Housing specialist conducts initial assessment (barriers, income, credit, debt)
3. Health team conducts separate assessment (insurance, care needs, behavioral health)
4. Youth services team assesses school and transportation needs
5. Each team enters data into the legacy database independently
6. Data is separately entered into HMIS (double entry)
7. Housing specialist acts as informal coordinator across teams
8. No unified timeline or step sequencing exists

**Current Process — Goods Distribution:**
1. Donations received at warehouse (community and corporate)
2. Staff manually sorts into categories and bins
3. Bins counted periodically for financial audit purposes (no SKU-level tracking)
4. Shelter guests access a "marketplace" for available items
5. Outreach specialists call warehouse to request items — no visibility into stock
6. Prevention families have no access to goods
7. Unusable items accumulate with no redistribution system

**Current Metrics (Estimated):**
- Shelter families served concurrently: Information needed
- Average length of stay: Increasing (exact baseline TBD)
- Intake assessment time: Multiple sessions across multiple teams over days/weeks
- Goods fulfillment rate for outreach families: Low (ad hoc, hit-or-miss)
- Donation utilization rate: 15–20%

### 1.4 Stakeholder Interviews Summary

**Jason Gortney (Chief Program and Innovation Officer):**
- Priority: Increase shelter throughput by streamlining the family journey
- Vision: AI-powered "Virtual Shelter Advocate" that assesses families, prioritizes steps, estimates timelines, and provides multilingual support
- Key insight: "If we had an AI that could understand all the barriers a family faces and prioritize — start the 3-month process on day one — that could make movement through shelter more efficient"
- Success metric: Reduced length of stay, more families sheltered with existing capacity

**Mike Komola (Chief HR and Operations Officer):**
- Priority: Solve the supply-to-demand information flow problem for goods distribution
- Vision: Centralized system connecting inventory to family needs across all service areas
- Key insight: "It's not availability of stuff — it's the process of getting it from where it is to where it needs to be"
- Success metric: Better fulfillment rates, targeted donations, redistribution to community

**Stakeholder-Stated Priorities:**
- A prototype or detailed concept with "enough meat" to shop for funding
- Help envisioning capabilities beyond what stakeholders have already imagined
- Follow-up discovery sessions needed with frontline staff (care coordinators, goods/distribution team)

### 1.5 Success Criteria

**Shelter Throughput:**
- Reduce average length of stay through better journey sequencing
- Decrease time from intake to first assessment milestone
- Enable capacity and demand forecasting

**Family Experience:**
- Families can engage with intake at their own pace
- Support in 12–15 languages with culturally attuned, trauma-informed communication
- Families understand their journey timeline and next steps

**Goods Distribution:**
- Increase fulfillment rate for outreach and prevention families
- Enable real-time inventory visibility across all staff
- Provide data-driven donation guidance to corporate partners

**Operational Efficiency:**
- Eliminate double data entry (internal system + HMIS)
- Reduce manual coordination burden on housing specialists
- Enable targeted corporate donation asks (replacing generic wish lists)

### 1.6 Prior Art

**Asylum Application Chatbot (Reference):**
- Built pro bono by Amazon Legal partners and a law firm
- Guided asylum-seeking families through the application in multiple languages
- Used trauma-informed UX
- Reduced attorney meeting time from 4 hours to 1 hour
- Proved the concept of AI-guided intake — directly inspired the Virtual Shelter Advocate idea
- No longer in active use (need has been met); not owned by Mary's Place

---

## 2. Synthesis

### 2.1 Solution Architecture Overview

The platform is organized into two products that share a common data layer:

**Product A: Virtual Shelter Advocate**
- AI-guided intake and assessment
- Journey mapping and step sequencing
- Timeline estimation
- Multilingual, trauma-informed interface
- Integration with staff workflows

**Product B: Inventory & Goods Management System**
- Real-time inventory tracking (item/SKU level)
- Centralized demand tracking across service areas
- Family-facing request interface
- Targeted donation guidance for development team
- Redistribution coordination for excess goods

**Shared Layer:**
- Unified family data model
- HMIS integration (eliminating double entry)
- Reporting and analytics
- User authentication and access control

### 2.2 Functional Requirements

#### Product A: Virtual Shelter Advocate

**FR-A1: AI-Guided Intake Assessment**
- Prompt families through comprehensive assessments (health, housing, youth services) in a single guided experience
- Allow families to complete at their own pace (not dependent on staff availability)
- Consolidate information that currently requires multiple team interactions
- Support pause/resume — families can stop and return later

**FR-A2: Multilingual Support**
- Support 12–15 languages reflecting the current family population
- Dynamically adapt available languages based on current shelter demographics
- Culturally attuned communication style (trauma-informed, empathetic tone)
- Consistent quality across all supported languages

**FR-A3: Journey Mapping & Prioritization**
- Analyze family-specific barriers (credit, health, employment, housing history)
- Generate a prioritized, sequenced action plan
- Identify long-lead processes and recommend starting them immediately
- Provide estimated timeline for the overall journey to rehousing
- Adapt plan as circumstances change

**FR-A4: Progress Tracking**
- Visual representation of the family's journey (steps completed, in progress, upcoming)
- Milestones and estimated completion dates
- Accessible to both families and their assigned staff
- Notifications when steps are due or overdue

**FR-A5: Staff Integration**
- Housing specialists, health team, and youth services can view the family's full picture
- Staff receive recommendations on when to schedule assessments (right time, right sequence)
- All information from AI-guided intake flows into the shared data system
- Staff can update progress, add notes, and adjust the plan

**FR-A6: Capacity & Demand Forecasting**
- Aggregate journey data to forecast shelter bed availability
- Estimate when families are likely to transition out
- Support resource planning for staff across teams

#### Product B: Inventory & Goods Management System

**FR-B1: Real-Time Inventory Tracking**
- Track goods at item/SKU level (replacing manual bin counts)
- Categorize by type, condition, suitability, and target population
- Support barcode/scanning for receiving and distribution
- Record donation source and date received

**FR-B2: Centralized Demand Tracking**
- Capture family needs across shelter, outreach, and prevention populations
- Match needs to available inventory
- Prioritize fulfillment based on urgency and availability
- Track fulfilled vs. unfulfilled requests

**FR-B3: Family-Facing Marketplace**
- Extend marketplace access to outreach and prevention families (not just shelter guests)
- Allow families to browse available items or submit requests
- Mobile-friendly interface
- Support multilingual access

**FR-B4: Outreach & Prevention Fulfillment**
- Enable outreach specialists to view inventory and request items for families
- Support short lead-time requests (days' notice when families move into housing)
- Track order status and delivery/pickup coordination
- "Make a Home" kit assembly and tracking

**FR-B5: Targeted Donation Guidance**
- Provide real-time dashboard of current family needs by category
- Equip development team with specific asks for corporate donors (replacing generic wish lists)
- Show donors the impact of their contributions
- Seasonal and trend-based forecasting of needs

**FR-B6: Redistribution Management**
- Identify goods unsuitable for Mary's Place families but valuable to community partners
- Catalog and categorize excess inventory
- Coordinate redistribution to other community organizations
- Track outbound donations for reporting

**FR-B7: Reporting & Analytics**
- Inventory turnover and aging reports
- Fulfillment rates by service area (shelter, outreach, prevention)
- Donation utilization rate
- Value tracking for financial audit compliance
- Community impact metrics

#### Shared Requirements

**FR-S1: HMIS Integration**
- Automated data sync between internal system and county-wide HMIS
- Eliminate manual double data entry
- Map internal data fields to HMIS required fields
- Support required demographic and outcome reporting

**FR-S2: Unified Family Record**
- Single view of family information across all service areas
- Assessment data, journey progress, goods requests, and case notes in one place
- Accessible to authorized staff across teams
- Maintain history and audit trail

**FR-S3: User Authentication & Access Control**
- Role-based access (family/guest, housing specialist, health team, warehouse staff, management)
- Secure authentication appropriate for each user type
- Family access does not require complex credentials (consider PIN, QR code, or phone-based auth)

### 2.3 Non-Functional Requirements

**NFR-1: Privacy & Security**
- Protect personally identifiable information (PII) for vulnerable populations including minors
- Data encryption in transit and at rest
- Access logging and audit trail for sensitive records
- Comply with any funder-mandated data handling requirements
- Data residency within the United States

**NFR-2: Accessibility & Inclusivity**
- WCAG 2.1 AA compliance
- Support for low digital literacy users (simple navigation, large text, clear icons)
- Mobile-first design (many families access via smartphones)
- Offline capability for basic functions (shelter environments may have limited connectivity)
- Support for assistive technologies (screen readers)

**NFR-3: Performance**
- Response time < 3 seconds for standard operations
- Support concurrent users across all shelter locations
- Reliable availability during operating hours (shelters are 24/7)

**NFR-4: Scalability**
- Support growth as Mary's Place expands services
- Design for potential adoption by other agencies (prototype scalable solutions)
- Handle increasing inventory volume and family count

**NFR-5: Maintainability**
- Solution must be maintainable by Mary's Place internal IT team after delivery
- Minimize dependency on specialized technical skills
- Configuration-driven where possible
- Clear documentation for administrators

**NFR-6: Integration**
- Microsoft ecosystem alignment (Office, Windows — existing infrastructure)
- HMIS integration (county system)
- Potential future integration with Amazon partnership systems
- API-based architecture for extensibility

**NFR-7: Trauma-Informed Design**
- Language and tone must be empathetic, non-judgmental, and empowering
- Interactions must not re-traumatize or feel clinical/institutional
- Families must feel in control of their information and journey
- Design reviewed by staff experienced in trauma-informed care

### 2.4 User Stories

**Epic A1: AI-Guided Intake**

- As a **family entering shelter**, I want to provide my information at my own pace in my own language so that I feel comfortable and in control of the process.
- As a **family entering shelter**, I want to understand what steps are needed for my journey to housing so that I feel motivated and informed.
- As a **housing specialist**, I want families to arrive at our first meeting with baseline information already gathered so that I can focus on the important work we need to do together.

**Epic A2: Journey Mapping**

- As a **family in shelter**, I want to see a timeline of my journey with clear next steps so that I know what to expect and can feel a sense of progress.
- As a **housing specialist**, I want the system to recommend which long-lead processes to start immediately so that families move through shelter as efficiently as possible.
- As a **program director**, I want to forecast shelter capacity based on projected family timelines so that I can plan bed availability.

**Epic B1: Inventory Management**

- As a **warehouse staff member**, I want to scan and track items as they arrive so that I know exactly what's available at any time.
- As an **outreach specialist**, I want to see what's in the warehouse before making a request so that I can set realistic expectations with families.
- As a **development team member**, I want real-time data on family needs so that I can make specific, targeted asks to corporate donors.

**Epic B2: Goods Distribution**

- As an **outreach specialist**, I want to place a request for a family moving into housing and get confirmation of what can be fulfilled so that the family gets what they need on time.
- As a **prevention family**, I want access to available goods so that I can get items I need to maintain housing stability.
- As a **warehouse manager**, I want to identify excess goods suitable for community redistribution so that nothing usable goes to waste.

---

## 3. Market & Competitive Analysis

### 3.1 Comparable Solutions in Nonprofit/Social Services

**Case Management Systems:**
- Apricot by Social Solutions — widely used in social services for case management
- Penelope by Athena Software — client information management for nonprofits
- CaseWorthy — configurable platform for human services

**Inventory/Goods Management for Nonprofits:**
- Link2Feed — food bank and goods distribution tracking
- Pantry Soft — inventory management for charitable distributions
- Custom solutions built on Salesforce Nonprofit Cloud

**AI in Social Services (Emerging):**
- Limited mature solutions exist for AI-guided intake in shelter/housing services
- Precedent: Asylum application chatbot (referenced in Prior Art) proved the concept
- Opportunity to lead in this space

### 3.2 Differentiation

The Mary's Place platform would be differentiated by:
- **AI-powered journey mapping** — no existing shelter management system offers intelligent step sequencing and timeline estimation
- **Multilingual, trauma-informed AI** — purpose-built for vulnerable populations rather than adapted from commercial customer service tools
- **Integrated supply-demand matching** — connecting goods inventory directly to tracked family needs across all service areas
- **Scalable design** — intended to extend beyond a single agency

### 3.3 Build vs. Buy Considerations

| Component | Recommendation | Rationale |
|-----------|---------------|-----------|
| AI Intake/Journey Mapping | Build (custom) | No existing solution offers this capability for shelter services |
| Inventory Management | Build or configure existing | Commercial inventory systems exist but may need adaptation for nonprofit donation workflows |
| HMIS Integration | Build (integration layer) | Must connect to county-specific system |
| Case Management | Evaluate existing platforms | May leverage existing nonprofit CMS as a foundation |

---

## 4. Risk Analysis

### 4.1 Risk Register

| Risk ID | Risk | Category | Likelihood | Impact | Mitigation |
|---------|------|----------|-----------|--------|------------|
| R001 | Families lack trust in AI-driven intake (prefer human interaction) | Adoption | Medium | High | Position as supplement to staff, not replacement; pilot with willing participants; always offer human alternative |
| R002 | Language/translation quality insufficient for sensitive topics | Technical | Medium | High | Use qualified translation services for validation; involve bilingual staff in testing; start with highest-need languages |
| R003 | Staff resistance to new workflows | Organizational | Medium | Medium | Involve frontline staff in design; demonstrate time savings; provide thorough training |
| R004 | Privacy breach exposing vulnerable population data | Security | Low | Critical | Encryption, access controls, security audit; minimize data collection; clear data retention policies |
| R005 | AI provides inappropriate or harmful guidance to families in crisis | Technical | Low | Critical | Human review of AI outputs; guardrails against medical/legal advice; escalation paths; extensive testing with social workers |
| R006 | Integration with legacy database proves prohibitively complex | Technical | Medium | High | Assess integration feasibility early; consider phased migration vs. direct integration |
| R007 | Funding not secured for full implementation | Business | Medium | High | Design modular solution allowing phased delivery; prototype demonstrates value for funding pitches |
| R008 | Limited internal IT capacity to maintain solution long-term | Organizational | Medium | Medium | Design for simplicity and maintainability; provide documentation; consider managed services |
| R009 | Families have limited device access or connectivity | Access | Medium | Medium | Support offline-capable features; provide shared devices at shelters; SMS-based fallback |
| R010 | Journey timeline estimates prove inaccurate, eroding trust | Technical | Medium | Medium | Frame estimates as ranges, not commitments; continuously calibrate with actual outcomes; set expectations clearly |

### 4.2 Critical Risk Mitigations

**R004 & R005 (Privacy and AI Safety):**
- No medical, legal, or crisis counseling advice from AI
- All AI-generated recommendations reviewed by staff before action
- Data minimization — collect only what's needed
- Regular security assessments
- Clear consent process for families

**R001 & R003 (Adoption):**
- Co-design with families and frontline staff
- Pilot program with willing participants before broad rollout
- Maintain human alternatives at all times
- Measure and communicate time savings

---

## 5. Technical Considerations

### 5.1 Technology Alignment

- **Microsoft ecosystem** — Mary's Place is a Microsoft shop (Office, Windows); solution should align
- **Amazon partnership** — deep relationship with Amazon (built 8-story shelter on campus); potential infrastructure or technical support
- **No existing cloud infrastructure** — solution must account for cloud adoption or on-premises hosting
- **AI/LLM capabilities** — leverage for multilingual communication, intake guidance, journey planning

### 5.2 Integration Points

- Legacy SQL database (read/write during transition period)
- County HMIS (automated data sync to eliminate double entry)
- Microsoft Office 365 (authentication, communication)
- Future: Amazon systems (wish list/donation coordination)

### 5.3 Infrastructure Decisions Needed

- Cloud hosting platform (Azure given Microsoft relationship, or AWS given Amazon partnership)
- Data migration strategy from legacy database
- Mobile delivery approach (native app vs. progressive web app)
- AI model hosting and selection

---

## 6. Timeline & Milestones

### Proposed Phasing

**Phase 0: Prototype & Funding (Months 1–3)**
- Develop concept with "enough meat" to secure funding
- Demonstrate Virtual Shelter Advocate vision
- Validate technical feasibility
- Conduct follow-up discovery with frontline staff

**Phase 1: Foundation (Months 4–6)**
- Establish cloud infrastructure
- Build unified family data model
- Implement HMIS integration (eliminate double entry)
- Deploy basic inventory tracking system

**Phase 2: Virtual Shelter Advocate MVP (Months 7–10)**
- AI-guided intake in top 3–5 languages
- Basic journey mapping and step sequencing
- Staff dashboard for viewing family progress
- Pilot with limited group of families

**Phase 3: Goods Management System (Months 8–11)**
- Real-time inventory tracking with scanning
- Request/fulfillment workflow for outreach specialists
- Extended marketplace access for outreach and prevention families
- Donation guidance dashboard for development team

**Phase 4: Enhancement & Scale (Months 12+)**
- Expand language support to full 12–15 languages
- Refine journey timeline estimation with real outcome data
- Redistribution coordination for community partners
- Capacity forecasting and advanced analytics
- Evaluate scalability to other agencies

---

## 7. Constraints & Dependencies

- **Budget:** Dependent on securing funding; prototype must demonstrate value
- **Internal IT Capacity:** Small team; solution must be maintainable without specialized skills
- **Legacy System:** 1990s database cannot be abandoned overnight; transition period required
- **HMIS Compliance:** County reporting requirements must be maintained throughout transition
- **Staff Capacity:** Change management and training required; staff already stretched thin
- **Privacy:** Vulnerable populations (including minors) require heightened data protection
- **Amazon Relationship:** Potential technical partnership must not create conflicts of interest

---

## 8. Open Questions

1. **Cloud Platform:** Azure (Microsoft relationship) or AWS (Amazon partnership) — or hybrid?
2. **Family Authentication:** How do families access the system securely without complex credentials?
3. **Device Access:** What devices are available to families? Shared tablets in shelter? Personal phones?
4. **Connectivity:** What is Wi-Fi/cellular reliability across shelter locations?
5. **Scale:** How many families are served concurrently across all service areas? How many shelter locations and beds?
6. **Staff Workflows:** Detailed process maps needed from frontline staff (care coordinators, warehouse team)
7. **Data Migration:** What data from the legacy system must be preserved? What can be left behind?
8. **HMIS Specifics:** What fields are required? Is there an API or is integration limited to file export?
9. **Funding Model:** What funding sources are targeted? What do funders need to see in a proposal?
10. **Maintenance Model:** Who will own and maintain the solution post-delivery? What's the internal capacity?
11. **Consent Framework:** How do families consent to data collection? Can they opt out of AI features while still receiving services?
12. **Success Baselines:** What are current measurable baselines for length of stay, fulfillment rates, and staff time allocation?

---

## 9. Next Steps

- [ ] Schedule follow-up discovery sessions with frontline staff (care coordinators, goods/distribution team)
- [ ] Document detailed current-state process maps (intake flow, goods fulfillment flow)
- [ ] Assess legacy database schema and HMIS integration requirements
- [ ] Determine cloud platform strategy
- [ ] Develop prototype/concept artifact for funding conversations
- [ ] Identify pilot group for Virtual Shelter Advocate testing
- [ ] Establish baseline metrics for success measurement

---

**Last Updated:** May 13, 2026  
**Status:** Draft — Discovery phase; pending follow-up stakeholder sessions

# Meeting Notes: Mary's Place Discovery Call
**Date:** November 14, 2025  |  **Duration:** 53 minutes
**Participants:** Jason Gortney (Chief Program & Innovation Officer), Mike Komola (Chief HR & Operations Officer), Casey Frith-Smith (Slalom), Lauren Milosky (Slalom)

## Meeting-Wide Summary

**Key Decisions Made:** 2 agreed, 1 tentative, 1 deferred
**Total Action Items:** 4 (2 assigned to Casey/Slalom, 2 requiring Mary's Place coordination)
**Open Questions:** 8 requiring follow-up
**Next Steps:** Slalom to follow up with email summarizing use cases; schedule follow-up calls with frontline staff (care coordinator, goods/distribution team)

---

## Feature: Virtual Shelter Advocate (AI-Guided Intake)

### Requirements
- AI-powered intake that prompts families through all assessment areas (health, housing, youth services) in a single guided experience (~min 12)
- Families can complete at their own pace, not dependent on staff availability (~min 13)
- System prioritizes steps: identifies long-lead processes (e.g., 3-month credit repair) and recommends starting them immediately (~min 16)
- Provides estimated journey timeline — "here's about how long we think your journey should be" (~min 17)
- Multilingual support across 12-15 languages with culturally attuned communication (~min 14-15)
- Trauma-informed, emotionally attuned interaction style — modeled after the asylum chatbot experience (~min 45)
- Information flows to all teams (housing, health, youth services) so they "could just cut to the important work" (~min 17)
- Scaffolds the experience — makes a complicated journey feel manageable (~min 13)
- No time limits on shelter stays; system adapts to each family's unique needs (~min 17)

### Decisions

> **Decision: Scope of AI intake tool**
> - Initial framing (~min 12): Jason described a "virtual advocate" that handles all assessments
> - Elaboration (~min 16): Emphasized prioritization and sequencing intelligence, not just data collection
> - **Status: Tentative** — strong vision from Jason, but needs frontline staff input before committing to scope

> **Decision: Desired deliverable from Slalom**
> - Jason's preference (~min 22): "A concept with enough meat on it" to shop for funding; also "help thinking through what a system like that could do" beyond what he's imagined
> - **Status: Agreed** — prototype or detailed concept for funding conversations

### Action Items
- [ ] Casey/Slalom: Follow up with email summarizing use cases heard *(next week)*
- [ ] Lauren/Slalom: Schedule follow-up call with a care coordinator for more detail on intake process
- [ ] Jason: Confirm availability of frontline staff for follow-up discovery

### Open Questions
- How do families currently access technology? (devices, connectivity in shelter)
- What does the legacy SQL database schema look like? Can it be integrated or must it be replaced?
- Is there an API for HMIS or only manual entry?
- What's the budget ceiling for Phase 1?
- How many families are served concurrently across all service areas?

### Key Quotes

> "One of the things I think about is it would be really cool to have some kind of like your virtual advocate or something that would sort of prompt you on all of that information." — Jason Gortney (~min 12)

> "If we had an AI that was really smart about understanding all the things that this family is facing in terms of barriers to becoming rehoused... we know that this particular thing takes like 3 months, so let's start that on day one." — Jason Gortney (~min 16)

> "It's a very complicated set of things that we have to do with people on a one-to-one basis with different team members." — Jason Gortney (~min 13)

> "Using technology to facilitate communication and those capabilities... to do what Jason described in a language in a communication style they're familiar with would also greatly add to enablement." — Mike Komola (~min 14)

### Stakeholder Alignment
- **Champions:** Jason (originated the idea, referenced it multiple times, compared it to the asylum chatbot success, visibly passionate)
- **Supportive:** Mike (added the multilingual requirement, agreed with the vision)
- **Concerns raised:** None explicitly — though the feasibility of building this was not discussed
- **Not heard from:** N/A (both Mary's Place stakeholders engaged)

### Dependencies
- Informs: Goods Distribution (families identified through intake may need goods)
- Depends on: Legacy system assessment (need to understand current data model)
- Prior art: Asylum application chatbot (proved concept, reduced attorney meeting from 4 hours to 1 hour)

---

## Feature: Inventory & Goods Management System

### Requirements
- Real-time inventory tracking at item/SKU level — replacing current bin-count system (~min 35)
- Centralized demand tracking connecting supply (warehouse) to demand (families across shelter, outreach, prevention) (~min 28)
- Outreach specialists need visibility into warehouse stock before making requests (~min 38)
- Prevention families need access to goods (currently excluded from distribution) (~min 37)
- System to identify and redistribute goods unsuitable for Mary's Place to other community organizations (~min 26)
- Short lead-time fulfillment — families moving into housing may give only days' notice (~min 40)
- "Make a Home" program coordination — sourcing household items for families transitioning to housing (~min 42)
- Marketplace concept extended beyond shelter to outreach and prevention populations (~min 41)
- Development team needs real-time data on family needs to guide targeted corporate donations (~min 31-33)

### Decisions

> **Decision: Who should have direct access to inventory?**
> - Discussion (~min 39): Lauren asked if families would have direct access or go through coordinators
> - Mike's response (~min 39): "We were just talking about this the other day" — envisioned giving families access to inventory information or ability to make requests
> - Evolved (~min 41): Combination of direct family access (marketplace concept for non-shelter) AND better information flow for staff
> - **Status: Tentative** — leaning toward hybrid (family self-serve + staff-mediated), discussed internally 2 days prior

> **Decision: What to do with unusable donations**
> - Position (~min 26): Don't refuse donations (development team values the relationships) but need to redistribute to community partners who can use them
> - Constraint: "It's not a simple matter of saying please don't give us stuff anymore" — donor relationships matter
> - **Status: Agreed** — redistribute, don't refuse; need logistics system to enable this

### Action Items
- [ ] Lauren/Slalom: Schedule follow-up call with goods/distribution team member
- [ ] Mike: Available for follow-up on warehouse operations detail

### Open Questions
- What categories/bins exist today? What's the current valuation system?
- How many community partner organizations could receive redistributed goods?
- What's the volume of goods flowing through (items per month)?
- Is barcode/scanning infrastructure feasible given warehouse setup?
- What's the staffing model for warehouse operations?

### Key Quotes

> "About 15 or 20% of that stuff is actually usable by our families, and the rest of that stuff is not. But we take it anyway." — Mike Komola (~min 25)

> "It's not the availability of stuff that's getting in our way. It's the process of getting it from where it is to where it needs to be." — Mike Komola (~min 29)

> "If the flow of information around from need through supply were coordinated, centralized, streamlined... then our development folks would be in a better position to focus and channel the giving energy to real needs, not perceived needs." — Mike Komola (~min 31)

> "Right now we do it with Amazon wish lists. Sort of generic, hey, we always need diapers. But if the flow of information was such that it's more targeted..." — Mike Komola (~min 32)

> "We have 20 cases of coats that are Eddie Bauer branded that you can only give away so many Eddie Bauer branded coats, right? So they're sitting in the warehouse." — Mike Komola (~min 33)

### Stakeholder Alignment
- **Champions:** Mike (this is his #1 operational challenge, deeply knowledgeable about the problem, returned to it multiple times with increasing detail)
- **Supportive:** Jason (agreed, deferred to Mike's expertise on operations)
- **Concerns raised:** Mike noted resource/staffing constraints — "it takes resources and time and effort"
- **Not heard from:** N/A

### Dependencies
- Depends on: No existing inventory system (greenfield build or purchase)
- Informs: Development/fundraising team (targeted donation asks)
- Connects to: "Make a Home" program (Olga's household sourcing workflow)
- Connects to: Virtual Shelter Advocate (families identified through intake have goods needs)

---

## Feature: Technology Infrastructure & Data Systems

### Requirements
- Eliminate double data entry between internal system and county HMIS (~min 20)
- Integration with or migration from legacy 1990s SQL database (~min 47-48)
- Microsoft ecosystem alignment (Office, Windows infrastructure) (~min 48)
- Current AI experiments: Copilot for HR chatbot (benefits, handbook, policies) (~min 49)
- No cloud infrastructure currently deployed (no AWS or Azure) (~min 47)

### Decisions

> **Decision: Technology platform**
> - Current state: Microsoft shop, no cloud infrastructure, legacy open-source SQL database
> - Relationship: Deep Amazon partnership (built 8-story shelter on campus) but no AWS deployment
> - **Status: Deferred** — no platform decision made; needs further assessment

### Action Items
- [ ] Slalom: Assess integration/migration feasibility as part of use case evaluation

### Open Questions
- Is Azure or AWS the right cloud platform given both Microsoft and Amazon relationships?
- Can the legacy database be integrated via API or does it require replacement?
- What's the IT team's capacity for managing new systems?
- Is the HMIS county system accessible via API?

### Key Quotes

> "It's an open source database model that was developed by a homeless services provider... it looks like something from the 1990s. It's an old SQL database." — Jason Gortney (~min 47)

> "Duplicate data entry." — Mike Komola (~min 20)

> "We're training copilot for HR applications right now with just basic chatbot functionality... we're just experimenting." — Mike Komola (~min 49)

### Stakeholder Alignment
- **Champions:** Neither — this is recognized as a constraint, not a passion area
- **Supportive:** Both acknowledged the need for modernization
- **Concerns raised:** Implicit concern about internal IT capacity ("we have an internal IT team that primarily manages our hardware")
- **Not heard from:** IT Director (not on this call but mentioned)

### Dependencies
- Blocks: All other features depend on infrastructure decisions
- External: County HMIS system (mandatory reporting)
- Relationship: Amazon partnership may provide infrastructure or technical support

---

## All Action Items (Consolidated)

**Slalom (Casey/Lauren):**
- [ ] Follow up with email summarizing use cases heard
- [ ] Schedule follow-up call with care coordinator (intake process detail)
- [ ] Schedule follow-up call with goods/distribution team member
- [ ] Assess technology/integration feasibility

**Mary's Place (Jason/Mike):**
- [ ] Jason: Confirm frontline staff availability for follow-up calls
- [ ] Mike: Available for warehouse operations follow-up

---

## All Open Questions (Consolidated)

1. How do families currently access technology? (devices, Wi-Fi in shelter?)
2. What does the legacy SQL database schema look like? Integration or replacement?
3. Is there an API for county HMIS or only manual data entry?
4. What's the budget ceiling for Phase 1?
5. How many families served concurrently across all service areas?
6. What categories/bins exist in the current warehouse system?
7. How many community partners could receive redistributed goods?
8. What's the IT team's capacity for ongoing system maintenance?

---

## All Key Quotes (Consolidated)

> "About 15 or 20% of that stuff is actually usable by our families, and the rest of that stuff is not. But we take it anyway." — Mike Komola (~min 25)

> "If we had an AI that was really smart about understanding all the things that this family is facing in terms of barriers to becoming rehoused... we know that this particular thing takes like 3 months, so let's start that on day one." — Jason Gortney (~min 16)

> "It's not the availability of stuff that's getting in our way. It's the process of getting it from where it is to where it needs to be." — Mike Komola (~min 29)

> "One of the things I think about is it would be really cool to have some kind of like your virtual advocate." — Jason Gortney (~min 12)

> "If the flow of information around from need through supply were coordinated, centralized, streamlined... then our development folks would be in a better position to focus and channel the giving energy to real needs, not perceived needs." — Mike Komola (~min 31)

> "It's an old SQL database... It looks like something from the 1990s." — Jason Gortney (~min 47)

> "We have 20 cases of coats that are Eddie Bauer branded that you can only give away so many Eddie Bauer branded coats." — Mike Komola (~min 33)

---

## Stakeholder Summary

**Jason Gortney (Chief Program & Innovation Officer)**
- **Championed:** Virtual Shelter Advocate / AI-guided intake — this is his vision and passion area
- **Energy level:** High — animated when describing the concept, drew on the asylum chatbot as proof of concept
- **Concerns:** None raised explicitly; focused on possibility and vision
- **Key insight:** Thinks bigger than just automation — wants the AI to help families build life skills ("scaffolding that experience")

**Mike Komola (Chief HR & Operations Officer)**
- **Championed:** Inventory & goods management — his #1 operational challenge, deeply detailed knowledge
- **Energy level:** High — needed prompting to start ("now you got me") but then provided extensive, structured detail
- **Concerns:** Staffing/resource constraints for implementation; donor relationship sensitivity
- **Key insight:** Frames the problem as information flow, not supply — "it's not the availability of stuff"

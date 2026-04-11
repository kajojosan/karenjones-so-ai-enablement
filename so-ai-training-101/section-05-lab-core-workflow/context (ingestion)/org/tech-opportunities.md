# Mary's Place — Technology Opportunities

## Proposed Product Solutions

### Virtual Shelter Advocate (AI-Powered Intake & Journey Mapping)
- AI-driven intake tool that prompts families through assessments (health, housing, youth services) at their own pace
- Consolidates multiple team assessments into a single guided experience
- Prioritizes and sequences steps based on family-specific barriers (e.g., starts 3-month processes on day one)
- Estimates an overall timeline for the family's journey through shelter to rehousing
- Multilingual support across 12–15 languages to match the family population at any given time
- Culturally attuned, trauma-informed communication style (modeled after the asylum-application chatbot)
- Enables capacity and demand forecasting for Mary's Place internally

### Inventory & Goods Management System
- Real-time inventory tracking at item/SKU level (replacing manual bin counts)
- Centralized demand tracking across shelter, outreach, and prevention populations
- Marketplace concept extended to outreach and prevention families — not just shelter guests
- Family-facing access to inventory information or a request/ordering interface
- Coordination layer between supply (warehouse) and demand (families across all service areas)
- Targeted donation guidance — equip the development team to tell corporate donors exactly what is needed
- Redistribution system to route unusable-for-MP goods to other community organizations

## Pain Points Suggesting Technology Needs

- **Double data entry** — no integration between the internal database and the county-wide HMIS
- **Outdated database** — open-source 1990s-era SQL system, heavily customized in-house, visually and functionally clunky
- **No centralized journey mapping** — families navigate multiple teams with no unified view of steps, timelines, or progress
- **No inventory management system** — warehouse tracking is manual (bin counts + financial audit-driven valuations)
- **Ad hoc fulfillment for non-shelter families** — outreach specialists call the warehouse with no visibility into stock; hit-or-miss results
- **Short lead times** — often only days' notice when a family moves into housing; better information flow could enable proactive sourcing
- **Inefficient donation utilization** — only 15–20% of donated goods are usable; excess accumulates with no redistribution path
- **Generic donation asks** — Amazon wish lists are broad ("we always need diapers") rather than driven by real-time family needs

## Existing Technology Relationships & Constraints

- **Microsoft shop** — Office suite, Windows infrastructure; using Microsoft Copilot for early AI experiments (HR chatbot for benefits/handbook)
- **Amazon partnership** — deep relationship (Amazon built an 8-story shelter on campus); Amazon Legal facilitates pro bono work; Amazon wish lists used for donation coordination
- **No cloud infrastructure** — not currently deployed on AWS or Azure; no sophisticated cloud-based tech stack
- **Internal IT team** — manages hardware, software contracts; strategic and experienced IT director
- **Internal data team** — maintains the legacy database, runs queries and reports, stewards data collection
- **HMIS (county system)** — required reporting destination; currently requires separate manual entry

## Prior Art: Asylum Application Chatbot
- Built pro bono by Amazon Legal partners and a law firm
- Walked asylum-seeking families through the application in multiple languages with trauma-informed UX
- Reduced attorney meeting time from 4 hours to 1 hour
- Proved the concept of AI-guided intake — directly inspired the virtual shelter advocate idea
- Not owned by Mary's Place; no longer in active use (need has been met)

## Stakeholder-Stated Priorities
- A prototype or detailed concept with "enough meat" to shop for funding
- Help envisioning capabilities beyond what stakeholders have already imagined
- Follow-up discovery sessions with frontline staff (care coordinators, goods/distribution team)

## Open Questions

**1. Users & Personas**
- Who are the staff roles that would use the system day-to-day? (housing specialists, health team, outreach specialists, warehouse staff, the "Make a Home" coordinator, data team, development/fundraising team)
- How many staff per role? What's their tech literacy?
- Family/guest personas — demographics, device access, connectivity, digital literacy

**2. Scale & Volume**
- How many families are served concurrently across shelter, outreach, and prevention?
- Number of shelter locations and beds
- Warehouse volume — how many donations received per week/month? How many bins/items flow through?
- Staff headcount

**3. Current Workflows (Process Maps)**
- Step-by-step intake flow today (who does what, in what order, how long each step takes)
- Goods request-to-fulfillment flow for shelter marketplace vs. outreach vs. Make a Home
- HMIS reporting workflow and what data fields are required

**4. Data & Systems Inventory**
- Name/vendor of the legacy SQL database
- What data it actually stores (schema or field-level detail)
- HMIS system specifics and API availability
- Other tools in use (spreadsheets, shared drives, scheduling tools, communication platforms)

**5. Constraints & Compliance**
- Privacy/data handling requirements (PII for vulnerable populations, minors)
- Any regulatory or funder-mandated reporting requirements beyond HMIS
- Data residency or security policies
- Accessibility requirements (ADA, WCAG)

**6. Budget & Resourcing**
- Budget range or funding model for a technology initiative
- Who would own/maintain the solution after delivery?
- Internal capacity to support change management and training

**7. Success Metrics**
- How would Mary's Place measure whether the solution is working? (e.g., reduced length of stay, faster intake, higher fulfillment rate, fewer manual hours)
- Current baselines for those metrics


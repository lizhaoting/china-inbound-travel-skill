# China Inbound Travel Skill: Requirements Document

> Version: 0.1 (planning) | 28 October 2026
> Intended hosts: Codex, Claude, and other agents that support `SKILL.md` / Agent Skills
> Research base: [164 distinct sources](china-travel-skill-research/sources.md). Of these, 144 pages were directly accessible (including the Agent Skills specification). Another 20 relevant GitHub repositories were identified through repository search, but direct repository pages timed out in this environment. Sources were screened for reachability and topical relevance; travel rules and platform capabilities still require a fresh check for each trip.

## 1. Product Definition

**Goal:** Help international visitors ask travel questions in their own language and receive actionable, evidence-backed guidance for China, with particular attention to entry, payments, connectivity, ticketing, transport, accommodation, and attraction reservations. Every primary recommendation should have a workable fallback when a common dependency fails.

This is an **agent workflow and reference set**, not a standalone app, ticketing system, or static encyclopedia. It should help an agent identify the travel phase, ask for only the conditions that affect the answer, select appropriate sources, and turn verified information into steps a visitor can follow.

### Target Users

| User | Typical task | Main obstacle |
| --- | --- | --- |
| First-time independent visitor | Check entry options, prepare payments, plan the first day | Unfamiliar local platforms, changing rules, Chinese addresses |
| Multi-city traveler | Compare trains and flights, buy tickets, connect stations and hotels | Passport names, station names, transfer time, refund rules |
| Visitor already in China | Fix a failed payment, lost connection, missed train, or reservation problem | Time pressure, language barriers, need for an immediate fallback |
| Family or traveler with specific needs | Plan around children, older travelers, accessibility, or dietary needs | Facility availability, pace, and differences between providers |

### Scope Boundaries

- Do not guarantee visa or visa-free eligibility. Consular authorities and border officials make the final determination.
- Do not treat search snippets, historical prices, seat availability, opening hours, or screenshots as live facts.
- Do not log in, enter identity or payment details, or submit an order by default. If the host has suitable tools and the user explicitly delegates the task, the agent may assist up to a reviewable step; show the material order details before payment or an irreversible submission.
- Do not attempt to maintain a static database of every Chinese city, attraction, and restaurant. The first release should focus on reusable workflows and selected city examples.

## 2. Research Findings and Product Implications

| Finding | Requirement implied | Representative sources |
| --- | --- | --- |
| Unilateral visa exemptions, mutual exemptions, transit exemptions, and other entry routes have different conditions. Nationality alone is insufficient to determine an individual's eligibility. | Identify the relevant entry route, then check passport, date, port, itinerary, duration, and official wording. | [S025](china-travel-skill-research/sources.md#s025), [S028](china-travel-skill-research/sources.md#s028), [S032](china-travel-skill-research/sources.md#s032), [S042](china-travel-skill-research/sources.md#s042) |
| Online arrival card and accommodation registration channels exist, while fraudulent entry points are a documented risk. | Label official entry points, verify links before use, and distinguish hotel registration from stays outside hotels. | [S023](china-travel-skill-research/sources.md#s023), [S029](china-travel-skill-research/sources.md#s029), [S031](china-travel-skill-research/sources.md#s031), [S155](china-travel-skill-research/sources.md#s155) |
| Both 12306 and third-party booking channels are used. Passport-name entry, identity checks, changes, and refunds create concrete friction. | Compare official and third-party channels by task; give a checklist for names, stations, documents, ticket status, and changes. | [S103](china-travel-skill-research/sources.md#s103), [S107](china-travel-skill-research/sources.md#s107), [S117](china-travel-skill-research/sources.md#s117), [S153](china-travel-skill-research/sources.md#s153) |
| Payments, phone numbers, connectivity, maps, and local services depend on one another. A single-app recommendation can fail at the next step. | Perform a combined readiness check for payment, connection, phone number, and navigation; provide independent fallbacks. | [S114](china-travel-skill-research/sources.md#s114), [S115](china-travel-skill-research/sources.md#s115), [S145](china-travel-skill-research/sources.md#s145), [S146](china-travel-skill-research/sources.md#s146) |
| Existing travel Skills tend to collect constraints in phases, verify changing facts, and deliver an executable itinerary. | Reuse those workflow ideas while centering the distinct problems of an international visitor using Chinese local services. Keep the entrypoint concise. | [S005](china-travel-skill-research/sources.md#s005), [S010](china-travel-skill-research/sources.md#s010), [S016](china-travel-skill-research/sources.md#s016), [S166](china-travel-skill-research/sources.md#s166) |

**Evidence rule:** Use government agencies and platform operators to confirm policies and platform rules. Use commercial guides to discover pain points, terminology, and fallback paths. Never bake a commercial article's fare, promotion, opening hour, country count, or payment support claim into the Skill as a permanent fact. Multiple articles from one publisher do not constitute independent institutional confirmation.

## 3. Invocation and Operating Modes

The Skill description should cover pre-trip preparation for international visitors to China, travel planning within China, use of Chinese consumer platforms, and problem solving during a trip. It should activate only when the request concerns travel to or within China. General international travel and unrelated visa-agent work are outside its trigger scope.

The agent selects one of four modes:

1. **Quick answer:** For example, “How do I buy a Beijing–Xi'an train ticket with a foreign passport?” Ask only for conditions that change the answer, then give steps and verification links.
2. **Pre-trip check:** Use travel dates, citizenship/passport, and destinations to produce entry, payment, connection, transport, accommodation, and reservation tasks.
3. **Full itinerary:** Establish city order, transport legs, and feasibility before filling in attractions, meals, and budget.
4. **In-trip troubleshooting:** Prioritize immediate action, fallback options, and official help channels. Do not regenerate a full travel guide when the visitor has an urgent issue.

## 4. Functional Requirements

**P0** means required for the complete first release; **P1** is an extension; **P2** is a later iteration. Each requirement must define its trigger, necessary inputs, output, and behavior when facts cannot be verified.

| ID | Priority | Requirement | Acceptance outcome |
| --- | --- | --- | --- |
| FR-01 | P0 | **Minimal intake.** Ask selectively for citizenship, passport/travel-document type, travel date, origin, arrival/departure port, destinations, and length of stay. For a full itinerary, also gather budget, interests, party composition, mobility, and dietary constraints. | Do not ask again for supplied information. Do not make an entry eligibility determination when a decisive condition is missing. |
| FR-02 | P0 | **Entry-route assessment.** Distinguish a visa, unilateral exemption, mutual exemption, transit exemption, and regional policies. Consult the responsible agency and relevant consular information. | Return a condition checklist with confirmed/unknown states, official links, and check date. Do not give a confident conclusion when sources conflict. |
| FR-03 | P0 | **Pre-trip readiness.** Check documents, arrival card, payment, connection/phone number, essential apps, lodging, and the first transport leg. | Produce a short time-ordered checklist with entry points and items to reconfirm before departure. |
| FR-04 | P0 | **Platform choice.** Compare official and third-party channels by task, noting language, identity, phone, payment, fee/service differences, and fallback. | Do not conflate international Trip.com with Chinese-language Ctrip. Do not describe a community 12306 integration as an official railway service. |
| FR-05 | P0 | **Rail booking and boarding.** Cover 12306 and Trip.com; check exact station names, passport-name entry, identity verification, seat type, boarding time, changes/refunds, and booking failures. | Provide usable steps. Timestamp live schedules, availability, and fees, or state that they were not checked live. |
| FR-06 | P0 | **Payment readiness and troubleshooting.** Cover Alipay, WeChat Pay, bank cards, cash, and viable alternatives. Branch on card binding, QR payment, limits, and merchant acceptance. | Never request a full card number or one-time code. Provide at least one fallback that does not rely on the failing channel. |
| FR-07 | P0 | **Airport/station transfer.** Compare metro/rail, taxis, ride-hailing, and prebooked transfer as appropriate; include the destination in Chinese and check terminal/station and last-service risks. | The visitor can show a Chinese address or sentence to staff. Do not confuse stations, airports, or terminals in the same city. |
| FR-08 | P0 | **Connection and navigation.** Compare roaming, local SIM/eSIM, and phone-number needs; cover Amap/Baidu Maps and offline address capture. | A traveler without a Chinese phone number or with no mobile data still has an actionable path. |
| FR-09 | P0 | **Lodging and registration.** Check passport name, address, arrival time, and contact channel before booking. Distinguish hotel registration from registration for stays outside hotels, using local official channels. | Do not imply all hotels or cities follow the same process. For check-in failure, provide a sequence for contacting the property, platform, and local authority. |
| FR-10 | P0 | **Attraction and museum reservations.** Prefer venue-owned channels. Check opening day, release time, accepted foreign documents, child rules, and on-site identity checks. | When a channel cannot accept a passport or no reservation is available, provide an official inquiry path or suitable alternative. |
| FR-11 | P0 | **Itinerary feasibility.** Calculate intercity travel, station-to-hotel transfers, opening days, holidays, dwell time, and rest together. | Each day has a realistic order of movements and activities; door-to-door travel is not represented by in-vehicle time alone. |
| FR-12 | P0 | **In-trip recovery and emergencies.** Cover missed trains, failed payment, no connection, lost passport, medical care, disrupted transport, and tourism complaints. | Start with immediate action. Verify emergency contacts for the current location; do not substitute channels intended for Chinese citizens traveling abroad. |
| FR-13 | P0 | **Evidence and uncertainty.** Attach sources and check dates to policies, prices, schedules, seat availability, opening hours, and platform capabilities. Separate facts, estimates, and advice. | When live checks are unavailable, say so explicitly; do not invent a fare, opening time, or available seat. |
| FR-14 | P0 | **Multilingual delivery.** Answer in the visitor's language. Include clear Chinese names, addresses, and short phrases for transport, allergies, and help requests. | Text can be copied or shown to local staff. Proper nouns are not given only in transliteration. |
| FR-15 | P1 | **Food and daily life.** Cover ordering, allergies, vegetarian/religious diets, drinking water, business hours, delivery, and review platforms. | Express dietary restrictions in unambiguous Chinese. Do not guarantee the absence of cross-contact. |
| FR-16 | P1 | **Families and accessibility.** Account for child fares, strollers, child seats, step-free routes, and pace for older travelers. | When a facility cannot be confirmed, identify exactly what to ask and provide another route. |
| FR-17 | P1 | **City modules.** Add Beijing, Shanghai, Guangzhou, Shenzhen, Chengdu, Xi'an, and other cities incrementally, covering transport, reservation, payment, and city-service entry points. | A city-specific rule applies only to that city. Expired sources trigger a fresh check. |
| FR-18 | P2 | **Reusable trip brief.** Retain user-confirmed citizenship, dates, order summaries, and preferences when the host supports it, without storing sensitive credentials. | Later requests reuse confirmed facts. Document numbers, payment credentials, and one-time codes are not retained. |

## 5. Platform Reference Requirements

The platform catalog is a set of **task-routed service cards**, not a generic “apps to download” list. Suggested fields: `name`, `category`, `official_url`, `operator`, `official_or_third_party`, `supported_tasks`, `language_options`, `identity_requirements`, `phone_requirements`, `payment_options`, `fee_notes`, `common_failures`, `fallbacks`, `source_urls`, `last_checked_at`, and `change_risk`. A field that cannot be checked should say “unknown”; the agent must not infer a value from an empty field.

| Task | Initial platforms | Difference the agent must explain |
| --- | --- | --- |
| Train travel | Railway 12306; Trip.com (international platform) | Official vs third-party channel, passport name/verification, service fees, change/refund channel, ticket status |
| Flights and lodging | Airline/property sites; Trip.com; Chinese-language Ctrip | Who fulfills the booking, document name, cancellation terms, customer-service language and contact route |
| Payment | Alipay; WeChat Pay; bank cards; cash | Check current foreign-card support; explain how to switch channels after a failure |
| Maps and local transport | Amap; Baidu Maps; DiDi; local public-transport channels | Chinese place names, location services, ride-hailing/payment prerequisites, city differences |
| Attractions and museums | Venue-owned reservation channels; third-party ticketing where needed | Passport support, time slots, on-site identity check, refund terms |
| Food and daily services | Meituan; Dianping; other relevant providers | Phone-number need, Chinese address, delivery vs in-person scope |

The **12306 / Trip.com procedure** deserves its own reference: select exact origin and destination stations → check train and availability → enter passenger details from the passport → confirm name/document/date/stations → pay and verify issuance → prepare for station checks → handle changes or refunds. A third-party status of “booking in progress” must never be treated as an issued ticket. Recheck current rules on the travel date. [S107](china-travel-skill-research/sources.md#s107) [S117](china-travel-skill-research/sources.md#s117) [S153](china-travel-skill-research/sources.md#s153)

## 6. Source Verification and Maintenance

1. **Source precedence.** Use immigration authorities and consulates for entry and accommodation law; railway and the actual ticket issuer for tickets; venue-owned channels for attractions; current local sources for weather and transport. Guides and community reports can surface problems but cannot independently settle a policy question.
2. **Recheck dynamic facts per request.** Entry policy, fares/availability, flight/train times, opening hours, holiday reservation rules, and payment-platform capabilities must be checked when relevant. Static reference files should store the lookup path, decision process, and known failure modes.
3. **Record evidence.** For material conclusions, keep URL, page title, publication/update date when available, check time, applicable place/citizenship, confidence, and conflicts.
4. **Handle conflicts.** If official sources disagree or an official page appears dated, state the conflict, mark the result as requiring human confirmation, and provide the responsible authority's inquiry channel.
5. **Handle bad entry points.** Stop using a page that redirects unexpectedly, returns 404, or asks for unofficial payment to complete an arrival card. Direct the visitor through the institution's homepage instead. [S031](china-travel-skill-research/sources.md#s031)

## 7. Agent Behavior and Output

### Minimum Workflow

```text
Identify the task and travel phase
  → extract known conditions; ask only for missing conditions that change the answer
  → load relevant references and official/platform entry points
  → check dynamic facts; record time and applicability
  → give a primary path, an independent fallback, and the next action
  → provide Chinese proper names or show-to-staff phrases when needed
```

### Output Shapes

- **Quick answer:** Current conclusion → 2–5 steps → decisive conditions → fallback → sources and check time.
- **Pre-trip check:** Ready / To arrange / Reconfirm, grouped into pre-departure and arrival-day tasks.
- **Full itinerary:** City order and transport skeleton → daily plan → booking priorities → budget estimate and basis → risks and alternatives.
- **In-trip troubleshooting:** Immediate action → fallback if that fails → Chinese phrase to show staff → official help channel.

For bookings, distinguish “a purchasable option was found,” “the user placed an order,” and “the provider issued or confirmed it.” A platform link must not imply that the agent has completed a transaction.

## 8. Cross-Agent Package Structure

Follow the Agent Skills `SKILL.md` entrypoint format [S166](china-travel-skill-research/sources.md#s166). Avoid depending on a tool name unique to one host. The agent should detect whether its environment supports web access, browser interaction, local files, or scripts. With limited capabilities, it should still offer a clear manual verification path.

```text
china-inbound-travel/
├── SKILL.md                       # Trigger, mode selection, core rules, reference routing
├── references/
│   ├── entry-and-documents.md     # Entry routes and official lookup points
│   ├── payments-and-connectivity.md
│   ├── rail-and-transport.md      # 12306, Trip.com, and local transport
│   ├── hotels-and-attractions.md
│   ├── emergency-and-language.md
│   ├── platform-catalog.md        # Service-card fields and entries
│   └── source-policy.md           # Precedence, freshness, and conflicts
└── scripts/                        # Add only if repeated validation warrants code
    └── validate-itinerary.*        # Optional: dates, transfers, and unknowns
```

Do not copy 100+ articles into `SKILL.md` or hardcode today's visa-exempt country list, fare, or platform support. Load city and platform references only for the relevant task. A CLI, MCP service, or browser integration is an optional capability adapter, not a prerequisite for using the Skill.

## 9. Release Plan

| Stage | Deliverable | Completion criterion |
| --- | --- | --- |
| M1: Validation slice | `SKILL.md`, entry/payment/rail/emergency references, platform catalog | Correctly handles first-visit preparation, passport-based rail booking, payment failure, and lost passport. This does not complete every P0 requirement. |
| M2: Complete first release | Add lodging, reservations, itinerary planning, city transfers, multilingual output, and the remaining P0 behavior | Produces a feasible multi-city itinerary; timestamps dynamic conclusions; passes all 10 acceptance cases below. |
| M3: Expansion and maintenance | P1 scenarios, city modules, source-checking checklist, service-card update rules, regression cases | New cities or policy changes can be added through references without changing the core workflow. |

## 10. Acceptance Cases

| Case | Example request | Expected behavior |
| --- | --- | --- |
| AC-01 | “I'm French. Can I visit Shanghai and Beijing visa-free next month?” | Confirm passport type, exact dates, and length of stay; check the applicable official rule; do not decide from citizenship alone. |
| AC-02 | “I'm flying Tokyo–Shanghai–Singapore. Can I use visa-free transit?” | Check onward destination, port, documents, duration, and permitted area; return a condition table with official evidence. |
| AC-03 | “How do I buy a Beijing–Xi'an train ticket on 12306 with a US passport?” | Explain station selection, name/document entry, verification, payment, issuance, and boarding; compare a Trip.com fallback. |
| AC-04 | “Trip.com says my train booking is in progress. Can I go to the station?” | Distinguish booking from issuance; guide the visitor to order status and support; do not claim that a ticket exists. |
| AC-05 | “My Alipay-linked card won't pay for the metro.” | Diagnose card binding, transaction restrictions, and acceptance; offer another payment or local transport path for immediate use. |
| AC-06 | “I have no Chinese phone number and arrive in Guangzhou tomorrow.” | Cover the minimum connection, payment, ride, property-contact, and offline-address preparations. |
| AC-07 | “Book the Palace Museum, National Museum, and Great Wall for me.” | Check date and document support, then use venue-owned channels and current rules; show order details before any submission. |
| AC-08 | “I lost my passport in Chengdu and have a train in two days.” | Prioritize reporting, embassy/consulate, immigration, and ticket-document steps; keep the emergency guidance focused. |
| AC-09 | “I'm taking a wheelchair and a child on the train to Shanghai.” | Include station accessibility, child fare, transfers, and time buffer; flag facilities that need confirmation. |
| AC-10 | Network unavailable or official page returns 404 | Do not fabricate a conclusion. Preserve known facts, label unknowns, and provide an institution/platform route for manual checking. |

## 11. Risks and Decisions for Implementation

- **Policy changes:** Static country lists, durations, and eligible areas can age quickly. Store the decision process and official entry points; recheck for the travel date.
- **Platform differences:** App language, foreign-card support, phone-number needs, and passport handling may vary by version and city. Service cards need a check date; a successful past use is not a universal guarantee.
- **Commercial incentives:** Third-party guides may favor their own booking products. Present meaningful official-vs-third-party differences without default promotional ranking.
- **Host capability:** Read-only research and instructions are the default first-release behavior. Agent-assisted form filling or an offline trip pack can be scoped later according to host tools and user direction.
- **Language support:** Start with English guidance plus Chinese names and show-to-staff phrases. Other visitor languages can use the host agent's translation ability, while critical legal and ticketing terms remain traceable to their source wording.

## 12. Deliverable Status

This phase delivers the requirements document and [source register](china-travel-skill-research/sources.md). It does **not** yet include the finished Skill. Implementation should begin with M1, test the 10 cases in Codex and Claude, then refine `SKILL.md` and its references from observed failures.

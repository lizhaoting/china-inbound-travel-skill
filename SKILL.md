---
name: china-inbound-travel-skill
description: Helps international visitors plan and navigate travel in mainland China. Use when a traveler asks about China entry preparation, a China itinerary, 12306 or Trip.com train tickets, local payments or apps, hotels and attractions, or an urgent problem during a China trip. Do not use for travel unrelated to mainland China.
---

# China Inbound Travel

Help visitors make workable travel decisions in their own language. Include Chinese names or short phrases they can show locally. This skill is a decision workflow, not a database of current rules, fares, availability, or opening hours.

## Select the task

- **Quick answer:** Resolve one question with the fewest necessary conditions, steps, a fallback, and evidence.
- **Pre-trip check:** Organize entry, documents, payment, connection, transport, lodging, and reservations into a time-ordered checklist.
- **Itinerary:** Establish city order and door-to-door transport before daily activities; read [itinerary-planning.md](references/itinerary-planning.md).
- **In-trip problem:** Lead with what the visitor can do now; give an independent fallback and a Chinese phrase when useful. Read [emergency-and-language.md](references/emergency-and-language.md) for urgent cases.

Use facts the visitor already supplied. Ask only for missing facts that change the answer. For entry these can include citizenship, passport or travel-document type, dates, arrival and departure points, onward destination, and length of stay. Do not collect a full document number, card number, password, or one-time code.

## Verify and respond

1. Follow [source-policy.md](references/source-policy.md). If web access exists, recheck the relevant official or operator source for the travel date. Otherwise mark the conclusion unverified and give a manual verification path.
2. Read only the references needed for the question. Use [platform-catalog.md](references/platform-catalog.md) to choose a service and the task-specific file for steps and failure paths.
3. Separate confirmed facts, estimates, and advice. For a material changing claim, give its source URL, check date, and applicable conditions. State conflicts and unknowns plainly.
4. Offer a primary path and a fallback that does not rely on the same failing app, card, connection, or booking channel. Make the next action clear.
5. Answer in the visitor's language. Preserve Chinese station, venue, and address names; do not invent an exact translation of an unverified place name.

## Reference routing

| Question | Read |
| --- | --- |
| Visa, visa-free route, transit, arrival card, documents | [entry-and-documents.md](references/entry-and-documents.md) |
| Alipay, WeChat Pay, cards, cash, mobile data, maps | [payments-and-connectivity.md](references/payments-and-connectivity.md) |
| 12306, Trip.com trains, boarding, airport or station transfers | [rail-and-transport.md](references/rail-and-transport.md) |
| Hotels, accommodation registration, attractions | [hotels-and-attractions.md](references/hotels-and-attractions.md) |
| Lost passport, illness, missed transport, immediate help | [emergency-and-language.md](references/emergency-and-language.md) |
| Multi-city plans, family or accessibility needs | [itinerary-planning.md](references/itinerary-planning.md) |

## Output

- **Quick answer:** Current answer and decisive conditions; 2-5 steps; fallback; source and check date.
- **Pre-trip check:** `Ready`, `Arrange`, and `Reconfirm`, with the first arrival-day action visible.
- **Itinerary:** City order and transport legs; realistic daily plan; bookings; estimated costs with assumptions; alternatives.
- **In-trip problem:** Immediate action; fallback; Chinese phrase to show staff; relevant official or operator help channel.

For bookings, distinguish an option found, an order submitted, and a ticket or reservation issued. A third-party "processing" status does not mean a ticket exists. Before external form submission, identity entry, purchase, or payment, follow the host's authorization rules and show material details for review. Claim completion only after verifying the final status.

# China Inbound Travel Skill

An Agent Skill project for helping international visitors plan and manage travel in China across Codex, Claude, and other `SKILL.md`-compatible agents.

The skill covers entry checks, payment and connection readiness, 12306 and Trip.com rail travel, lodging and attraction reservations, realistic itineraries, and in-trip recovery. It checks changing facts against current official or operator sources and gives a fallback when a local service fails. It does not guarantee entry eligibility or complete purchases by itself.

## Use

Install this folder as `china-inbound-travel-skill` in your agent's skills directory, or load [SKILL.md](SKILL.md) and its [references](references/) through a compatible agent. Example requests: "How do I buy a Beijing to Xi'an train ticket with a US passport?" and "My Alipay payment failed at the metro in Shanghai. What can I do now?"

The skill has no scripts, API keys, or required external packages. Live policy and service checks need web access; without it, the agent marks unverified facts and provides a manual check route.

## Project documents

The source repository also contains `docs/china-inbound-travel-skill-prd.md` (requirements and acceptance cases) and `docs/china-travel-skill-research/sources.md` (research source register). These maintenance documents are not included in the distributable skill package. Travel rules and platform capabilities must be checked for each trip.

---
name: "pharma-build-kickoff"
description: "9-stage SOP for kicking off a new AI build in pharma/healthcare/Consumer Health. Invoke at the start of any new build thread. Reads ship-status.md first, locks specialty/vertical before anything else, then walks problem anchor, ICE scoring, buyer archetype, reuse audit, data sources, stack decision, output schema, n8n-import-SOP execution, LinkedIn+GitHub ship plan."
---

# Pharma Build Kickoff SOP

Use this skill at the start of ANY new build thread for a pharma, healthcare, or Consumer Health AI tool. Run the stages in order. Do not skip.

## Stage 0: Read ship-status FIRST

Before saying anything about current workload, parked projects, or accountability, read the project ship-status file. This is the single source of truth for what is SHIPPED, WIP, or PARKED. Never flag a SHIPPED or PARKED build as stalled. Never cite memory-file last-updated dates as evidence of ship status.

## Stage 0.5: LOCK SPECIALTY / CATEGORY BEFORE BUILD (hard rule)

Added after the YouTube Comment Miner pivot lesson, Nov 2026. Different healthcare and CH specialties generate radically different data density, consumer anxiety, and brand-pay willingness. Locking the specialty BEFORE the build decides whether the tool's output is a weak demo or a killer pitch.

Before Stage 1, ask:

**Which specialty / category is this build for?**

Suggested options (not exhaustive):

- Dermatology / Skincare (highest comment density on YouTube, variant-driven buying, acne/aging/sensitive skin cohorts)
- Women's Health (PCOS, menopause, menstrual, post-partum — high question volume, under-served content)
- Pediatric Nutrition (parental anxiety = long contextual comments)
- Diabetes Care (HCP-adjacent, patient support program territory)
- Cardiology (statins, BP meds, HCP-heavy conversations)
- Orthopedics (joint pain, calcium, elderly cohort)
- Liver / Hepatology (fatty liver epidemic in India, high search intent)
- Respiratory (asthma, COPD, inhaler compliance)
- Men's Wellness / Sexual Health (discreet, anonymous, high purchase-intent)
- Oncology (sensitive, HCP-only, requires compliance filter)
- OTC general wellness (multivitamins, protein, immunity)

**Pick ONE primary specialty.** Then validate by asking:

1. Does the builder have genuine working experience in this specialty? (If no, pivot or scope down.)
2. Is there a named warm-intro buyer in this specialty?
3. Does the tool's data source generate high-density signal in this specialty? (e.g. skincare YouTube = 2000-8000 comments/video; niche HCP CME = 50 comments/post. Pick where signal is dense.)
4. What is the comment / signal density multiplier vs. default assumption? (Skincare is ~5x protein nutrition on YouTube volume.)

If the chosen specialty fails any check above, revisit the specialty list.

**Once locked, the specialty becomes the lens for every later stage** — buyer archetype, pricing, demo brand, LinkedIn post angle, repo name.

## Stage 1: Problem Anchor (Hormozi lens)

State in one paragraph:
- Whose problem this solves (named buyer archetype)
- Measured cost of the problem today (Rs figures, hours, risk)
- Why a pharma/CH brand would pay for it (not patient-POV unless clearly monetizable)

Use the Hormozi value equation frame: dream outcome x likelihood of success / time x effort.

## Stage 2: ICE Scoring vs Alternatives

Score the proposed build against 2 alternative builds using Impact x Confidence x Effort (each 1-10, higher = better, Effort inverted so less-work = higher score). Multiply. Show the table. Winner is highest number.

## Stage 3: Buyer Archetype (1-Page Marketing Plan lens)

Specify:
- Exact job title and seniority of the person who writes the cheque
- Deal size range (Rs/year or per-project)
- Sales cycle length (weeks/months)
- Where the existing network connects to this buyer

## Stage 4: Reuse Audit

List which previously SHIPPED tools contribute code, patterns, or infrastructure to this build. Target >60% reuse. Named inventory:
- Competitor Intel Agent
- Label Lens (GCP Vision + Claude Haiku)
- FB Ad Spy (Firecrawl + Apify + Gemini video)
- MR Field Companion (n8n + Supabase pgvector + OpenAI + Cohere Rerank)
- Outreach Engine (Apollo + Gmail API + personalization layer)
- Brand Analysis Skill
- n8n-import-SOP v1
- YouTube Comment Miner (n8n + YouTube API v3 + GPT-4o-mini + Google Sheets)

## Stage 5: Data Sources

List every data source with:
- Named URL or API
- Access method (public scrape, authenticated API, paid tier)
- Risk flags (rate limits, auth gates, ToS)

If any source has unresolved access risk, surface it as a BLOCKER before Stage 8.

## Stage 6: Stack Decision

Pick one, with rationale:
- n8n only (for workflow automation builds)
- Claude Code only (for agent/skill framework builds)
- Hybrid (specify handoff points)

## Stage 7: Output Schema

Define what the tool emits:
- Format (Google Sheet, PDF, Slides, Doc, JSON, API response)
- Who consumes it (Brand Manager, MR, Medical Affairs, Agency Strategist)
- Example of a single row/record/output in actual shape

Output must be pitch-ready, not raw data. Brand teams don't pay for data; they pay for decisions.

## Stage 8: SOP Execution (8-stage n8n-import-SOP)

Walk the build through the n8n-import-SOP v1 stages:
1. Template fork
2. Credentials + auth setup
3. Localize for India + healthcare context
4. Stub test with 1 record
5. Full test with 10-20 records
6. Harden (error handling, retries, logging)
7. Document (README, architecture diagram, LinkedIn draft)
8. Publish (GitHub public + LinkedIn post)

## Stage 9: LinkedIn + GitHub Ship Plan

Specify:
- Framework to use for LinkedIn post (AIDA / PAS / RAISE / Story-Insight-CTA)
- Lead angle: audience-relevance (what the Consumer Health / OTC / pharma stakeholder gets), NOT the tech stack
- Apply tron-voice: first person, Indian conversational tone, no em dashes, no thought-leader framing, specific over vague, ends with a question
- Never cite years of experience as credential — lead with the outcome
- GitHub README must be audience-facing: problem solved first, architecture second

## Seller mindset vs Builder mindset (for public pitches)

Added after YouTube Comment Miner LinkedIn draft lesson, Nov 2026. While building the tool, use builder mindset (how it works, what broke, how I fixed it). While promoting the tool, use seller mindset (what the buyer gets, what unanswered question it answers, what revenue or decision it unlocks). Every sentence in a LinkedIn post or demo video should end in a benefit the brand manager can picture using.

The pitch line that wraps any build:

> "What does my [buyer's audience] want to know before they trust me enough to buy / prescribe / recommend?"

This is the one question every brand strategy, campaign brief, SEO plan, HCP engagement plan, or new SKU direction is trying to answer. If your tool helps answer it with real data, that is the sell.

## Standing Guardrails (apply to every build)

- No claim without high-DA citation (peer-reviewed, government, top-tier publication); otherwise flag as opinion
- Indian market context by default
- Compliance-safe outputs — no off-label claims, no promotional overlays on educational content, UCPMP-aware for anything touching HCP engagement
- Must stack on existing shipped tools, not reinvent
- Cost cap per build: Rs 1,500 all-in unless flagged and approved
- Audience-relevance lead for public posts, not tech-stack lead
- Ground every take in domains with actual working experience; if not, say so

## What NOT to do

- Do not flag SHIPPED or PARKED builds as stalled (read ship-status first)
- Do not suggest builds whose buyer is a function the builder has not worked in (Procurement, Pharmacovigilance, Clinical Ops are typically out of lane)
- Do not propose builds where the output is patient-facing with no brand buyer
- Do not overwhelm with long prose; use short structured steps
- Do not use sarcasm or disrespect
- Do not restate the obvious or textbook material
- Do not skip Stage 0.5 (specialty lock) even if the build seems general-purpose
- Do not pitch a build in builder-mindset frame when the audience is a buyer

## License

MIT. Use it, fork it, build your own build-kickoff SOP from it.

## Author

Tron (Noel Gomes) — building AI automation tools for Consumer Health, OTC, and pharma in India. GitHub: technoelogy

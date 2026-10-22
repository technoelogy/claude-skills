# BRAND ANALYSIS SKILL
### For: Digital & Brand Strategist — India Market
### Version: 1.0 | Last Updated: March 2025

---

## SKILL OVERVIEW

This skill instructs Claude to conduct a **comprehensive, consulting-grade brand analysis** for any brand operating in India — spanning D2C Beauty & Personal Care, OTC/Consumer Healthcare, Rx/Ethical Pharma, and FMCG/Modern Trade categories.

**Output:** A detailed Word (.docx) consulting report — dense, referenced, comprehensive — following the structure below.

**Research method:** Fully automated. Claude uses web_search, web_fetch, and all available public intelligence sources. It flags clearly when data requires manual input (e.g., SEMrush export, Jungle Scout data, internal client materials).

**Geography:** India-first lens throughout. Global brand context flagged where directly relevant to India strategy.

---

## HOW TO TRIGGER THIS SKILL

The user will provide one of the following:
- A brand name + URL
- A brand name + category
- A client brief (may include competitor names, brand type, and campaign context)

**Example triggers:**
- *"Run a brand analysis on Cipla's Nicotex"*
- *"Analyse Himalaya Drug Company — OTC and personal care"*
- *"Do a full brand audit on Boat Lifestyle"*
- *"Client brief attached — do the full analysis"*

---

## STEP 0 — BRAND TYPE CONFIRMATION (MANDATORY FIRST STEP)

Before beginning ANY research, Claude must:

1. **Identify the likely brand type** from the name/URL/brief:
   - `D2C_BPC` — D2C Beauty & Personal Care (e.g. Pilgrim, Minimalist, mCaffeine)
   - `OTC_CH` — OTC / Consumer Healthcare (e.g. Vicks, Dettol, Nicotex, Dabur Chyawanprash)
   - `RX_PHARMA` — Rx / Ethical Pharma (e.g. brand is prescription-only, no direct consumer advertising)
   - `FMCG_MT` — FMCG / Modern Trade (e.g. HUL, P&G, Godrej brands)
   - `HYBRID` — Spans multiple types (e.g. Cipla which has Rx + OTC + wellness)

2. **Always ask the user to confirm** before proceeding:

```
I've identified this as a likely [BRAND_TYPE] brand. Before I begin the full analysis, please confirm:

1. Brand type: [detected type] — correct, or should I switch to a different mode?
2. For Rx brands: Is this a patient-facing digital brief, an HCP-facing brief, or both?
3. Competitors: I'll auto-identify [Comp A, Comp B, Comp C] from the category — or would you like to specify your own?
4. Any client brief, internal documents, or specific focus areas I should prioritise?
5. Agency pitch angle: Should the opportunity section focus on [SEO & Content / Social & Influencer / Science-backed Comms / Full-funnel Digital / Other]?
```

3. **Load the correct framework module** based on confirmed brand type (see Section: BRAND TYPE MODULES at the end of this skill).

---

## STEP 1 — RESEARCH EXECUTION PLAN

Once brand type is confirmed, Claude executes the following research sequence **before writing a single word of the report**. Each search should be specific, targeted, and logged mentally as a data source.

### 1A. Brand Website Intelligence
```
Search queries to run:
- "[brand name] official website"                          → Fetch homepage
- "[brand name] about us founding story"
- "[brand name] technology stack Shopify WooCommerce"
- "[brand name] mobile app iOS Android"
- "[brand name] WhatsApp Business chatbot"
- "[brand URL]" via web_fetch                              → Full homepage scrape
- "[brand URL]/blogs" or "/articles"                       → Content hub check
- site:[brand URL] (inferred from results)                 → Site structure
```

### 1B. Category & Market Context
```
- "[category] market size India 2024 2025"
- "[category] top brands India market share"
- "[category] growth trends India"
- "[brand name] market share India"
- "[brand name] revenue funding valuation 2024 2025"
```

### 1C. E-commerce & Marketplace Presence
```
- "[brand name] Amazon India best sellers reviews"
- "[brand name] Flipkart listing"
- "[brand name] Nykaa"
- "[brand name] Myntra"
- "[brand name] 1mg PharmEasy Netmeds"
- "[brand name] Blinkit Zepto Instamart"
- "[brand name] BigBasket"
- "[brand name] JioMart"
- "[brand name] best selling products SKUs [platform]"
```

### 1D. Social Media Presence
```
- "[brand name] Instagram followers"
- "[brand name] YouTube subscribers"
- "[brand name] Facebook page"
- "[brand name] LinkedIn"
- "[brand name] Twitter/X"
- "[brand name] influencer campaign 2024 2025"
- site:instagram.com "[brand name]"
```

### 1E. Advertising Intelligence
```
- "[brand name] Meta Facebook ads"                         → Note: Also check Meta Ad Library manually
- "[brand name] Google ads campaigns 2024"
- "[brand name] display advertising"
- "[brand name] Amazon sponsored ads"
- "[brand name] CTV OTT advertising Hotstar JioCinema"
- "[brand name] TVC television commercial 2024 2025"
- "[brand name] influencer marketing campaign"
- "[brand name] UGC user generated content campaign"
```

### 1F. SEO & Organic Traffic
```
- "[brand name] organic traffic SEO"
- "[brand name] keyword rankings"
- "[brand name] blog content strategy"
- "[brand name] backlinks domain authority"
→ FLAG: Request SEMrush export from user for deeper keyword data
```

### 1G. Reviews & Community Sentiment
```
- "[brand name] reddit reviews"
- "[brand name] quora answers"
- "[brand name] Amazon reviews negative"
- "[brand name] consumer complaints"
- "[brand name] trustpilot reviews"
- "[condition/therapy area] reddit India" (for OTC/Rx brands)
- "[brand name] App Store Google Play reviews"
```

### 1H. Competitor Research (run for EACH competitor)
```
- "[competitor] Amazon best sellers"
- "[competitor] Instagram followers"
- "[competitor] marketing strategy 2024"
- "[competitor] revenue funding"
- "[competitor] vs [brand name]"
```

### 1I. Regulatory & Compliance Check (OTC/Rx brands)
```
- "[brand name] ASCI complaint"
- "[brand name] CDSCO approval"
- "[brand name] advertising violation India"
- "[brand name] misleading claims"
```

### 1J. Emerging Digital Presence
```
- "[brand name] ChatGPT AI mentions"
- "[brand name] Custom GPT"
- "[brand name] WhatsApp Business API"
- "[brand name] GEO generative engine optimization"
- "[brand name] AI search visibility"
```

---

## STEP 2 — REPORT STRUCTURE

Generate a Word (.docx) report using the docx npm library following the full structure below. Apply the formatting standards specified at the end of this skill.

---

### SECTION 00 — COVER PAGE
- Brand name (large, brand color if identifiable)
- Report subtitle: "Comprehensive Brand & Digital Audit — [Month Year]"
- Brand type badge: D2C_BPC / OTC_CH / RX_PHARMA / FMCG_MT / HYBRID
- Geography: India Market
- Tagline: "Prepared for [Agency Name] Pitch" or "Internal Strategy Document"
- Benchmarked against: [Competitor 1] | [Competitor 2] | [Competitor 3]

---

### SECTION 01 — EXECUTIVE SUMMARY
**Target length:** 1 page

Cover in dense prose:
- Brand snapshot: founding year, founders, HQ, category, positioning
- Revenue / funding / valuation (latest available)
- One-line brand promise and core differentiation
- 5 things the brand is doing exceptionally well (bullet)
- 5 critical gaps or vulnerabilities (bullet)
- Overall digital maturity score: Rate 1–10 across: Website / SEO / Social / Commerce / Advertising / Reputation
- Strategic headline: One sentence that frames the core opportunity for your agency

---

### SECTION 02 — BRAND WEBSITE ANALYSIS

#### 2.1 Website Overview
- URL, platform/CMS (Shopify / WordPress / Custom / Magento — detect from page source clues)
- Site type: D2C store / informational / hybrid / HCP portal
- Primary CTAs: What actions is the site built to drive?
- Homepage above-the-fold messaging: Is it product-first, benefit-first, ingredient-first, story-first?
- Navigation architecture: How is content organised? Concern-based / product-based / ingredient-based?

#### 2.2 Mobile vs Desktop Experience
- Is the site mobile-optimised? (Check responsive design signals)
- Mobile CTA placement and thumb-zone accessibility
- Page load assessment (infer from tech stack and asset use)
- Mobile-specific features: sticky add-to-cart, mobile chat widget, app download prompt

#### 2.3 Tech Stack & Integrations
Identify and flag presence/absence of:
- E-commerce platform (Shopify / WooCommerce / custom)
- Payment gateway (Razorpay / PayU / Cashfree / Stripe)
- CRM / Marketing automation (Klaviyo / WebEngage / MoEngage / HubSpot)
- WhatsApp Business API integration (Interakt / Wati / Gupshup / Zoko)
- Chat widget (Tidio / Intercom / custom)
- Loyalty/referral program (Yotpo / Smile.io / custom)
- Custom GPT or AI assistant on site
- Review aggregation tool (Judge.me / Okendo / Stamped)
- Analytics (GA4 / Mixpanel / Hotjar / Clarity)

#### 2.4 WhatsApp Business & Conversational Commerce
- Is WhatsApp Business API active?
- Use case: Support only / Abandoned cart / Broadcast / Full commerce?
- Click-to-WhatsApp ads active?
- WhatsApp catalogue integration?
- **Benchmark:** What are category leaders doing with WhatsApp?
- **Gap/Opportunity:** What is missing?

#### 2.5 Custom GPT / AI Assistant
- Does the brand have an AI chatbot, Custom GPT, or AI-driven recommendation tool?
- If yes: What does it do? (Product finder / ingredient guide / symptom checker / support)
- **Benchmark vs. category**
- **Opportunity:** What AI-powered tool would add most value for this brand?

#### 2.6 Content Hub & SEO Content Strategy
- Does the brand have a blog / articles / knowledge hub?
- Publication frequency (estimated)
- Content types: ingredient guides / concern articles / how-to / news / clinical
- Is content SEO-optimised? (H1 structure, meta descriptions, internal linking)
- **Gap:** What content categories are missing relative to search demand?

#### 2.7 Website — What Is Working Well
Bulleted list with brief explanation for each point.

#### 2.8 Website — What Needs Improvement
Bulleted list with brief explanation and recommended fix for each gap.

#### 2.9 Competitive Website Benchmarking Table
| Parameter | [Brand] | [Comp 1] | [Comp 2] | [Comp 3] |
|---|---|---|---|---|
| Platform/CMS | | | | |
| Mobile Optimisation | | | | |
| WhatsApp Integration | | | | |
| Custom GPT / AI | | | | |
| Content Hub | | | | |
| Skin/Hair Quiz | | | | |
| Loyalty Program | | | | |
| International Shipping | | | | |
| Science/Clinical Section | | | | |

---

### SECTION 03 — MOBILE APP ANALYSIS
*(Skip this section with a note if brand has no app)*

#### 3.1 App Overview
- App name, platform (iOS / Android / both)
- App Store rating (iOS) + Google Play rating
- Total reviews count
- Last updated
- App size and performance signals

#### 3.2 App Functionality
- Core features: Browse / Buy / Track / Loyalty / Content / Community / Symptom checker / Prescription upload
- Onboarding flow (what does first-use look like?)
- Personalisation features
- Push notification strategy (inferred from reviews)
- In-app commerce vs. redirect to website

#### 3.3 App Reviews Analysis
- Top positive themes from reviews (summarise)
- Top negative/complaint themes (summarise)
- Any recurring UX/UI bugs mentioned?
- Competitor app comparison (rating, reviews, feature parity)

#### 3.4 App — Gaps & Opportunities

---

### SECTION 04 — BUSINESS LISTINGS & LOCAL PRESENCE

#### 4.1 Google My Business (GMB)
- Is GMB verified and active?
- Business category accuracy
- Photo quality and recency
- Review count and average rating on GMB
- Q&A section populated?
- Posts active?
- **Red flags:** Unverified listing / negative reviews unresponded / inconsistent NAP (Name, Address, Phone)

#### 4.2 Google Knowledge Panel
- Does the brand have a Knowledge Panel?
- Is it accurate? (Founding date, founders, social profiles, description)
- Are press articles indexed?
- **Opportunity:** What is missing from the Knowledge Panel?

#### 4.3 Other Business Listings
Check and report status for:
- Justdial
- IndiaMart (if B2B relevance)
- Sulekha
- Practo (for healthcare brands)
- Lybrate (for healthcare brands)
- LinkedIn Company Page
- Crunchbase / Tracxn (funding/investor visibility)
- Wikipedia (does a page exist?)

#### 4.4 NAP Consistency Audit
- Is Name / Address / Phone consistent across all major listings?
- Any duplicate or unverified listings?

---

### SECTION 05 — COMMERCE CHANNEL PRESENCE

Run this section for EACH applicable channel. Use the following sub-structure for each:

**Channels to cover (all applicable):**
- Amazon.in
- Flipkart
- Nykaa (BPC brands)
- Myntra (BPC/Fashion brands)
- 1mg (OTC/Healthcare/BPC)
- PharmEasy (OTC/Healthcare)
- Netmeds (OTC/Healthcare)
- Blinkit
- Zepto
- Swiggy Instamart
- BigBasket / BB Now
- JioMart
- Modern Trade: BigBazaar, DMart, Reliance Smart, Spencer's (infer offline presence from brand communications)
- Brand's own D2C website

#### Per-Channel Sub-Structure:
**5.X [Channel Name]**
- **Presence:** Active / Inactive / Not Listed
- **Top Selling SKUs:** List top 3–5 products visible on the platform (by reviews/BSR/visibility)
- **Ratings:** Average rating of top SKUs
- **Review Volume:** Reviews count on top SKUs
- **Listing Quality:** Title optimisation / bullet points / images / A+ content (for Amazon/Flipkart)
- **Brand Store:** Present / Absent / Quality assessment
- **Pricing:** In line with D2C / discounted / premium
- **Gaps:** What is missing?
- **Benchmark:** How do top competitors appear on this channel?

#### 5.Z Channel Presence Summary Table
| Channel | Present? | Top SKU | Rating | A+/Enhanced Content | Brand Store |
|---|---|---|---|---|---|
| Amazon.in | | | | | |
| Flipkart | | | | | |
| Nykaa | | | | | |
| 1mg | | | | | |
| PharmEasy | | | | | |
| Blinkit | | | | | |
| Zepto | | | | | |
| Instamart | | | | | |
| BigBasket | | | | | |
| D2C Site | | | | | |

---

### SECTION 06 — TOP SELLING SKUs BY PLATFORM

#### 6.1 Hero SKU Identification
For each platform where the brand is present, identify and list:
- Product name
- Price point
- Rating + review count
- Bestseller Rank (BSR) if visible on Amazon
- Key claims on listing
- Estimated sales velocity signals (number of reviews as proxy)

#### 6.2 SKU Performance Heatmap Table
| Product Name | D2C Site | Amazon | Flipkart | Nykaa | 1mg | Blinkit | Notes |
|---|---|---|---|---|---|---|---|
| [SKU 1] | ✓ | ✓ | ✓ | ✓ | – | – | Hero SKU |
| [SKU 2] | ✓ | ✓ | – | ✓ | ✓ | – | Healthcare crossover |
| [SKU 3] | ✓ | – | – | – | – | ✓ | QC-specific |

#### 6.3 SKU White Spaces
- Which SKUs are listed only on D2C and missing from key marketplaces?
- Which competitor SKUs dominate a category where the brand has a product but weak presence?
- Pricing inconsistency flags across channels

---

### SECTION 07 — SOCIAL MEDIA PRESENCE

#### 7.1 Platform-by-Platform Overview Table
| Platform | Handle | Followers/Subscribers | Post Frequency | Avg Engagement | Content Type | Last Active |
|---|---|---|---|---|---|---|
| Instagram | | | | | | |
| YouTube | | | | | | |
| Facebook | | | | | | |
| Twitter/X | | | | | | |
| LinkedIn | | | | | | |
| Pinterest | | | | | | |
| ShareChat/Moj | | | | | | |

#### 7.2 Instagram Deep Dive
- Follower count and growth trajectory (if data available)
- Content pillars: What recurring content types are used?
- Reels vs. Static vs. Carousel: What is the mix?
- Engagement rate: Estimated (likes+comments / followers)
- Use of Instagram Shopping / product tags
- Stories and Highlights strategy
- Branded hashtag: Active? Volume?
- Celebrity / ambassador content integration
- **What is working well**
- **What needs improvement**

#### 7.3 YouTube Analysis
- Subscriber count
- Upload frequency
- Top performing video types (TVC / how-to / ingredient / unboxing / testimonial)
- Average views per video
- Comment sentiment (positive / mixed / negative)
- SEO on YouTube: Titles, descriptions, thumbnails optimised?
- **Gap:** What content categories are missing?

#### 7.4 Influencer Ecosystem Analysis

**Tier Breakdown:**
| Tier | Definition | Brand's Current Use | Quality Assessment |
|---|---|---|---|
| Mega (>1M followers) | Celebrity ambassadors | | |
| Macro (100K–1M) | Category creators | | |
| Micro (10K–100K) | Niche/community creators | | |
| Nano (<10K) | Everyday advocates / affiliates | | |

- **Influencer content quality:** Is it scripted/forced or organic?
- **Category of influencers used:** Beauty / Health / Lifestyle / Medical / Fitness / Parent / Regional
- **Regional language influencers:** Present or absent? (Hindi, Tamil, Telugu, Kannada, Bengali)
- **Science/expert influencers:** Dermatologists, trichologists, nutritionists, doctors — used or not?
- **UGC (User Generated Content):**
  - Is there an active UGC program?
  - Is UGC being repurposed on brand channels?
  - Volume of organic UGC visible
  - UGC quality: Before/after results / unboxings / routine videos
- **Benchmark:** How does the influencer ecosystem compare to top 2 competitors?

#### 7.5 Social Media — What Is Working
#### 7.6 Social Media — What Needs Improvement
#### 7.7 Competitive Social Benchmarking Table

---

### SECTION 08 — ADVERTISING AUDIT

#### 8.1 Meta (Facebook + Instagram) Advertising
- **Meta Ad Library check:** Are ads running? (Note: User should manually verify at https://www.facebook.com/ads/library)
- Ad formats in use: Single image / Carousel / Reels / Stories / Collection
- Campaign objectives inferred: Awareness / Traffic / Conversions / App installs / Lead gen
- Click-to-WhatsApp ads: Active?
- Retargeting signals: Dynamic product ads visible?
- Creative quality: Production level, messaging clarity, CTA strength
- Frequency of new creative: Static library or active testing?
- **Gaps:** What ad formats or objectives appear absent?

#### 8.2 Google Advertising
- Search ads: Brand keywords covered? Category keywords?
- Display Network: Banner ads visible on content sites?
- YouTube ads: Pre-roll / bumper / in-feed?
- Performance Max campaigns: Signals of PMax use
- Shopping ads: Google Shopping listings active?
- **Benchmark:** Are competitors outbidding on branded terms?

#### 8.3 Amazon Sponsored Advertising
- Sponsored Products: Hero SKUs appearing in sponsored positions?
- Sponsored Brands: Brand headline ads with logo visible?
- Sponsored Display: Retargeting ads on and off Amazon?
- Stores + Posts: Amazon Posts active?
- **Benchmark:** Competitor sponsored share of shelf for key category keywords

#### 8.4 Display Advertising
- Programmatic display presence (inferred from SimilarWeb / web observation)
- Publisher categories targeted (health sites / lifestyle / news)
- Creative format: Standard IAB / rich media / native

#### 8.5 CTV / OTT Advertising
- Hotstar / JioCinema / SonyLIV / Zee5 / MX Player presence
- Connected TV ad formats: Pre-roll / mid-roll / pause ads
- Any branded content / show sponsorships on OTT?
- Regional OTT presence (Sun NXT, Aha, etc.)

#### 8.6 GEO — Generative Engine Optimisation
*(New and critical parameter for 2025+)*
- Does the brand appear when searched in ChatGPT, Perplexity, or Google AI Overviews?
- Test queries: "[brand name] reviews", "best [category] brand India", "what is [key product]"
- Brand visibility in AI-generated answers
- Is the brand's website structured for AI citation? (Structured data, FAQ schema, authoritative content)
- **Opportunity:** How to set up the brand to be recommended by AI search engines

#### 8.7 Setting Up Brand in ChatGPT / AI Ad Ecosystem
- Is the brand running ads in ChatGPT (if applicable — Meta/OpenAI partnerships)?
- Is brand content structured for LLM training citation?
- Does the brand have an AI brand kit / structured data for AI assistant recognition?
- **Recommendation:** Steps to improve AI discoverability and citation

#### 8.8 Advertising Spend Breakdown Table (Estimated)
*(Based on public signals, Meta Ad Library activity, SimilarWeb referral data, and search impression share)*
| Channel | Estimated Activity Level | Creative Volume | Audience Targeting Signal | vs. Competitor |
|---|---|---|---|---|
| Meta (FB+IG) | High / Medium / Low | | | |
| Google Search | | | | |
| Google Display | | | | |
| YouTube | | | | |
| Amazon Ads | | | | |
| CTV/OTT | | | | |
| Programmatic | | | | |

*Note: Exact spend data requires SEMrush Advertising Research export or Facebook Ad Library. Flag for manual input.*

---

### SECTION 09 — SEO & ORGANIC DIGITAL PRESENCE

#### 9.1 Domain Authority & Traffic Signals
- Domain age
- Estimated monthly organic traffic (SimilarWeb / Ahrefs public data — flag if SEMrush export needed)
- Top traffic sources: Organic / Direct / Social / Referral / Paid
- Top organic landing pages (inferred from site structure + search)
- **Flag:** Request SEMrush organic keyword report for precise data

#### 9.2 Keyword Positioning
- Branded keyword strength: Does the brand rank #1 for its own name?
- Category keyword visibility: Top 3 category terms — does brand appear page 1?
- Informational keyword gaps: High-volume queries the brand should own but doesn't
- Long-tail opportunity: 3–5 high-intent long-tail queries the brand could realistically capture

#### 9.3 Content Audit
- Total estimated indexed pages
- Blog/content hub: active / inactive / absent
- Content quality: Surface-level / ingredient-depth / clinical-depth
- Schema markup: Product schema / FAQ schema / Review schema / Article schema — present or absent?
- Core Web Vitals signals (inferred)

#### 9.4 Backlink Profile
- Estimated domain authority
- Key backlink sources: Press / blogs / industry directories / government / .edu
- PR-driven backlinks vs. organic editorial links
- **Competitor comparison:** Is competitor DA significantly higher?

#### 9.5 Local SEO (for brands with retail / clinic presence)
- Google Maps visibility for retail touchpoints
- Location pages on website?

---

### SECTION 10 — REVIEWS & REPUTATION AUDIT

#### 10.1 Platform-by-Platform Review Summary
| Platform | Avg Rating | Review Count | Top Positive Theme | Top Negative Theme |
|---|---|---|---|---|
| Amazon.in | | | | |
| Flipkart | | | | |
| Nykaa | | | | |
| 1mg / PharmEasy | | | | |
| Google / GMB | | | | |
| App Store (iOS) | | | | |
| Google Play | | | | |
| Trustpilot / Others | | | | |

#### 10.2 Reddit / Quora / Yahoo Answers — 3 Community Conversations

For each of 3 conversations found:
- **Platform:** Reddit / Quora / Yahoo
- **Thread title / question**
- **URL** (if findable)
- **Date**
- **Gist of conversation:** What are people saying about the brand OR the condition/therapy area?
- **Sentiment:** Positive / Mixed / Negative / Curious
- **Key insight for brand strategy:** What does this tell us?

*(For OTC/Rx brands: prioritise threads about the condition/therapy area, not just the brand name)*

#### 10.3 Reputation Risk Flags
- Any major public complaints or controversies?
- ASCI complaints filed against the brand? (Search: "[brand] ASCI complaint")
- Misleading advertising allegations?
- Product quality or safety concerns in public domain?
- Delivery / logistics complaint patterns (for D2C)

#### 10.4 Reputation Score & Recommendation
Overall reputation health: Strong / Moderate / At Risk
Key actions recommended

---

### SECTION 11 — REGULATORY & COMPLIANCE AUDIT
*(Depth varies by brand type — most critical for OTC_CH and RX_PHARMA)*

#### 11.1 Advertising Compliance (ASCI)
- Any known ASCI complaints or upheld violations?
- Are claims on website/ads ASCI-compliant?
- Common risk areas: Superlative claims ("best", "fastest"), comparative claims, before/after imagery, clinical claim substantiation
- **Flag high-risk claims** found on current website/ads

#### 11.2 CDSCO / Drug Regulatory Compliance
*(For OTC and Rx brands)*
- Is the product CDSCO-approved / Schedule H / Schedule H1 / OTC Schedule K?
- Are mandatory labelling requirements met on digital platforms?
- Any listed recalls or safety alerts?

#### 11.3 FDA / Import Compliance
*(For brands claiming imported ingredients or globally manufactured products)*
- Are import claims accurate and verifiable?
- FDA (US) approval claimed? Verify accuracy.

#### 11.4 Digital Advertising Compliance
- Are prescription drug brands advertising direct-to-consumer in violation of guidelines?
- WhatsApp broadcast compliance (TRAI DLT registration)
- Privacy policy and cookie consent adequacy (IT Rules 2021)
- Influencer disclosure compliance (ASCI influencer guidelines — "#ad" / "#sponsored")

---

### SECTION 12 — COMPETITION ANALYSIS

*Run the full sub-analysis below for each of 3 competitors (auto-identified or client-specified).*

#### 12.X — [Competitor Name]

**12.X.1 Competitor Snapshot**
- Brand overview, founding, revenue/funding
- Core positioning and differentiation
- Target audience

**12.X.2 Website & Tech**
- URL, platform, key CTAs
- Content hub quality
- WhatsApp / AI tools

**12.X.3 Commerce Presence**
- Top platforms, hero SKUs, ratings

**12.X.4 Social & Influencer**
- Follower counts, content strategy, ambassador

**12.X.5 Advertising**
- Key channels, campaign themes, creative approach

**12.X.6 SEO Strength**
- Estimated traffic, key ranking terms

**12.X.7 What They Do Better Than [Brand]**
**12.X.8 What [Brand] Does Better Than Them**

#### 12.Z — Master Competitive Matrix

Build a comprehensive comparison table covering all key parameters:
| Parameter | [Brand] | [Comp 1] | [Comp 2] | [Comp 3] |
|---|---|---|---|---|
| Revenue (est.) | | | | |
| Website Platform | | | | |
| Content Hub | | | | |
| WhatsApp Commerce | | | | |
| Custom GPT/AI | | | | |
| Instagram Followers | | | | |
| YouTube Subscribers | | | | |
| Influencer Strategy | | | | |
| Amazon Rating (top SKU) | | | | |
| Amazon Reviews (top SKU) | | | | |
| A+ Content Quality | | | | |
| Quick Commerce | | | | |
| ePharmacy Presence | | | | |
| Meta Ad Activity | | | | |
| Google Ad Activity | | | | |
| Amazon Ads | | | | |
| CTV/OTT Ads | | | | |
| GEO / AI Visibility | | | | |
| ASCI Compliance | | | | |
| Overall Digital Maturity | /10 | /10 | /10 | /10 |

---

### SECTION 13 — BRAND POSITIONING IN CATEGORY CONTEXT

#### 13.1 Category Map
- Draw a verbal 2x2 positioning map:
  - Axis 1: Science-led ↔ Natural/Lifestyle-led
  - Axis 2: Mass/Affordable ↔ Premium
  - Place brand and all competitors on this map
  - *(For OTC/Rx: Efficacy-led ↔ Wellness-led; Prescription ↔ OTC)*

#### 13.2 Share of Voice (Estimated)
- Estimated share of digital conversation: Brand vs. competitors
- Dominant platforms where competitors are louder

#### 13.3 Consumer Perception Gap
- What does the brand *want* to be known for?
- What is the consumer *actually* saying? (from reviews + community data)
- The gap between intended and perceived positioning

#### 13.4 White Space Opportunities in the Category
- Underserved consumer need states
- Ingredient or formulation claims not yet owned
- Platform or channel gaps vs. the category
- Audience segments underserved (Regional / Tier 2-3 / Male / Senior / Teen)

---

### SECTION 14 — WHAT IS WORKING & WHAT HAS ROOM FOR IMPROVEMENT

#### 14.1 Master What's Working / What Needs Work Table
| Area | Green — Doing Well | Red — Needs Improvement |
|---|---|---|
| Website UX & Tech | | |
| Mobile Experience | | |
| WhatsApp Commerce | | |
| Custom GPT / AI | | |
| Content & SEO | | |
| GEO / AI Visibility | | |
| Social Media | | |
| Influencer Ecosystem | | |
| UGC Program | | |
| Amazon Presence | | |
| Flipkart Presence | | |
| Nykaa/Myntra | | |
| ePharmacy | | |
| Quick Commerce | | |
| Modern Trade Signals | | |
| Meta Advertising | | |
| Google Advertising | | |
| Amazon Ads | | |
| CTV/OTT | | |
| Display/Programmatic | | |
| Reviews & Reputation | | |
| Regulatory Compliance | | |
| Competitive Standing | | |

---

### SECTION 15 — NEED GAPS & AGENCY PITCH OPPORTUNITIES

*Frame every gap as a revenue-generating or brand-equity-building opportunity your agency can solve.*

#### 15.1 Priority Opportunity Stack
Rank opportunities by:
- **Impact** (High/Medium/Low)
- **Effort** (High/Medium/Low)
- **Timeline** (Quick win <30 days / Medium 30–90 days / Long-term 90+ days)

Present as a table:
| # | Opportunity | Why It Matters | Impact | Effort | Timeline | Your Agency's Role |
|---|---|---|---|---|---|---|
| 1 | | | | | | |
| 2 | | | | | | |
| ... | | | | | | |

#### 15.2 Detailed Opportunity Write-ups
For each of the top 5 opportunities, write a full paragraph covering:
- The specific gap observed
- Competitive context (who is doing this better)
- What the brand is losing by not addressing it
- Recommended intervention
- Expected outcome

#### 15.3 Agency Pitch Closing Statement
End with 2–3 punchy paragraphs that:
- Summarise the brand's position in 1 sentence
- State the single biggest opportunity in 1 sentence
- Position your agency as the right partner to capture it

---

### SECTION 16 — APPENDIX

#### 16.1 Data Sources & Research Log
List all URLs fetched, searches conducted, and data sources used during the analysis. Flag which data points were estimated vs. confirmed.

#### 16.2 Manual Data Inputs Required
List everything Claude could not find automatically that would strengthen the report:
- SEMrush organic keyword export
- Jungle Scout Amazon sales rank data
- Meta Ad Library manual screenshot
- Internal client revenue / sell-out data
- App analytics (installs, DAU, retention)
- CRM / email database size
- Offline retail distribution data

#### 16.3 Glossary
Define key terms used in the report (GEO, A+ Content, BSR, QC, ePharmacy, ASCI, CDSCO, etc.) for client-facing use.

---

## BRAND TYPE MODULES

These modules modify the standard framework for specific brand types. Load on top of the base structure.

---

### MODULE: OTC_CH (OTC / Consumer Healthcare)

**Additional parameters to include:**
- Pharmacy distribution: presence in chemist chains (Apollo Pharmacy, MedPlus, Wellness Forever)
- Chemist recommendation programs: Is brand running chemist loyalty/incentive programs?
- Doctor recommendation: Any endorsement from medical associations?
- Regulatory: CDSCO drug classification, Schedule status
- Seasonal marketing: Does brand capitalise on seasonal demand (flu season, allergy season, summer)?
- Category entry point: Is brand the market creator or challenger?
- OTC vs. Prescription switching: Is this an Rx-to-OTC switch product?
- Health claim substantiation: Are efficacy claims on digital platforms backed by visible clinical data?
- AYUSH / Allopathic / Homeopathic: Which regulatory framework?

**Modified Social lens:** Look for condition community conversations, not just brand conversations.
**Modified Review lens:** Include pharmacy app reviews, health forum discussions.

---

### MODULE: RX_PHARMA (Rx / Ethical Pharma)

**Confirm with user before proceeding:** Patient-facing OR HCP-facing OR both?

**If Patient-Facing Digital:**
- Disease awareness websites: Does brand run a condition-specific awareness site?
- Patient community presence: Reddit, Facebook groups, condition-specific forums
- Patient support programs: Adherence apps, helplines, reimbursement assistance
- OTT/CTV presence for disease awareness (condition, not brand)
- Social media for unbranded disease education content
- SEO for condition/symptom keywords (not brand keywords)
- Pharma-compliant content: Fair balance, ISI summary, no promotional claims

**If HCP-Facing Digital:**
- HCP portal: Does brand have a doctor-facing website / CME portal?
- Medscape / Doceree / Medwiki ad presence
- eDetailing: Any digital MR tools or iPad detailing apps?
- KOL (Key Opinion Leader) digital engagement
- Medical conference / congress digital presence
- PubMed / clinical data visibility: Is brand's clinical data indexed?
- Doctor app presence: Practo, Lybrate, DoctorInsta listings or ads

**Regulatory compliance is MANDATORY in this module:**
- No direct-to-consumer promotional advertising for Rx drugs
- Medical disclaimer presence
- Fair balance in all communications
- UCPMP (Uniform Code of Pharmaceutical Marketing Practices) compliance

---

### MODULE: FMCG_MT (FMCG / Modern Trade)

**Additional parameters:**
- Modern Trade visibility: DMart, Reliance Smart, BigBazaar shelf presence signals
- General Trade distribution signals
- Kirana / neighbourhood store presence (inferred from distribution claims)
- Point-of-sale (POS) digital integration
- Trade marketing: Any visible retail activation, gondola end caps, in-store digital
- Private label threat: Is brand under pressure from retailer private labels?
- Rural distribution signals
- Sachet / small-unit format for mass market
- Regional brand strength: Does the brand have stronger presence in specific states?

---

### MODULE: HYBRID (Multiple Brand Types)

- Run all applicable modules
- Clearly segment findings by brand line / category
- Note where the brand's digital presence creates confusion between Rx and OTC lines

---

## FORMATTING STANDARDS FOR WORD REPORT

Use the following when generating the .docx file:

```javascript
// Colors
BRAND_PRIMARY: Detect from brand website if possible, else use: "1A3C5E" (professional navy)
SECTION_HEADER: Same as BRAND_PRIMARY
ACCENT_BG: "EBF5FB" (light blue — for callout boxes)
GOOD_BG: "E9F7EF" (light green — for what's working)
GAP_BG: "FDEDEC" (light red — for gaps)
OPPORTUNITY_BG: "FEF9E7" (light yellow — for opportunities)
TABLE_HEADER: BRAND_PRIMARY with white text

// Typography
H1 (Section): 32pt, Bold, BRAND_PRIMARY, bottom border
H2 (Sub-section): 26pt, Bold, BRAND_PRIMARY
H3 (Sub-sub-section): 22pt, Bold, Dark
Body text: 21pt, Arial
Table body: 19pt, Arial
Footer note: 17pt, Gray

// Layout
Page: US Letter (12240 x 15840 DXA), 1-inch margins
Header: Brand name + "Brand Audit [Month Year]" | top border in brand color
Footer: "Confidential — Prepared for [Agency] Pitch | Page N"

// Tables
Always use DXA widths that sum to 9360
Always include column headers in brand color with white text
Alternate row shading optional but consistent
Cell padding: top/bottom 80, left/right 120

// Callout Boxes
Use colorBox() pattern (single-column table) for:
- Agency opportunity summaries (OPPORTUNITY_BG)
- Key findings (ACCENT_BG)
- What's working (GOOD_BG)
- Critical gaps (GAP_BG)

// Numbering
All bullet lists: LevelFormat.BULLET with proper indent
No unicode bullet characters
```

---

## QUALITY CHECKS BEFORE DELIVERING REPORT

Before presenting the final .docx, Claude must verify:

- [ ] Brand type confirmed with user before research began
- [ ] All 16 sections present (with justified exceptions noted)
- [ ] At least 3 competitors analysed
- [ ] Minimum 3 Reddit/Quora/community conversations found and summarised
- [ ] All India-specific channels checked: Amazon, Flipkart, Nykaa, 1mg, PharmEasy, Blinkit, Zepto, Instamart, BigBasket
- [ ] Advertising audit covers: Meta, Google, Amazon Ads, Display, CTV/OTT, GEO
- [ ] WhatsApp Business and Custom GPT both assessed
- [ ] UGC program assessed
- [ ] ASCI/regulatory flags included for OTC and Rx brands
- [ ] Agency opportunity section ends with a pitch-worthy closing statement
- [ ] Appendix lists all data sources + manual data inputs required
- [ ] Docx validated (no broken XML, all tables have correct DXA widths)
- [ ] File saved to /mnt/user-data/outputs/[BrandName]_Brand_Audit_[Month][Year].docx

---

## IMPORTANT OPERATING NOTES

1. **Never start writing the report before completing the research phase.** Run all applicable searches in Step 1 first, then synthesise into the report.

2. **When data is unavailable:** Write "Data not publicly available — recommend [specific manual action]" rather than guessing or leaving blank.

3. **Competitor auto-identification:** Use category + geography signals. For a haircare brand, identify top 3 Indian haircare D2C brands by revenue/market share. State your selections and rationale, and allow user to override.

4. **SEMrush data:** Always flag "For precise keyword and traffic data, please provide a SEMrush organic research export for [brand URL]." Do not fabricate traffic numbers.

5. **Jungle Scout data:** Flag "For Amazon sales rank and estimated revenue data by SKU, please provide a Jungle Scout export." Use review count and BSR rank as proxy signals where Jungle Scout data is absent.

6. **Meta Ad Library:** Claude cannot directly access the Ad Library tool. Always instruct: "Verify active ads at: https://www.facebook.com/ads/library/?q=[brand+name]&country=IN". Infer activity from page signals and search results.

7. **Tone:** The report is written in third person, consulting style. Dense, confident, referenced. No filler. Every sentence should be actionable or analytical.

8. **Length:** Do not truncate. This is a comprehensive report. A thorough analysis will typically produce a 30–50 page Word document. Use the iterative file-building approach for long documents.

9. **GEO Testing:** Where possible, Claude should actually test the brand's AI visibility by formulating the query as if a user would ask ChatGPT or Perplexity about it, and note whether the brand appears in the response.

10. **Regulatory caution:** Never make definitive legal or regulatory compliance judgements. Always write "appears to be compliant" or "may present compliance risk — recommend legal review."

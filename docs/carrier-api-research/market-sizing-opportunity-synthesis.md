# Market Opportunity Synthesis: Carrier API Integration SaaS Platform

**Date:** 2026-04-06
**Type:** Market Research / Final Assessment
**Status:** Complete
**Recommendation:** Conditional GO

---

## 1. Executive Summary

- **A meaningful market opportunity exists** for a developer-first carrier API integration platform, but it is narrower and more nuanced than the original hypothesis assumed. The addressable market for an ocean-only, usage-based API product is approximately $200-400M annually, growing at 16-22% CAGR. This is not a venture-scale opportunity on its own, but it is a viable bootstrapped or lightly-funded business with clear product-market fit in one specific segment.

- **The beachhead customer is the logistics tech developer, not the freight forwarder.** Customer discovery research unambiguously shows that the primary buyer of a developer-friendly carrier API is a software company building logistics products -- digital forwarders, TMS builders, freight marketplaces, visibility tool startups. Traditional freight forwarders (including SSL) need a finished product (dashboard, alerts), not an API. The API platform serves forwarders indirectly, through the tech companies that build for them.

- **The unit economics are strong.** Variable cost per container tracked is $0.08-$0.15/month. At a $1.50/container price point, gross margins reach 88-92%. Carrier API access is currently free across all major carriers. Break-even on a lean 2-person team requires approximately 33,000 containers/month -- roughly 70-130 mid-market customers.

- **DCSA standardization is a structural tailwind.** Nine carriers covering ~75% of global container trade are adopting standardized APIs. This reduces integration build cost by roughly 60% compared to five years ago and creates a window where new entrants can achieve carrier coverage at a fraction of the historical cost.

- **The WiseTech/E2open consolidation creates a time-limited switching window.** WiseTech's $2.1B acquisition of E2open (INTTRA) and CargoWise's pricing restructure (25-35% cost increases) are pushing forwarders and their tech partners to re-evaluate carrier data providers. This window is open now but will close as integration settles.

- **The open-source SDK strategy is the key differentiator.** No open-source SDK for ocean carrier API integration exists in any language. An open-source TypeScript SDK combined with a managed SaaS platform creates a distribution funnel no competitor has. This is the most defensible element of the strategy.

- **The recommendation is GO, conditioned on a lean startup approach** -- 2-3 engineers, open-source SDK first, managed platform second, targeting logistics tech developers. This is not a "raise $20M and go big" opportunity. It is a "build something excellent with a small team and grow organically" opportunity, with optionality to expand into multimodal tracking, booking, and intelligence features over time.

---

## 2. Market Sizing

### TAM: Total Addressable Market

The total global spend on carrier API integration, tracking aggregation, and supply chain visibility services is approximately **$1.0-1.5B in 2025**, growing to **$4.2-6.6B by 2034-2036**.

| Data Point | Value | Source |
|---|---|---|
| End-to-end multimodal visibility platform market (2025) | ~$1.0B | FMI / Competitive landscape research |
| Same market projected (2036) | ~$4.2B (13.7% CAGR) | FMI |
| Container tracking API market (2024) | $964M | Market.us / Pricing research |
| Same market projected (2034) | $6.6B (21.3% CAGR) | Market.us |
| Freight forwarding software market (2025) | $14.3B | Mordor Intelligence |
| Same market projected (2030) | $22.2B | Mordor Intelligence |
| Digital freight forwarding market, US (2026) | $9.8B (19% CAGR) | Mordor Intelligence |
| Companies currently using container tracking APIs | ~4,500 | Market.us |

The TAM includes all modalities (truck, rail, air, ocean, parcel) and all buyer segments (enterprise, mid-market, small). Ocean freight visibility is a subset, estimated at 30-40% of the total visibility market based on modal split data.

**Estimated ocean-specific TAM: $300M-$600M (2025), growing to $1.3-2.6B by 2034.**

### SAM: Serviceable Addressable Market

The SAM excludes: (a) large enterprises that will only buy through enterprise sales processes with 6-12 month cycles (project44, FourKites territory), (b) pure portal/dashboard users with no API consumption capability, and (c) non-ocean modalities.

The SAM is the market for **developer-friendly, self-serve, usage-based ocean carrier API platforms** -- the segment occupied today by Vizion ($4-5/container), Terminal49 ($3-10/container), and budget players (Shipsgo, JSONCargo, TRADLINX).

| Segment | Estimated Companies | Avg. Monthly Spend | Annual Segment Value |
|---|---|---|---|
| Logistics tech startups (API consumers) | 300-500 | $500-$5,000 | $36-60M |
| Mid-market forwarders with IT teams | 500-2,000 | $1,000-$10,000 | $60-120M |
| TMS/freight software vendors (embed) | 50-100 | $5,000-$50,000 | $30-60M |
| Small forwarders (portal + API) | 2,000-5,000 | $100-$500 | $24-60M |

**Estimated SAM: $150-300M annually.**

### SOM: Serviceable Obtainable Market

Realistically capturable in years 1-3, given:
- 6-month build phase before any revenue
- 12 initial carrier adapters (covering ~75% of global container capacity)
- Developer-first GTM with no enterprise sales team
- Competition from Vizion (funded, established), Terminal49 (funded, good DX), and expanding budget players

| Year | Customers | Containers/Month | Price Point | Annual Revenue |
|---|---|---|---|---|
| Year 1 | 50-200 | 10,000-50,000 | $1.50 avg | $180K-$900K |
| Year 2 | 200-500 | 50,000-150,000 | $1.25 avg | $750K-$2.25M |
| Year 3 | 500-1,000 | 150,000-400,000 | $1.00 avg | $1.8M-$4.8M |

**Year 3 SOM: $2-5M ARR.** This assumes the moderate growth scenario from the pricing research. The aggressive scenario (reaching $2.5M ARR by end of Year 2) requires product-market fit in the logistics tech developer segment and effective developer marketing, both achievable but not guaranteed.

---

## 3. Hypothesis Validation

### a) "Accessible, usage-based billing" -- Is there demand?

**Verdict: Strongly supported.**

The research documents a clear pricing gap. Enterprise platforms (project44 at $6,250+/month minimum, FourKites with enterprise contracts) are inaccessible to mid-market buyers. The competitive landscape analysis found that a mid-market forwarder handling 500-5,000 containers/month "has no ideal solution today -- they either overpay for enterprise tools or cobble together cheaper alternatives that lack polish."

Specific evidence:
- TRADLINX's aggressive per-B/L pricing ($1.11-$1.39/B/L) and explicit competitive positioning against project44 demonstrate that price-conscious buyers exist and are actively switching.
- Terminal49's free tier of 100 containers is the strongest developer acquisition funnel in the market, validating the freemium model.
- The customer discovery research found that logistics tech startups evaluate platforms by "documentation quality, sandbox experience, and API design before talking to sales" -- they explicitly avoid enterprise sales processes.
- 92% of forwarding agents expect margins to tighten further in 2026, making cost-conscious tooling decisions more urgent.

### b) "Comes with SDKs" -- Is the developer persona real?

**Verdict: Supported, but the developer market is smaller than assumed.**

The customer discovery research identifies logistics tech developers as "almost certainly the best primary segment." These include digital forwarders (Navio, Nowports, Nuvocargo), TMS builders (GoFreight, Reform), visibility tool builders, and freight marketplaces. YC alone has funded 50+ supply chain/logistics startups.

However, the total addressable developer population is modest. The research estimates 300-500 logistics tech companies globally that would consume a carrier tracking API. This is not a massive developer ecosystem like payments (Stripe) or communications (Twilio). The logistics developer community is "nascent compared to fintech or SaaS" -- there is no dominant Slack/Discord community, and developers participate in broader communities rather than logistics-specific ones.

Critically, **traditional freight forwarders like SSL are not the developer buyer.** They have zero developers on staff. The customer discovery research is blunt: "Small forwarders like SSL are a pain-signal source but not the ideal first customer for an API product." SSL needs a finished dashboard product, not an SDK.

The open-source SDK strategy helps here: it extends reach beyond paying customers by creating a community asset that attracts developers even before the managed platform launches.

### c) "Solid margins while undercutting" -- Do the unit economics support this?

**Verdict: Strongly supported.**

The pricing research demonstrates definitively viable unit economics:

| Price Point | Variable Cost | Gross Margin |
|---|---|---|
| $1.00/container/month | $0.12 | 88% |
| $1.50/container/month | $0.12 | 92% |
| $2.00/container/month | $0.10 | 95% |

The critical input: **carrier API access is free** across all major carriers (Maersk, MSC, Hapag-Lloyd, CMA CGM, Evergreen, ONE, HMM, ZIM). The entire variable cost is compute infrastructure ($0.08-$0.15/container/month on AWS). This means the platform's margin structure is similar to a pure software business, not a data resale business.

At $1.50/container, the platform undercuts Vizion by 70%, Terminal49 by 50-62%, and project44 by 75%+ -- while maintaining 92% gross margins. The pricing research shows break-even at 33,333 containers/month on a lean team ($45K/month burn), achievable with 67-133 customers averaging 250-500 containers each.

### d) "Inttra is overpriced and dated" -- Is Frank's perception accurate?

**Verdict: Accurate on the technology, but the competitive picture is more nuanced.**

The competitive landscape research validates that INTTRA's technology "reflects its early-2000s origins." Industry observers describe it as "a system that gets the job done slowly and with room for error." The platform is "EDI-centric" and "rigid and expensive to maintain." It has only 3 reviews on G2 despite claiming 35,000 active shippers -- a striking signal of user disengagement.

However, INTTRA's competitive position is more defensible than "overpriced and dated" implies:
- It processes 25% of global ocean container bookings through a 60+ carrier network.
- Its network effects are real: carriers are there because shippers are there.
- The booking workflow is where INTTRA's moat is strongest. No new entrant can replicate the booking network quickly.
- The WiseTech acquisition, while creating vendor lock-in concerns, also gives INTTRA the resources of a $16B market cap parent.

The nuance Frank may be missing: **INTTRA is weakest in tracking/visibility and strongest in booking.** A competitive strategy should target tracking first (where alternatives are abundant and INTTRA adds little value) and avoid direct competition on booking (where network effects protect them). Over time, as DCSA Booking APIs mature, the booking moat erodes.

---

## 4. Competitive Positioning

### Where the Product Fits

The competitive landscape maps along two axes: developer-friendly vs. enterprise/portal, and point solution vs. platform/suite. The whitespace is in the **developer-friendly, feature-rich quadrant** -- a product that combines the API polish of Vizion/Terminal49 with pricing accessibility of TRADLINX/Shipsgo, built on a DCSA-native architecture that no existing player has.

### Positioning Statement

"The open-source carrier integration SDK for logistics developers. Track containers across 30+ carriers through a single, DCSA-native API. Usage-based pricing starting at $0/month."

### Direct Competitors

| Competitor | Overlap | Key Difference |
|---|---|---|
| **Vizion** | API-first, webhook-driven, developer-focused | We are 70% cheaper, open-source SDK, DCSA-native |
| **Terminal49** | Developer-friendly, free tier, API + dashboard | We have more carriers, open-source SDK, lower pricing |
| **TRADLINX** | Cheapest per-B/L pricing, SMB focus | We offer SDKs and developer tools; they are portal-first |
| **Shipsgo** | Credit-based, SMB-friendly | We are API-first; they are portal-first |

### Indirect Competitors

| Competitor | Overlap | Why They Are Indirect |
|---|---|---|
| **project44** | Container tracking data | Enterprise-only, $6,250/month minimum, different buyer |
| **FourKites** | Supply chain visibility | Enterprise-only, trucking-first, different buyer |
| **CargoWise** | Carrier connectivity bundled in TMS | TMS platform, not a standalone API product |
| **INTTRA/E2open** | Carrier network, booking | Legacy EDI, booking focus, different value prop |

### Competitive Moat Assessment

The honest assessment: the moat is **narrow but real**.

- **Open-source SDK** creates distribution and community that no competitor has. Once developers build on your SDK, switching costs increase.
- **DCSA-native architecture** provides structural cost advantages over platforms that must retrofit.
- **Carrier adapter maintenance** is the unglamorous but real moat. Maintaining reliable integrations across 30+ carriers as they update APIs, change auth mechanisms, and modify response schemas is tedious, expensive work. Customers pay to avoid it.
- **Pricing** alone is not a moat. Competitors can match pricing. The moat is pricing + DX + open-source -- the combination is hard to replicate.

What is NOT a moat: data access (carrier APIs are free and public), tracking data itself (commodity), or carrier coverage (anyone can build adapters given enough time).

---

## 5. Beachhead Market Recommendation

**Primary beachhead: Logistics technology companies (developers building freight platforms).**

This segment is recommended based on converging evidence from the customer discovery and competitive landscape research:

1. **They have the pain.** Each carrier integration costs 2-6 engineer-weeks to build and 1-4 weeks/year to maintain. A startup integrating 10 carriers diverts 30-60 weeks of engineering time from their core product. At $200K/year loaded cost per engineer, that is $120K-$230K in opportunity cost.

2. **They have the budget.** Startups in this segment spend $100-$5,000/month on carrier data services, scaling to $20,000/month at growth stage. The ROI calculation is straightforward: if the platform saves one engineer-month of integration work, it pays for itself at any reasonable price point.

3. **They have the buying behavior.** Short sales cycle, self-serve evaluation, decision made by CTO or founding engineer. No procurement process, no 6-month enterprise sales cycle.

4. **They are growing.** YC has funded 50+ supply chain startups. Digital freight forwarding is growing at 18.8% CAGR. New logistics tech companies launch continuously, each needing carrier data from day one.

5. **They amplify reach.** When a logistics tech company builds on the platform, every customer of that company becomes an indirect user. Vizion's case study of CANdata building Freight Flow on Vizion's API, which then serves Alcon Logistics, illustrates this multiplier effect.

**Secondary beachhead: Mid-market freight forwarders (500-5,000 containers/month) with IT staff**, but only after a dashboard/portal product is built on top of the API. This segment has budget ($1,000-$10,000/month) and pain (WiseTech lock-in anxiety, rising CargoWise costs), but needs a finished product, not developer tools.

---

## 6. Strategic Risks

### Risk 1: WiseTech Vertical Integration

**Severity: High. Probability: Medium.**

WiseTech now controls CargoWise (~70% TMS market share) and INTTRA/E2open (~25% of global container bookings). If WiseTech bundles superior tracking/visibility into CargoWise at no additional cost, the addressable market for standalone tracking products shrinks significantly. The CargoWise pricing restructure (moving to per-shipment "Value Packs") creates the billing mechanism for bundled visibility.

**Mitigating factors:** WiseTech's integration of E2open/INTTRA is a multi-year project. WiseTech's acquisitions often result in "different modules exhibiting different levels of modernization." CargoWise's rising costs are pushing some forwarders to evaluate alternatives. And the developer/logistics-tech segment is largely outside the CargoWise ecosystem -- startups building new freight platforms are not CargoWise customers.

### Risk 2: DCSA Commoditization

**Severity: Medium. Probability: Medium-High over 3-5 years.**

As DCSA standardization matures, the integration layer becomes thinner. When every carrier exposes a DCSA-compliant Track & Trace API with identical schemas, the value of an aggregation platform diminishes. A developer could integrate directly with 10 DCSA carriers using a thin wrapper library.

**Mitigating factors:** DCSA defines the API contract but not implementation quality. Response times, data freshness, error handling, and authentication mechanisms vary significantly across carriers even when they claim DCSA compliance. The long tail of non-DCSA carriers (~25% of capacity, dozens of regional operators) will persist. And the managed platform layer (hosted polling, webhooks, event history, analytics) provides value beyond raw API aggregation.

### Risk 3: Market Size Insufficient for Meaningful Returns

**Severity: Medium. Probability: Medium.**

The SOM for years 1-3 ($2-5M ARR) is meaningful for a bootstrapped business but not for a venture-backed company needing to grow to $50M+ ARR. The ocean-only API market has approximately 4,500 current buyers globally. At $1.50/container and moderate volumes, even winning 10% of the market yields only $10-15M ARR.

**Mitigating factors:** Multimodal expansion (air, rail, drayage) multiplies the addressable market. The platform can expand from tracking into booking, schedules, and document management. Intelligence features (predictive ETAs, carrier scoring) command premium pricing. The $2-5M ARR year-3 target is viable for a lean team with no venture capital.

### Risk 4: Carriers Start Charging for API Access

**Severity: High. Probability: Low in near term, medium in 3-5 years.**

The entire margin structure depends on free carrier API access. Maersk explicitly "reserves the right to charge in the future." If carriers impose per-call fees, the $0.08-$0.15 variable cost per container could increase significantly.

**Mitigating factors:** Carriers benefit from third-party platforms that drive adoption of their digital services. Charging for API access would slow DCSA adoption. Intelligent caching and polling optimization can reduce API call volume by 50-70%.

### Risk 5: Timing

**Severity: Low-Medium. Probability: Low.**

The question is whether the window is opening or closing. The evidence suggests it is opening: DCSA adoption is accelerating, WiseTech consolidation is creating switching moments, and the logistics tech startup ecosystem is growing. However, Vizion (founded 2018, $18.7M raised) and Terminal49 (founded 2017, $8.7M raised) have an 8-year head start in carrier relationships and integration maintenance.

**Assessment:** The timing is favorable. DCSA convergence makes new entrant economics dramatically better than even 3 years ago. The open-source angle is differentiated enough to overcome the head start.

---

## 7. The WiseTech Factor

WiseTech Global's $2.1B acquisition of E2open (completed August 2025) is the single most consequential event in the ocean freight technology landscape. It deserves dedicated analysis because it simultaneously creates and threatens opportunity.

### What WiseTech Now Controls

| Asset | Market Position |
|---|---|
| **CargoWise** | ~70% of forwarding software market; 16,500 customers in 195 countries; 24 of top 25 3PLs |
| **INTTRA/E2open** | ~25% of global container bookings; 60+ carrier network; 35,000+ shippers |
| **Softship** | Legacy ocean freight TMS (acquired earlier) |

Combined, WiseTech has a plausible path to controlling the full carrier-to-forwarder data pipeline: booking flows through INTTRA, operations run on CargoWise, and carrier connectivity is bundled.

### Does This Create Opportunity or Threat?

**Both -- but in different segments.**

**Threat (for CargoWise customers):** WiseTech can bundle tracking into CargoWise Value Packs, making standalone tracking products less attractive for the 16,500 CargoWise customers. If WiseTech executes well on integration, the mid-market forwarder segment (which overlaps heavily with CargoWise's customer base) becomes harder to win.

**Opportunity (for everyone else):**

1. **Vendor lock-in anxiety.** The customer discovery research identifies "vendor consolidation anxiety" as a high-frequency switching trigger happening now (2025-2026). Forwarders using INTTRA are reconsidering their dependency on a platform now controlled by WiseTech. The positioning angle: "Your carrier data shouldn't be controlled by your TMS vendor."

2. **CargoWise pricing revolt.** WiseTech's late-2025 transition to Value Pack pricing increased costs 25-35% for some forwarders. DSV is migrating from CargoWise to DB Schenker's Tango TMS. This pricing disruption creates unusual market receptivity to unbundled alternatives.

3. **The non-CargoWise segment.** Logistics tech startups -- the primary beachhead segment -- are not CargoWise customers. They are building their own platforms and need carrier data as an input, not a TMS feature. WiseTech's consolidation is irrelevant to their buying decision.

### Strategic Implication

**Avoid direct competition with CargoWise-bundled tracking.** Instead, target the segments WiseTech cannot reach: logistics tech developers who need APIs (not a TMS), forwarders migrating away from CargoWise, and startups building the next generation of freight platforms. Position as vendor-neutral infrastructure, not an operational platform.

---

## 8. Recommended Product Strategy

### Core Product: Open-Source SDK + Managed Platform

**Open-source SDK (free, MIT licensed, published to npm):**
- TypeScript library for ocean carrier API integration
- Carrier authentication management (OAuth2, API Key, JWT, Bearer Token per carrier)
- Request construction and response parsing
- Normalization to DCSA data model (Track & Trace v2.2 event types and classifiers)
- Local caching layer for rate limit management
- 12 carrier adapters at launch (9 DCSA-compliant + 3 proprietary)

**Managed platform (paid, usage-based SaaS):**
- Hosted polling infrastructure (configurable intervals per transit phase)
- Webhook delivery for event-driven updates
- Persistent event history (all tracking events stored and queryable)
- Multi-tenant credential management
- Monitoring, alerting, and reliability guarantees
- Analytics dashboard (carrier performance, transit times, exception rates)

This mirrors the Elastic/GitLab/Redis model: open-source core drives adoption and trust; the managed platform captures revenue from production workloads.

### Pricing (per the unit economics research)

| Tier | Price | Target |
|---|---|---|
| **Free** | $0/month, 500 containers | Developers, sandbox, very small operators |
| **Growth** | $1.50/container (first 10K), $1.00 (10K-100K), $0.75 (100K+) | Logistics tech startups, mid-market forwarders |
| **Business** | $0.75/container + $500/month platform fee | Companies needing SLA and priority support |
| **Enterprise** | Custom | High-volume, custom requirements |

At the Growth tier, tracking 1,000 containers/month costs $1,500 -- compared to $5,000 at Vizion, $3,000-$4,000 at Terminal49, and $6,250+ at project44. The price/value ratio is the strongest in the market while maintaining 88%+ gross margins.

### Carrier Coverage Priorities

| Priority | Carriers | Rationale |
|---|---|---|
| **Launch (P0)** | Maersk, MSC, Hapag-Lloyd, CMA CGM, Evergreen | Top 5 by capacity (~64% of global fleet). All DCSA-aligned. |
| **Fast-follow (P1)** | ONE, HMM, Yang Ming, ZIM | DCSA members. Completes top 9 carrier coverage (~82% of global capacity). |
| **Expand (P2)** | COSCO, Grimaldi, Eimskip | Proprietary APIs requiring custom adapters. COSCO has official OSS client. |
| **Long-tail (P3)** | Crowley, Matson, Wan Hai, SM Line, others | EDI/portal-only. Out of scope for v1; evaluate scraping or EDI later. |

### Build Timeline

Based on the engineering cost estimates from the pricing research:

| Phase | Duration | Output |
|---|---|---|
| SDK core + DCSA base adapter | 6 weeks | TypeScript library, DCSA type definitions, shared adapter framework |
| 5 P0 carrier adapters | 8 weeks | Maersk, MSC, Hapag-Lloyd, CMA CGM, Evergreen |
| Testing, docs, npm publish | 4 weeks | Open-source SDK launch |
| Managed platform infrastructure | 8 weeks | Polling, webhooks, event storage, API gateway |
| 4 P1 carrier adapters | 4 weeks | ONE, HMM, Yang Ming, ZIM |
| **Total to production** | **~30 weeks (7-8 months) with 2 engineers** | SDK + managed platform with 9 carriers |

### Year-1 Financial Model (Moderate Scenario)

| Metric | Value |
|---|---|
| Monthly revenue (end of Year 1) | $78,000 |
| Annual revenue | $936,000 |
| Gross margin | 92% |
| Monthly burn (3-person team) | $72,500 |
| Operating margin | 7.6% |
| 18-month cash requirement (including build phase) | ~$540K-$990K |

---

## 9. Go / No-Go Recommendation

### Recommendation: Conditional GO

The research supports pursuing this opportunity under specific conditions. The case is built on five pillars:

**Pillar 1: The unit economics are excellent.** 88-92% gross margins at target pricing. Free upstream data (carrier APIs). Variable costs under $0.15/container. Break-even achievable within 12 months of launch on a lean team. This is not a business that needs $50M in venture capital to reach profitability.

**Pillar 2: A genuine whitespace exists.** No open-source SDK for ocean carrier API integration exists in any language. The competitive landscape confirms that "the mid-market is dramatically underserved" and that a DCSA-native platform built today has structural cost advantages over legacy competitors. The open-source + managed platform model is unmatched in this market.

**Pillar 3: The timing is favorable.** DCSA adoption is accelerating (9 carriers, ~75% of capacity). WiseTech consolidation is creating switching windows. CargoWise pricing changes are pushing forwarders to evaluate unbundled alternatives. The logistics tech startup ecosystem is growing (18.8% CAGR in digital freight forwarding).

**Pillar 4: The risk profile is manageable.** The main risks (WiseTech vertical integration, DCSA commoditization, market size limits) are real but mitigable through segment focus (developers, not CargoWise customers), value-layer differentiation (DX, reliability, intelligence features), and multimodal expansion.

**Pillar 5: The downside is limited.** Even if the SaaS platform fails to achieve product-market fit, the open-source SDK has standalone value as a community asset and as the integration layer for SSL's own operations. The steamship-integrations work already planned for SSL is not wasted -- it becomes the foundation of the SDK.

### The Conditions

1. **Do not raise venture capital for this.** The SOM ($2-5M ARR in 3 years) does not support venture expectations. This is a bootstrapped or angel-funded business. The $540K-$990K 18-month cash requirement can be covered by savings, a small angel round, or consulting revenue.

2. **Target developers first, forwarders second.** The original hypothesis assumed freight forwarders like SSL would be the primary buyer. The research disproves this. The API product must be built for software developers. A forwarder-facing portal product can come later, built on top of the API.

3. **Start with the SDK, not the platform.** The open-source SDK is the distribution engine. Ship it first, build community, then launch the managed platform once there is adoption signal. This derisks the investment by validating demand before building the paid product.

4. **Plan for multimodal expansion.** Ocean-only is a viable starting point but not a terminal destination. The path to $10M+ ARR requires expanding to air freight, rail, and drayage tracking.

### If GO: Next Steps

1. **Complete the steamship-integrations SDK for SSL.** This is already planned and serves dual purpose: operational tool for SSL + foundation for the open-source SDK.
2. **Publish the SDK to npm under MIT license.** Establish the open-source project with documentation, examples, and contributor guidelines.
3. **Join DCSA+ as a technology partner.** Access implementation support, early-stage testing, and industry credibility.
4. **Build the managed platform.** Hosted polling, webhooks, event storage, and API gateway.
5. **Launch with transparent pricing page.** $0 free tier, usage-based growth tier. No "contact sales."
6. **Developer marketing.** Technical blog posts on carrier API integration, presence in logistics dev communities, conference talks at DCSA Week and logistics tech events.

### If NO-GO: What Happens to the SDK Work

The steamship-integrations SDK for SSL proceeds regardless -- it has clear value as an internal tool for SSL's operations (automated tracking, cutoff monitoring, demurrage avoidance). The SDK simply remains a private, internal tool rather than becoming the foundation of a SaaS business.

---

## 10. Open Questions

The following questions remain unresolved and would materially de-risk the go decision:

| Question | Why It Matters | How to Resolve |
|---|---|---|
| **How many logistics tech companies actively pay for carrier tracking APIs today?** | Market.us estimates 4,500 companies using container tracking APIs, but how many pay vs. use free tiers or build in-house? | Conduct 10-15 customer discovery interviews with logistics tech CTOs |
| **What is Vizion's actual ARR and customer count?** | If Vizion (the closest competitor) has not achieved product-market fit despite $18.7M in funding, that is a warning signal | Public filings are unavailable; estimate from employee count and pricing |
| **Will carriers start charging for API access?** | Free API access is the foundation of the margin structure. Maersk's reservation of rights to charge is a latent risk | Monitor carrier API terms; build rate-limit-aware caching from day one |
| **How sticky is the CargoWise lock-in?** | If forwarders cannot practically switch away from CargoWise (and its bundled INTTRA integration), the mid-market forwarder segment may be smaller than estimated | Interview mid-market forwarders currently evaluating TMS alternatives |
| **Is there appetite for an open-source ocean freight SDK?** | The strategy depends on developer adoption of the OSS SDK. Developer communities in logistics are nascent | Ship the SDK, monitor GitHub stars and npm downloads, gauge community engagement |
| **What is the real switching cost for logistics tech companies currently using Vizion or Terminal49?** | If switching costs are low, customers may be easy to acquire; if high (tight API coupling), harder | Review Vizion and Terminal49 API contracts; assess data model portability |
| **Can a 2-3 person team maintain 12+ carrier adapters reliably?** | Carrier APIs change without notice. Maintenance burden could exceed capacity of a small team | Track actual maintenance hours during SSL SDK development as a proxy |

The highest-priority action is **customer discovery interviews with 10-15 logistics tech CTOs**. This would validate the developer buyer persona, confirm willingness to pay, and surface unmet needs that the research-only approach cannot capture. The cost is minimal (2-3 weeks of outreach and calls) and the risk-reduction is significant.

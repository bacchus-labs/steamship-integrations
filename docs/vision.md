# OpenPort: The Open-Source Carrier Integration Platform

> A developer-first API platform for ocean freight data, built on an open-source SDK that normalizes 30+ carrier APIs to a single DCSA-native interface. Usage-based pricing starting at $0/month.

---

## The Problem

Every company that touches ocean freight -- freight forwarders, logistics tech startups, 3PLs, cargo owners -- needs data from ocean carriers: where is my container, when will it arrive, has the schedule changed, what are the cutoff deadlines. Today, getting that data is painful:

- **Major carriers expose APIs, but every one is different.** Maersk uses OAuth2 + API Key (different auth for different paths). MSC requires partner onboarding. Hapag-Lloyd uses IBM API Connect. Grimaldi has a proprietary WebAPI. Even among carriers implementing the DCSA standard, implementations vary in data quality, response time, and completeness.

- **Building carrier integrations is expensive.** Each carrier adapter costs 2-6 engineer-weeks to build and 1-4 weeks/year to maintain. A startup integrating 10 carriers diverts 30-60 weeks of engineering time from their core product -- $120K-$230K in opportunity cost.

- **Existing solutions are either overpriced, legacy, or enterprise-gated.** Vizion charges $5/container. Terminal49 charges $3-10/container. project44 has a $6,250/month minimum. INTTRA (now owned by WiseTech Global) is EDI-centric with dated UX. No solution offers an open-source SDK, transparent pricing, and developer-grade documentation in one package.

- **No open-source alternative exists.** We searched. The closest thing is a dead Python scraping library with 7 carriers and no standards alignment. No TypeScript/JavaScript SDK for ocean carrier API integration exists in any form, in any language.

---

## The Opportunity

Three structural shifts are converging to create a window:

### 1. DCSA Standardization

The Digital Container Shipping Association (founded 2019 by 9 carriers representing ~75% of global container capacity) is driving adoption of common API standards for Track & Trace, Booking, and Commercial Schedules. For the first time, building a multi-carrier integration platform can lean on shared data models rather than bespoke adapters per carrier. This reduces integration cost by roughly 60% compared to five years ago.

### 2. WiseTech Vertical Integration

WiseTech Global acquired E2open (which owns INTTRA) for $2.1B in 2025 and already owns CargoWise (~70% of the forwarding TMS market). This consolidation is triggering vendor lock-in anxiety across the industry. DSV is migrating off CargoWise. CargoWise's 2025 pricing restructure (25-35% cost increases for some forwarders) is pushing customers to evaluate unbundled alternatives. The switching window is open now but will narrow as integration settles.

### 3. The Logistics Tech Startup Boom

Digital freight forwarding is growing at 18.8% CAGR. YC alone has funded 50+ supply chain/logistics startups. Each one needs carrier data from day one, and none of them want to spend engineering time building and maintaining carrier integrations when they could be working on their core product.

---

## The Product

### Open-Source SDK (free, MIT-licensed)

A TypeScript library published to npm that handles the hard parts of carrier API integration:

- **Unified interface** -- one `track()` call works across all carriers
- **DCSA-native data model** -- all carrier events normalized to standard event codes (GTOT, GTIN, LOAD, DISC, ARRI, DEPA) and classifiers (PLN, EST, ACT)
- **Carrier authentication** -- OAuth2, API Key, JWT, Bearer Token handled per carrier
- **12 carrier adapters at launch** -- 9 DCSA-compliant (Maersk, MSC, Hapag-Lloyd, CMA CGM, Evergreen, ONE, HMM, Yang Ming, ZIM) + 3 proprietary (Grimaldi, COSCO, Eimskip), covering ~82% of global container capacity
- **Rate limit management** -- intelligent caching and backoff per carrier
- **Type-safe** -- full TypeScript types generated from DCSA OpenAPI specs

```typescript
import { OpenPort } from '@openport/sdk';

const client = new OpenPort({
  carriers: {
    maersk: { clientId: '...', clientSecret: '...' },
    msc: { apiKey: '...' },
  },
});

const shipment = await client.track({
  carrier: 'MAEU',
  containerNumber: 'MSKU1234567',
});

// shipment.currentMilestone -> 'LOAD'
// shipment.milestones -> [{ code: 'GTOT', classifier: 'ACT', timestamp: '...' }, ...]
// shipment.cutoffs -> [{ code: 'VCO', deadline: '...', status: 'upcoming' }, ...]
// shipment.route -> { origin: 'CNSHA', destination: 'USOAK', vessel: '...', eta: '...' }
```

The SDK is the distribution engine. Developers adopt it for free, build on it, contribute carrier adapters back. This creates a community asset and developer trust that no closed-source competitor can match.

### Managed Platform (paid, usage-based SaaS)

For production workloads, the managed platform adds infrastructure that individual developers don't want to build or operate:

- **Hosted polling** -- configurable intervals per transit phase (every 4 hours during ocean transit, every hour during port operations)
- **Webhook delivery** -- event-driven push notifications when milestones change, ETAs shift, or cutoffs approach
- **Event history** -- persistent storage of all tracking events, queryable via API
- **Multi-tenant credential management** -- securely store and rotate carrier credentials
- **Reliability guarantees** -- monitoring, alerting, automatic failover, SLA
- **Analytics** -- carrier performance dashboards, transit time analysis, exception rates

This is the Elastic / Redis / GitLab model: open-source core drives adoption and trust; the managed platform captures revenue from production workloads where reliability, convenience, and SLA matter.

---

## Who It's For

### Primary: Logistics Technology Companies

The research is unambiguous -- the beachhead customer is the software developer building freight platforms, not the traditional freight forwarder.

These are companies like:
- **Digital forwarders** (Navio, Nowports, Nuvocargo) building modern logistics platforms
- **TMS vendors** (GoFreight, Reform) who need carrier data in their products
- **Visibility tool builders** adding tracking to their platforms
- **Freight marketplaces** offering shipment status to their users

They have developers. They consume APIs natively. They evaluate products by documentation quality and sandbox experience before talking to sales. They have immediate, measurable pain (engineering hours diverted to carrier integrations). And when they build on OpenPort, every customer of theirs becomes an indirect user -- a multiplier effect.

### Secondary: Mid-Market Freight Forwarders

Forwarders handling 500-5,000 containers/month -- too sophisticated for manual tracking, too cost-conscious for enterprise platforms. They have small IT teams (1-5 people) who can work with APIs, budgets of $1,000-$10,000/month, and growing frustration with WiseTech lock-in.

This segment comes second because they need more than an API -- they need a dashboard, alerts, and customer-facing tracking portal. These will be built on top of the API platform as it matures.

---

## Pricing

| Tier | Price | What You Get |
|------|-------|-------------|
| **Free** | $0/month, 500 containers | Full API access, SDK, sandbox. No credit card required. |
| **Growth** | $1.50/container (first 10K), $1.00 (10K-100K), $0.75 (100K+) | Hosted polling, webhooks, event history, email support |
| **Business** | $0.75/container + $500/month | Priority support, SLA guarantee, dedicated account |
| **Enterprise** | Custom | SSO, custom integrations, on-prem SDK option |

**How this compares:**

| Tracking 1,000 containers/month | Monthly Cost |
|---------------------------------|-------------|
| **OpenPort (Growth)** | **$1,500** |
| Vizion | $5,000 |
| Terminal49 | $3,000-$4,000 |
| project44 | $6,250+ (minimum) |
| TRADLINX | $1,250-$1,390 |

At $1.50/container, we undercut Vizion by 70% and Terminal49 by 50-62%, while maintaining 88-92% gross margins. The free tier of 500 containers is generous enough for development and small production workloads, driving adoption without requiring a sales conversation.

---

## Unit Economics

The numbers work because **carrier API access is free** across all major carriers.

| Metric | Value |
|--------|-------|
| Variable cost per container/month | $0.08-$0.15 |
| Gross margin at $1.50/container | 88-92% |
| Monthly fixed costs (lean 2-person team) | $38K-$57K |
| Break-even containers/month | ~33,000 |
| Break-even customers (avg. 250-500 containers each) | 67-133 |

### Year 1-3 Financial Model (Moderate Scenario)

| | Year 1 | Year 2 | Year 3 |
|---|--------|--------|--------|
| Customers | 50-200 | 200-500 | 500-1,000 |
| Containers/month | 10K-50K | 50K-150K | 150K-400K |
| Avg. price/container | $1.50 | $1.25 | $1.00 |
| Annual revenue | $180K-$900K | $750K-$2.25M | $1.8M-$4.8M |
| Gross margin | 88-92% | 90-92% | 91-93% |
| Team size | 2-3 | 3-4 | 4-6 |

The 18-month cash requirement (including ~7 months of build before revenue) is $540K-$990K. This is fundable through savings, a small angel round, or consulting revenue. Venture capital is not appropriate -- the ocean-only SOM of $2-5M ARR at year 3 doesn't support venture return expectations. This is a bootstrapped or lightly-funded business with a path to profitability in year 1-2 post-launch.

---

## Competitive Positioning

The market segments into four quadrants:

```
                    Developer-Friendly
                          |
          OpenPort        |        Vizion
          (open-source,   |        (API-first,
           usage-based)   |         $5/container)
                          |
    Accessible  ----------+----------  Premium
                          |
          TRADLINX        |        project44
          Shipsgo         |        FourKites
          (budget,        |        ($6,250+/mo,
           portal-first)  |         enterprise)
                          |
                    Enterprise/Portal
```

**Our quadrant** (developer-friendly + accessible) is empty. Vizion is developer-friendly but expensive. TRADLINX is cheap but portal-first with no SDK. project44 is enterprise-only. Nobody occupies the intersection of great developer experience, open-source foundation, and aggressive usage-based pricing.

### What's NOT a Moat

- Data access (carrier APIs are free and public)
- Tracking data itself (commodity)
- Carrier coverage given sufficient time (anyone can build adapters)

### What IS a Moat

- **Open-source SDK community** -- once developers build on the library, switching costs increase and the community contributes carrier adapters, bug fixes, and ecosystem tools
- **DCSA-native architecture** -- structural cost advantages over platforms retrofitting legacy integrations
- **Carrier adapter maintenance** -- the unglamorous but real barrier. Maintaining reliable integrations across 30+ carriers as APIs evolve is tedious, expensive work. Customers pay to avoid it.
- **Developer trust and distribution** -- npm downloads, GitHub stars, and Stack Overflow answers create compounding awareness that closed-source competitors can't replicate

---

## Roadmap

### Phase 0: SDK for SSL (already in progress)
- Complete the steamship-integrations SDK for Sea Shipping Line
- This work serves dual purpose: operational tool for SSL + foundation for the open-source SDK
- Validates architecture and carrier adapter patterns against real production needs

### Phase 1: Open-Source Launch (months 1-4)
- Extract, clean, and generalize the SSL SDK into a publishable open-source library
- 5 P0 carrier adapters (Maersk, MSC, Hapag-Lloyd, CMA CGM, Evergreen -- ~64% of global capacity)
- Full TypeScript types, documentation, examples, contributor guide
- Publish to npm under MIT license
- **Goal:** Establish the project, attract early adopters, gather feedback

### Phase 2: Platform MVP (months 4-8)
- 4 P1 carrier adapters (ONE, HMM, Yang Ming, ZIM -- brings total to ~82% of capacity)
- Hosted polling infrastructure
- Webhook delivery
- Event history storage and query API
- Multi-tenant credential management
- Pricing page, Stripe billing integration
- **Goal:** First paying customers. Free tier drives adoption, Growth tier captures production workloads.

### Phase 3: Growth (months 8-18)
- P2 carrier adapters (COSCO, Grimaldi, Eimskip -- proprietary APIs)
- Analytics dashboard
- Forwarder-facing portal product (tracking dashboard, alerts, customer-branded tracking pages)
- Join DCSA+ as technology partner
- Developer marketing: technical blog, conference talks, logistics dev community presence
- **Goal:** Product-market fit in the logistics tech developer segment. 200+ customers, $750K+ ARR.

### Phase 4: Expansion (months 18+)
- Multimodal expansion (air freight, drayage, rail) -- this is the path from $5M to $50M+ ARR
- Booking API support as DCSA Booking standard matures
- Predictive ETA intelligence (ML layer on top of historical event data)
- Schedule reliability analytics
- Document management APIs

---

## Risks

| Risk | Severity | Mitigation |
|------|----------|------------|
| **WiseTech bundles tracking into CargoWise** | High | Our beachhead (logistics tech devs) is outside the CargoWise ecosystem. Position as vendor-neutral infrastructure. |
| **DCSA makes direct integration trivial** | Medium | DCSA defines contracts, not quality. Value comes from normalization, reliability, long-tail carriers, and the managed platform layer. |
| **Carriers start charging for API access** | High (impact), Low (probability near-term) | Build rate-limit-aware caching from day one. Carriers benefit from third-party adoption driving their digital services. |
| **Market too small for meaningful returns** | Medium | Ocean-only SOM is $2-5M. Multimodal expansion is the answer. Plan for it from the start. |
| **Vizion/Terminal49 drop prices to match** | Medium | Open-source SDK is ours alone. Community distribution can't be replicated by dropping prices. |
| **2-3 person team can't maintain 12+ adapters** | Medium | Track actual maintenance hours during SSL work. AI-assisted development reduces maintenance burden. Community contributions help for popular carriers. |

---

## What Makes This Different

Most logistics technology is built by logistics people learning technology. This would be built by technologists learning logistics -- and that's the point. The industry's technology stack reflects decades of EDI-era thinking. Carrier APIs exist now. DCSA standards are maturing. The tools to build a modern integration layer are available. What's missing is someone building it the way developers expect: open-source core, great documentation, transparent pricing, and an API you can call in 5 minutes instead of waiting 6 weeks for a sales call.

The ocean shipping industry moves $14+ trillion in goods annually. The companies orchestrating that movement deserve tools built to modern standards. That's what we'd build.

---

## Next Steps

1. **Validate the developer buyer persona.** Conduct 10-15 customer discovery interviews with logistics tech CTOs. Confirm they'd use an open-source SDK. Confirm willingness to pay for the managed platform. Surface unmet needs the desk research didn't capture.

2. **Complete the SSL SDK.** The work already planned for Sea Shipping Line becomes the foundation. Every design decision, every carrier adapter, every normalization pattern feeds directly into the open-source project.

3. **Name and register.** Secure npm package name, GitHub org, domain. "OpenPort" is a working name -- needs trademark clearance.

4. **Determine funding approach.** The 18-month cash requirement is $540K-$990K. Options: bootstrap with consulting revenue, small angel round, or a combination. No venture capital.

---

## Reference Materials

All supporting research lives in this repository:

| Document | Location |
|----------|----------|
| Container Shipping 101 | `docs/industry/container-shipping-101.md` |
| Players and Roles | `docs/industry/players-and-roles.md` |
| Freight Forwarder Business Model | `docs/industry/freight-forwarder-business.md` |
| Shipping Technology Landscape | `docs/industry/shipping-technology-landscape.md` |
| Use Cases for Carrier API Data | `docs/industry/use-cases-for-carrier-api-data.md` |
| Competitive Landscape | `.wingman/notes/competitive-landscape-carrier-integration-platforms.md` |
| Customer Discovery | `.wingman/notes/customer-discovery-demand-signals.md` |
| Pricing & Unit Economics | `.wingman/notes/pricing-unit-economics-model.md` |
| Market Sizing & Opportunity Synthesis | `.wingman/notes/market-sizing-opportunity-synthesis.md` |
| Open-Source Landscape | `.wrangler/memos/open-source-landscape-research.md` |
| SSL Business Context | `.wrangler/memos/context-on-existing-state-for-rate-requests.md` |
| Carrier API Audit Spec | `.wrangler/specifications/steamship-line-api-audit.md` |
| Carrier Index (~45 carriers) | `docs/steamship-lines.md` |
| Per-Carrier API Inventories | `docs/carriers/` |

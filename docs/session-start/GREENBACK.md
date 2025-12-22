# GreenBack - Session Start Document

> **Read this first.** This document contains everything needed to start a productive session on GreenBack.

---

## 1. Quick Context

| Field | Value |
|-------|-------|
| **Project** | GreenBack |
| **Tagline** | "Get your green back" |
| **What** | Climate incentive discovery platform with homeowner calculator + contractor ecosystem |
| **Stack** | SvelteKit + Supabase + Railway |
| **Revenue** | Lead gen ($50-200/lead) + Contractor SaaS ($79-199/mo) + Financing referrals |
| **Target** | $5-10K/month at scale |
| **Status** | Planning Complete |
| **Repo** | Not yet created |
| **Domain** | getgreenback.com, greenback.io (TBD) |

---

## 2. Full Vision

### What is GreenBack?

GreenBack helps homeowners discover climate incentives they're missing - federal tax credits, state rebates, utility programs, and local incentives - all in one personalized view. Then it connects them with vetted contractors who can help them claim those incentives.

**The double meaning:**
- "Green" = money (get your money back)
- "Green" = climate (get rewarded for going green)

**Two-sided platform:**
1. **For Homeowners:** Free calculator showing all incentives they qualify for
2. **For Contractors:** Paid leads + SaaS dashboard for sales enablement

### Why This Will Work

1. **$369 billion opportunity** - IRA allocated massive funding for clean energy
2. **Fragmented discovery** - Incentives scattered across 50 states, thousands of utilities
3. **Major transition Dec 2025** - Federal credits expire, state/utility programs become critical
4. **Existing tools have gaps:**
   - DSIRE: Database format, not personalized
   - Rewiring America: Consumer-only, rolling state coverage
   - EnergySage: Solar-focused marketplace
5. **Our moat:** Utility and local program coverage nobody else has
6. **Mission-aligned business** - Make money while accelerating climate action

### Target Users

**Homeowners:**
| Persona | Trigger | Needs |
|---------|---------|-------|
| **Upgrader** | "Time for a new HVAC" | What incentives exist for heat pumps? |
| **Bill Payer** | "Electric bills too high" | What can I do that pays for itself? |
| **Climate Conscious** | "Want to electrify my home" | Complete picture of all incentives |
| **First-Time Buyer** | "Just bought a house" | What should I do first? |

**Contractors (Solar, HVAC, Electrical):**
| Persona | Pain Point | Needs |
|---------|------------|-------|
| **Sales Rep** | "Hard to explain all the incentives" | Customer-facing presentation mode |
| **Owner** | "Which leads are worth pursuing?" | Lead qualification with incentive data |
| **Estimator** | "Incentives change constantly" | Auto-updated incentive database |

### Key Differentiators

| Existing Solutions | GreenBack |
|-------------------|-----------|
| Consumer calculators only | Consumer + Contractor ecosystem |
| Federal/major state focus | Utility and local program coverage (the moat) |
| Static incentive lists | Real-time fund availability |
| Separate from sales workflow | Integrated contractor dashboard |
| Post-2025 uncertainty | Built for state/utility-dominant future |

---

## 3. Revenue Model

### Stream 1: Lead Generation (Primary - 60%)

| Metric | Value |
|--------|-------|
| Lead type | Exclusive, pre-qualified |
| Price per lead | $100-200 (solar), $50-100 (HVAC) |
| Quality signal | User has seen their incentives, expressed intent |
| Expected conversion | 15-20% (vs 5-8% industry average) |

**Why our leads are better:**
- User already knows their incentive picture
- Educated buyers close faster
- Pre-qualified by income, property type, location

### Stream 2: Contractor SaaS (Secondary - 30%)

| Tier | Price | Features |
|------|-------|----------|
| **Free** | $0 | View incentives for your service area |
| **Pro** | $79/mo | Customer presentation mode, pipeline integration, priority leads |
| **Team** | $199/mo | Multi-user, CRM integration, white-label reports |

**Flywheel:**
- Contractors who pay for SaaS get first access to leads
- Better close rates → more SaaS subscribers
- More subscribers → more leads → more homeowners

### Stream 3: Financing Referrals (Tertiary - 10%)

| Partner Type | Referral Fee |
|--------------|--------------|
| POS financing (GreenSky, FinMkt) | 0.5-1% of loan |
| PACE financing | Varies by provider |
| Equipment manufacturers | Potential co-marketing |

---

## 4. Data Strategy

### Hybrid Approach

**Layer 1: Rewiring America API (Federal + Major State)**
- Free, updated weekly
- Covers federal tax credits and major state rebates
- Rolling coverage of HOMES/HEAR programs
- Don't reinvent this wheel

**Layer 2: Our Utility Database (The Moat)**
- DSIRE only tracks utilities with 30,000+ customers
- Thousands of smaller utilities offer rebates
- Manual + AI-assisted data collection
- Start with top 200 utilities, expand systematically

**Layer 3: Local Program Database**
- DSIRE only has ~250 local programs
- Tens of thousands of local governments have programs
- Focus on major metros first (50 largest cities)
- Crowdsource: Let contractors report programs we're missing

**Layer 4: Real-Time Enhancements**
- Fund availability status (many programs run out)
- Wait times for rebate processing
- Contractor reviews/ratings (future)

### Maintenance Strategy

| Data Type | Update Frequency | Method |
|-----------|-----------------|--------|
| Federal (via RA API) | Weekly (automatic) | API pull |
| State (via RA API) | Weekly (automatic) | API pull |
| Utility programs | Monthly | Manual + AI review |
| Local programs | Quarterly | Manual + crowdsource |
| Fund availability | Weekly | Scrape + manual verification |

---

## 5. Technical Architecture

### Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| **Framework** | SvelteKit | Fast, SSR + client, consistent with Summit58 |
| **Database** | Supabase (Postgres) | Auth, DB, RLS, familiar |
| **Hosting** | Railway | Familiar, scalable |
| **External API** | Rewiring America | Federal/state incentive data |
| **Analytics** | Plausible | Privacy-focused |
| **Payments** | Stripe | Contractor subscriptions + lead purchases |
| **Email** | Resend or Postmark | Transactional + lead notifications |

### Project Structure

```
greenback/
├── src/
│   ├── lib/
│   │   ├── components/
│   │   │   ├── Calculator/
│   │   │   │   ├── StepZipCode.svelte
│   │   │   │   ├── StepIncome.svelte
│   │   │   │   ├── StepHomeType.svelte
│   │   │   │   └── StepGoals.svelte
│   │   │   ├── Results/
│   │   │   │   ├── IncentiveCard.svelte
│   │   │   │   ├── IncentiveList.svelte
│   │   │   │   └── TotalSavings.svelte
│   │   │   ├── Contractor/
│   │   │   │   ├── Dashboard.svelte
│   │   │   │   ├── LeadCard.svelte
│   │   │   │   └── PresentationMode.svelte
│   │   │   └── common/
│   │   │       ├── Button.svelte
│   │   │       └── Card.svelte
│   │   ├── server/
│   │   │   ├── supabase.ts
│   │   │   ├── rewiring-america.ts
│   │   │   ├── incentives.ts
│   │   │   └── stripe.ts
│   │   └── utils/
│   │       ├── income.ts        # AMI calculations
│   │       └── eligibility.ts   # Incentive matching logic
│   ├── routes/
│   │   ├── +page.svelte                    # Homepage
│   │   ├── +layout.svelte                  # App shell
│   │   ├── calculator/
│   │   │   └── +page.svelte                # Multi-step calculator
│   │   ├── results/
│   │   │   └── +page.svelte                # Personalized results
│   │   ├── incentive/[id]/
│   │   │   └── +page.svelte                # Incentive detail
│   │   ├── get-quotes/
│   │   │   └── +page.svelte                # Connect with contractors
│   │   ├── contractors/
│   │   │   ├── +page.svelte                # Contractor landing
│   │   │   ├── signup/+page.svelte         # Registration
│   │   │   ├── dashboard/+page.svelte      # Main dashboard
│   │   │   ├── leads/+page.svelte          # Lead management
│   │   │   └── present/[id]/+page.svelte   # Presentation mode
│   │   ├── pricing/
│   │   │   └── +page.svelte                # Subscription tiers
│   │   ├── about/
│   │   │   └── +page.svelte                # Mission, methodology
│   │   └── api/
│   │       ├── incentives/+server.ts       # Incentive lookup
│   │       ├── leads/+server.ts            # Lead management
│   │       └── webhooks/stripe/+server.ts  # Subscription webhooks
│   ├── app.html
│   └── app.css
├── supabase/
│   └── migrations/
├── static/
│   └── images/
├── svelte.config.js
├── tailwind.config.js
└── package.json
```

### Database Schema

```sql
-- Users (homeowners and contractors)
CREATE TABLE profiles (
  id UUID PRIMARY KEY REFERENCES auth.users(id),
  type TEXT CHECK (type IN ('homeowner', 'contractor')),
  email TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Homeowner profiles
CREATE TABLE homeowner_profiles (
  id UUID PRIMARY KEY REFERENCES profiles(id),
  zip_code TEXT,
  income_bracket TEXT, -- 'under_80_ami', '80_to_150_ami', 'over_150_ami'
  home_type TEXT, -- 'single_family', 'multifamily', 'manufactured'
  ownership TEXT, -- 'owner', 'renter'
  utility_electric TEXT,
  utility_gas TEXT
);

-- Contractor profiles
CREATE TABLE contractor_profiles (
  id UUID PRIMARY KEY REFERENCES profiles(id),
  company_name TEXT NOT NULL,
  service_types TEXT[], -- ['solar', 'hvac', 'electrical']
  service_zips TEXT[], -- Zip codes they serve
  subscription_tier TEXT DEFAULT 'free',
  stripe_customer_id TEXT
);

-- Our utility program database (the moat)
CREATE TABLE utility_programs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  utility_name TEXT NOT NULL,
  utility_id TEXT, -- EIA ID or similar
  state TEXT NOT NULL,
  service_zips TEXT[],
  program_name TEXT NOT NULL,
  program_type TEXT, -- 'rebate', 'credit', 'financing'
  technology TEXT[], -- ['heat_pump', 'solar', 'ev_charger']
  amount TEXT, -- "$500" or "30% up to $2000"
  requirements TEXT,
  url TEXT,
  status TEXT DEFAULT 'active',
  last_verified TIMESTAMPTZ,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Local government programs
CREATE TABLE local_programs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  locality_name TEXT NOT NULL, -- City or county name
  state TEXT NOT NULL,
  program_name TEXT NOT NULL,
  technology TEXT[],
  amount TEXT,
  requirements TEXT,
  url TEXT,
  status TEXT DEFAULT 'active',
  last_verified TIMESTAMPTZ,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Lead tracking
CREATE TABLE leads (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  homeowner_id UUID REFERENCES homeowner_profiles(id),
  contractor_id UUID REFERENCES contractor_profiles(id),
  project_type TEXT NOT NULL, -- 'solar', 'heat_pump', etc.
  incentive_total INTEGER, -- Estimated total incentives
  status TEXT DEFAULT 'new', -- 'new', 'contacted', 'quoted', 'closed', 'lost'
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Saved incentive searches
CREATE TABLE saved_searches (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  homeowner_id UUID REFERENCES homeowner_profiles(id),
  search_params JSONB,
  results_snapshot JSONB,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Indexes
CREATE INDEX idx_utility_programs_state ON utility_programs(state);
CREATE INDEX idx_utility_programs_status ON utility_programs(status);
CREATE INDEX idx_leads_contractor ON leads(contractor_id);
CREATE INDEX idx_leads_status ON leads(status);
CREATE INDEX idx_contractor_service_zips ON contractor_profiles USING GIN(service_zips);
```

### URL Structure

```
greenback.com/
├── /                           # Homepage + calculator entry
├── /calculator                 # Multi-step incentive calculator
├── /results                    # Personalized incentive results
├── /incentive/[id]             # Individual incentive detail
├── /get-quotes                 # Connect with contractors
├── /contractors
│   ├── /contractors/signup     # Contractor registration
│   ├── /contractors/dashboard  # Contractor dashboard
│   ├── /contractors/leads      # Lead management
│   └── /contractors/present/[id] # Customer presentation mode
├── /pricing                    # Contractor subscription tiers
├── /about                      # Mission, methodology
└── /api/
    ├── /api/incentives         # Incentive lookup
    ├── /api/leads              # Lead management
    └── /api/webhooks/stripe    # Subscription webhooks
```

---

## 6. Implementation Plan

### Phase 1: MVP Calculator (Foundation)

**Goal:** Working homeowner calculator that shows federal + state incentives via Rewiring America API.

**Deliverables:**
- [ ] Initialize SvelteKit project with Tailwind
- [ ] Set up Supabase project
- [ ] Build multi-step calculator UI (zip, income, home type, goals)
- [ ] Integrate Rewiring America API
- [ ] Display personalized results page
- [ ] Basic SEO (meta tags, OG images)
- [ ] Deploy to Railway
- [ ] Landing page explaining value prop

**Exit Criteria:** User can enter info, see their federal + state incentives, share results.

### Phase 2: Utility Database (The Moat)

**Goal:** Add utility-specific incentives that RA API doesn't cover.

**Deliverables:**
- [ ] Research and document top 50 utilities with programs
- [ ] Build utility_programs table and admin interface
- [ ] Create utility lookup by zip code (EIA data or similar)
- [ ] Integrate utility incentives into results
- [ ] Build data verification workflow
- [ ] Add "report missing program" feature

**Exit Criteria:** Results include utility-specific incentives for top 50 utilities.

### Phase 3: Lead Generation

**Goal:** Connect homeowners with contractors, monetize.

**Deliverables:**
- [ ] Build "Get Quotes" flow
- [ ] Contractor signup and profile
- [ ] Lead delivery system (email + dashboard)
- [ ] Lead status tracking
- [ ] Stripe integration for lead purchase
- [ ] Contractor matching algorithm (by zip, service type)

**Exit Criteria:** Homeowners can request quotes, contractors receive and pay for leads.

### Phase 4: Contractor SaaS

**Goal:** Subscription product for contractors.

**Deliverables:**
- [ ] Contractor dashboard with pipeline view
- [ ] Customer presentation mode (shareable incentive report)
- [ ] Subscription tiers (Free/Pro/Team)
- [ ] Stripe subscription billing
- [ ] Priority lead access for paid tiers
- [ ] Basic analytics (lead conversion tracking)

**Exit Criteria:** Contractors can subscribe, access premium features, receive priority leads.

### Phase 5: Scale & Polish

**Goal:** Expand coverage, improve conversion.

**Deliverables:**
- [ ] Expand utility coverage to 200+ utilities
- [ ] Add local program database (50 largest cities)
- [ ] Email nurture sequences
- [ ] Contractor reviews/ratings
- [ ] A/B testing on calculator flow
- [ ] SEO content (blog, incentive guides by state)
- [ ] Consider mobile app / PWA

**Exit Criteria:** Comprehensive coverage, sustainable lead flow, positive unit economics.

---

## 7. Competitive Landscape

### vs. Rewiring America Calculator

| They Have | We Add |
|-----------|--------|
| Federal + major state incentives | Utility and local programs |
| Consumer-only focus | Contractor ecosystem |
| Informational | Transactional (connect to installers) |
| Non-profit mission | Sustainable business model |

**Coexistence strategy:** We USE their API. Not competitors, complementary.

### vs. EnergySage

| They Have | We Add |
|-----------|--------|
| Solar-focused | Full electrification (HVAC, EV, etc.) |
| Marketplace model | Incentive-first discovery |
| Acquired by Schneider Electric | Indie, nimble |
| Well-funded | Lean, focused |

**Differentiation:** They're a solar marketplace. We're an incentive finder that happens to connect you with installers.

### vs. DSIRE

| They Have | We Add |
|-----------|--------|
| Comprehensive database | Personalized results |
| Academic/policy focus | Consumer UX |
| Database format | Calculator format |
| Static | Real-time fund availability |

**Relationship:** They're a data source. We're a consumer product.

---

## 8. Key Integrations

### Rewiring America API

```typescript
// Example API call
const response = await fetch('https://api.rewiringamerica.org/api/v1/calculator', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${RA_API_KEY}`
  },
  body: JSON.stringify({
    zip: '80202',
    owner_status: 'homeowner',
    household_income: 80000,
    tax_filing: 'joint',
    household_size: 4
  })
});

// Response includes federal tax credits, state rebates
const incentives = await response.json();
```

### Utility Lookup (EIA or similar)

```typescript
// Map zip code to utility
async function getUtilitiesByZip(zip: string): Promise<Utility[]> {
  // Option 1: EIA API
  // Option 2: Pre-built zip-to-utility mapping
  // Option 3: OpenEI utility rate database
}
```

### Stripe Integration

```typescript
// Lead purchase
const paymentIntent = await stripe.paymentIntents.create({
  amount: 15000, // $150 per lead
  currency: 'usd',
  customer: contractor.stripe_customer_id,
  metadata: {
    lead_id: lead.id,
    contractor_id: contractor.id
  }
});

// Subscription
const subscription = await stripe.subscriptions.create({
  customer: contractor.stripe_customer_id,
  items: [{ price: 'price_pro_monthly' }]
});
```

---

## 9. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Federal programs end Dec 2025 | Certain | High | Built for state/utility focus post-2025 |
| Rewiring America API changes | Medium | High | Abstract API layer, can switch sources |
| State programs get paused | Medium | Medium | Diversified coverage, real-time status |
| EnergySage dominates | Medium | Medium | Different positioning (incentive-first) |
| Data maintenance burden | High | Medium | Hybrid approach, crowdsourcing |
| Low contractor adoption | Medium | High | Prove lead quality first, SaaS second |

---

## 10. Success Metrics

| Phase | Metric | Target |
|-------|--------|--------|
| MVP | Calculator completions | 1,000/month |
| MVP | Time on results page | >2 minutes |
| Lead Gen | Lead requests | 100/month |
| Lead Gen | Lead close rate | 15%+ |
| SaaS | Contractor signups | 50 |
| SaaS | Paid subscribers | 10 |
| Scale | Monthly revenue | $5K |

---

## 11. Passivity Analysis

| Factor | Score | Notes |
|--------|-------|-------|
| **Content Freshness** | 4/10 | Incentives change frequently, especially state/utility |
| **Maintenance** | 4/10 | Data updates, API changes, fund tracking |
| **Support Burden** | 5/10 | Contractors may need support, lead disputes |
| **Scaling** | 8/10 | Platform scales with more data/contractors |
| **Technical** | 5/10 | Backend requires monitoring, API integrations |

**Overall Passivity Score: 5/10**

This is intentionally NOT a passive project. It's a higher-effort, higher-reward business that:
- Requires ongoing data maintenance
- Has real customers (contractors) who need support
- Involves payments and lead quality disputes
- Needs continuous improvement

**Trade-off:** Lower passivity, but higher revenue ceiling ($5-10K/month vs $1-2K), more defensible moat, and mission-aligned work.

---

## 12. AI Agent Instructions

### Do
- Use Rewiring America API for federal/state data (don't rebuild)
- Focus on UX - calculator should feel fast and helpful
- Make results shareable (social proof, word of mouth)
- Track incentive eligibility carefully (income brackets, property types)
- Abstract external APIs behind internal service layer
- Use SvelteKit conventions (load functions, form actions)
- Consider mobile experience (many users will be on phone)

### Don't
- Over-engineer Phase 1 - get the calculator working first
- Build contractor features before validating homeowner demand
- Assume incentives are static - build for change
- Ignore the post-2025 transition - federal credits are ending
- Copy incentive text verbatim (write original summaries)
- Forget affiliate disclosures where required

### Decisions Already Made
- SvelteKit over Next.js (consistent with Summit58, lighter)
- Supabase over custom backend (familiar, all-in-one)
- Railway over Vercel (familiar, more control)
- Rewiring America API for core data (free, maintained)
- Build own utility database (the moat)
- Lead gen first, SaaS second (prove value before subscription)

### Open Questions
- Which financing partners to prioritize?
- How to handle contractor verification/vetting?
- Email provider: Resend vs Postmark?
- A/B testing framework for calculator optimization?

### Common Pitfalls to Avoid

1. **Don't ignore income verification** - State rebates depend heavily on AMI brackets
2. **Don't assume nationwide coverage immediately** - Roll out state-by-state
3. **Don't skip real-time fund checking** - Programs run out, causes user frustration
4. **Don't underestimate contractor sales cycle** - They're skeptical of lead quality

---

## 13. Session Log

### 2025-12-18 - Project Created
- Identified climate incentives as high-value opportunity
- Researched competitive landscape (DSIRE, Rewiring America, EnergySage)
- Decided on hybrid data strategy (RA API + own utility/local database)
- Chose dual-sided model (homeowners + contractors)
- Named project GreenBack - "Get your green back"
- Confirmed SvelteKit + Supabase + Railway stack
- Created comprehensive session-start document
- Defined 5-phase implementation plan

---

## 14. Quick Reference

### Commands
```bash
# Development
npm run dev

# Build
npm run build

# Preview production
npm run preview

# Supabase
supabase start        # Local dev
supabase db push      # Push migrations
supabase gen types    # Generate TypeScript types
```

### Key Links
- Rewiring America API: https://api.rewiringamerica.org/docs
- Rewiring America API Signup: https://rewiring.link/api-signup
- DSIRE Database: https://www.dsireusa.org/
- EIA Utility Data: https://www.eia.gov/electricity/data/eia861/
- SvelteKit Docs: https://kit.svelte.dev/docs
- Supabase Docs: https://supabase.com/docs
- Stripe Docs: https://stripe.com/docs

### Environment Variables
```
PUBLIC_SUPABASE_URL=
PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
REWIRING_AMERICA_API_KEY=
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
```

---

**Next Action:** Create greenback repo and begin Phase 1 (MVP Calculator)

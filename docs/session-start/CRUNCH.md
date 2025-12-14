# CRUNCH - Session Start Document

> **Last Updated**: 2025-12-13
> **Current Phase**: Pre-Development (Planning Complete)
> **Project Repo**: Not yet created
> **Project Name**: Crunch
> **Tagline**: "Crunch the numbers"

---

## 1. Quick Context

**What**: A network of 20-50 highly specific, interconnected calculators targeting long-tail SEO keywords.

**Revenue Model**: Display ads (primary) + affiliate links + lead gen

**Why This Will Work**: Calculator queries have high search intent, zero customer support burden, content doesn't go stale, and can be built once then left alone.

**Target Revenue**: $1-5K/month passive income

**Passivity Score**: 10/10 - Most passive option evaluated

---

## 2. Full Project Vision

### What We're Building

A collection of niche calculators that each solve one specific problem extremely well. Unlike generic calculator sites, we target underserved niches where:
- Search volume exists (500-5000 monthly searches)
- Competition is low (no dominant tools)
- User intent is high (people actively solving problems)

### Why It Will Succeed

1. **SEO Fundamentals**: Each calculator = dedicated page = SEO entry point
2. **High Intent Traffic**: People searching for calculators are trying to make decisions
3. **Zero Support**: No accounts, no subscriptions, no customer service
4. **Evergreen**: Calculators don't go "stale" like blog content
5. **Compounding**: Internal linking between related calculators builds domain authority
6. **Embeddable**: Free embed widgets = backlinks and distribution

### Target Users

- Freelancers calculating taxes/rates
- Side hustlers evaluating opportunities
- Content creators estimating revenue
- FIRE/personal finance enthusiasts
- Gig economy workers (Uber, Airbnb, etc.)

### Key Differentiators

1. **Interconnected Network**: Not isolated tools, but a linked ecosystem
2. **Niche Focus**: "YouTube AdSense calculator" not "calculator"
3. **Modern UX**: Fast, mobile-first, shareable results
4. **Embed-First**: Every calculator can be embedded on other sites

### Success Metrics

| Metric | 6 Month Goal | 12 Month Goal |
|--------|--------------|---------------|
| Calculators Live | 20 | 50 |
| Monthly Pageviews | 30K-50K | 100K-200K |
| Monthly Revenue | $500-1,000 | $2,000-5,000 |
| Domain Authority | 15-20 | 25-35 |

---

## 3. Technical Architecture

### Stack Decisions (FINAL - Do Not Re-evaluate)

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Framework | **Astro** | SSG for max performance, great SEO, islands for interactivity |
| Styling | **Tailwind CSS** | Rapid development, small bundle |
| Hosting | **Cloudflare Pages** | Free tier generous, edge performance, no cold starts |
| Analytics | **Plausible** | Privacy-focused, simple, no cookie banner needed |
| Ads | **Google AdSense** → Mediavine | Start with AdSense, graduate to Mediavine at 50K sessions |

### Why Astro Over Next.js

- Calculators are mostly static with small interactive islands
- Better Core Web Vitals out of the box
- Simpler mental model for this use case
- No server needed = cheaper hosting

### Data Model

No database needed for MVP. Each calculator is self-contained.

```
Calculator Page:
├── Static content (title, description, SEO)
├── Interactive calculator component (client-side JS)
├── Result sharing (URL params encode state)
├── Embed code generator
└── Related calculators (internal links)
```

### URL Structure

```
crunch.tools/   (or getcrunch.com, crunch.fyi)
├── /                           # Homepage with category grid
├── /freelance/                 # Category landing
│   ├── /freelance/tax-calculator
│   ├── /freelance/rate-calculator
│   └── /freelance/w2-vs-1099
├── /creator/
│   ├── /creator/youtube-adsense
│   ├── /creator/twitch-revenue
│   └── /creator/patreon-calculator
├── /gig-economy/
│   ├── /gig-economy/uber-earnings
│   ├── /gig-economy/airbnb-profit
│   └── /gig-economy/doordash-earnings
└── /personal-finance/
    ├── /personal-finance/fire-calculator
    ├── /personal-finance/emergency-fund
    └── /personal-finance/subscription-audit
```

### SEO Architecture

Each calculator page includes:
- Unique title: "[Calculator Name] - Free [Use Case] Calculator"
- Meta description with target keyword
- Schema.org WebApplication markup
- FAQ schema for featured snippets
- Open Graph tags for social sharing
- Canonical URL

### Embed System

```html
<!-- Embed code structure -->
<iframe
  src="https://crunch.tools/embed/freelance/tax-calculator?theme=light"
  width="100%"
  height="400"
  frameborder="0"
></iframe>
```

---

## 4. Implementation Plan

### Phase 1: Foundation (Week 1-2) ← START HERE

**Deliverables:**
- [ ] Astro project setup with Tailwind
- [ ] Base calculator component template
- [ ] Homepage with category navigation
- [ ] SEO utilities (meta tags, schema, sitemap)
- [ ] Analytics integration (Plausible)
- [ ] 3 pilot calculators:
  - Freelancer hourly rate calculator
  - YouTube AdSense estimator
  - Side hustle time-to-goal calculator

**Definition of Done:**
- Site deploys to Cloudflare Pages
- All 3 calculators functional
- Lighthouse scores 90+ across the board
- Sitemap submitted to Google Search Console

### Phase 2: Core Calculators (Week 3-4)

**Deliverables:**
- [ ] 12 more calculators (15 total):
  - Freelance: Quarterly tax, W2 vs 1099, Project rate
  - Creator: Twitch revenue, Etsy fees, Patreon earnings
  - Gig Economy: Uber net earnings, Airbnb profit, DoorDash
  - Personal Finance: FIRE runway, Emergency fund, Rent vs Buy
- [ ] Category landing pages with internal linking
- [ ] Embed functionality for all calculators
- [ ] Social sharing with pre-filled results

**Definition of Done:**
- 15 calculators live
- Internal linking structure complete
- Embed codes functional

### Phase 3: Monetization Setup (Week 5)

**Deliverables:**
- [ ] Google AdSense application and setup
- [ ] Ad placement optimization (sidebar, below results)
- [ ] Affiliate links where relevant:
  - Tax calculator → TurboTax affiliate
  - Freelance tools → FreshBooks/Wave
  - Investment calculators → brokerage affiliates
- [ ] Lead gen opt-in for high-value calculators

**Definition of Done:**
- Ads displaying
- Affiliate links placed
- Revenue tracking in place

### Phase 4: Scale (Week 6+)

**Deliverables:**
- [ ] Expand to 30+ calculators
- [ ] Programmatic SEO variations (by state, by country)
- [ ] Guest post outreach for backlinks
- [ ] Monitor and optimize based on traffic data

---

## 5. Critical Files Reference

Once project is created, these will be the key files:

```
crunch/
├── src/
│   ├── components/
│   │   ├── Calculator.astro      # Base calculator template
│   │   ├── CalculatorInput.tsx   # React input component
│   │   ├── CalculatorResult.tsx  # React result display
│   │   ├── EmbedCode.astro       # Embed code generator
│   │   └── RelatedCalcs.astro    # Internal linking component
│   ├── layouts/
│   │   ├── BaseLayout.astro      # Site-wide layout
│   │   └── CalculatorLayout.astro # Calculator page layout
│   ├── pages/
│   │   ├── index.astro           # Homepage
│   │   ├── [category]/
│   │   │   └── [calculator].astro # Dynamic calculator pages
│   │   └── embed/
│   │       └── [...path].astro   # Embed routes
│   └── lib/
│       ├── calculators/          # Calculator logic files
│       │   ├── freelance-tax.ts
│       │   ├── youtube-adsense.ts
│       │   └── ...
│       ├── seo.ts                # SEO utilities
│       └── analytics.ts          # Analytics helpers
├── public/
│   └── og-images/               # Social share images
├── astro.config.mjs
├── tailwind.config.js
└── package.json
```

---

## 6. Context for AI Agents

### Instructions for New Sessions

1. **Read this entire document first** before taking any action
2. **Check the project-tracker.md** in the interstellar repo for current status
3. **Do not re-debate decided decisions** (stack, architecture, etc.)
4. **Focus on the current phase** deliverables
5. **Update this document** at session end with progress

### Decisions Already Made (DO NOT CHANGE)

- Stack: Astro + Tailwind + Cloudflare Pages
- No database for MVP
- AdSense first, then Mediavine
- URL structure as defined above
- Embed system approach

### Open Questions (Can Still Decide)

- Specific calculator list prioritization
- Exact affiliate programs to join
- Email capture strategy (if any)
- Social media presence (if any)

### Common Pitfalls to Avoid

1. **Don't over-engineer**: Each calculator should be simple
2. **Don't add auth**: No user accounts needed
3. **Don't add a database**: URL params for state sharing
4. **Don't build a CMS**: Hardcoded content is fine
5. **Don't optimize prematurely**: Ship calculators, then optimize

### Useful Commands

```bash
# Start development
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Deploy to Cloudflare
npm run deploy
```

---

## 7. Session Log

### 2025-12-13 - Initial Planning Session
- Completed full ideation and research in interstellar HQ
- Chose Calculator Network as primary project
- Named project "Crunch"
- Created this session-start document
- Next: Create crunch repo and begin Phase 1

---

## Appendix: Calculator Ideas Backlog

### Priority 1 (Build First)
1. Freelancer hourly rate calculator
2. YouTube AdSense revenue estimator
3. Side hustle time-to-goal calculator
4. Freelancer quarterly tax estimator
5. W2 vs 1099 comparison calculator

### Priority 2
6. Etsy seller fee calculator
7. Twitch subscriber revenue calculator
8. Patreon take-home calculator
9. Uber/Lyft net earnings calculator
10. Airbnb profit calculator

### Priority 3
11. FIRE (Financial Independence) runway
12. Emergency fund calculator
13. Rent vs Buy calculator
14. Subscription audit/savings calculator
15. DoorDash earnings calculator

### Future Ideas
- 3D printing cost calculator
- Homebrewing cost-per-beer
- Photography gear ROI
- Podcast hosting cost comparison
- Newsletter revenue estimator
- Freelancer project quote generator
- Contractor benefits calculator
- Stock option value calculator
- Crypto tax estimator
- Solar panel ROI calculator

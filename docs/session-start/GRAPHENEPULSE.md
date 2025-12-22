# Graphene Pulse - Session Start Document

> **Read this first.** This document contains everything needed to start a productive session on Graphene Pulse.

---

## 1. Quick Context

| Field | Value |
|-------|-------|
| **Project** | Graphene Pulse |
| **Tagline** | "The pulse of the graphene industry" |
| **What** | AI-powered news aggregation + beautiful wiki for the graphene industry |
| **Stack** | Astro + Tailwind + Supabase + Railway |
| **Revenue** | Newsletter sponsorships, premium tier, display ads |
| **Target** | $2-5K/month |
| **Status** | In Development |
| **Repo** | [github.com/BenTyson/pulse](https://github.com/BenTyson/pulse) |

---

## 2. Full Vision

### What is Graphene Pulse?

Graphene Pulse is the premiere news aggregation and knowledge hub for the graphene industry. We serve researchers, investors, engineers, executives, and curious minds with automated, beautifully curated content.

Think of it as **TechCrunch meets Wikipedia for graphene** - authoritative but accessible, beautiful but substantive, automated but high-quality.

**Core components:**
1. **Automated News Aggregation** - AI-powered pipeline scrapes, filters, classifies, and summarizes graphene news from dozens of sources
2. **Beautiful Wiki** - Not a traditional ugly wiki, but a magazine-quality knowledge base covering graphene properties, applications, companies, and history
3. **Weekly Newsletter** - "Graphene Weekly" curated digest with top stories and deep dives
4. **Company Directory** - Database of graphene manufacturers, startups, and research labs

### Why This Will Work

1. **Massive market potential** - $200M (2023) → $1.5B+ (2030), thousands of patents annually
2. **Content gap is real** - Graphene-Info is dated and cluttered, Graphene Council is gated, academic journals are paywalled
3. **Diverse audience** - Researchers, investors, engineers, students all searching for graphene info
4. **Automation advantage** - AI-powered pipeline means content at scale with minimal intervention
5. **UI/UX as differentiator** - Stunning design where competitors look like 2005

### Target Users

| Audience | What They Want | How We Serve |
|----------|---------------|--------------|
| **Researchers/Scientists** | Latest papers, breakthroughs, funding | Research news, paper summaries, grant announcements |
| **Investors** | Market trends, company news, IPOs | Investment section, company profiles, funding rounds |
| **Engineers/Developers** | Applications, products, how-to | Application guides, product news, technical wiki |
| **Executives/Industry** | Market intel, partnerships, regulations | Industry news, partnership announcements, policy updates |
| **Curious Public** | "What is graphene?", cool applications | Wiki, explainers, "wow factor" stories |
| **Students** | Learning, career, research opportunities | Educational wiki, university news, career section |

### Differentiators

| Graphene Pulse | Competitors |
|----------------|-------------|
| Beautiful, modern design (dark mode, silver accents) | Dated 2010s layouts |
| AI-powered automation | Manual curation only |
| Open access, free | Membership-gated (Graphene Council) |
| Clean, scannable UX | Cluttered, slow, ad-heavy |
| Newsletter digest | No email outreach |
| Company directory | Limited company info |

### Success Metrics

| Metric | 6 Month Goal | 12 Month Goal |
|--------|--------------|---------------|
| Monthly Visitors | 10K | 50K |
| Newsletter Subscribers | 500 | 2,500 |
| Articles Published | 500+ | 2,000+ |
| Newsletter Sponsors | 1 | 3-5 |

---

## 3. Technical Architecture

### Stack Decisions (FINAL - Do Not Re-evaluate)

| Layer | Choice | Rationale |
|-------|--------|-----------|
| **Framework** | Astro | SSG/SSR hybrid, perfect for content sites, fast |
| **Styling** | Tailwind CSS | Consistent with portfolio, rapid development |
| **Database** | Supabase (Postgres) | Articles, sources, wiki, subscribers |
| **Hosting** | Railway | Familiar, scalable, good for background jobs |
| **Scraping** | Node.js + Cheerio + Playwright | RSS, HTML, and JS-rendered sites |
| **AI Processing** | Claude API | Classification, summarization, relevance scoring |
| **Search** | Meilisearch | Fast full-text, self-hosted, cost-effective |
| **Newsletter** | Buttondown | Simple API, good for automated sends |
| **Analytics** | Plausible | Privacy-focused |
| **Job Queue** | BullMQ + Redis | Scheduled scraping and processing |

### Scraping Pipeline

```
┌─────────────────────────────────────────────────────────────┐
│                     SCRAPING PIPELINE                        │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐              │
│  │  Sources │───▶│ Scrapers │───▶│ Raw Feed │              │
│  │  Config  │    │ (scheduled)   │  (Queue) │              │
│  └──────────┘    └──────────┘    └──────────┘              │
│                                        │                    │
│                                        ▼                    │
│                              ┌──────────────┐               │
│                              │ AI Processor │               │
│                              │ - Relevance  │               │
│                              │ - Classify   │               │
│                              │ - Summarize  │               │
│                              │ - Dedupe     │               │
│                              └──────────────┘               │
│                                        │                    │
│                                        ▼                    │
│                              ┌──────────────┐               │
│                              │  Published   │               │
│                              │   Articles   │               │
│                              └──────────────┘               │
│                                        │                    │
│                         ┌──────────────┼──────────────┐     │
│                         ▼              ▼              ▼     │
│                    ┌────────┐    ┌──────────┐   ┌────────┐  │
│                    │  Site  │    │Newsletter│   │  RSS   │  │
│                    └────────┘    └──────────┘   └────────┘  │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Database Schema

```sql
-- News sources to scrape
CREATE TABLE sources (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  url TEXT NOT NULL,
  feed_url TEXT,              -- RSS feed if available
  scrape_type TEXT,           -- 'rss', 'html', 'api'
  scrape_config JSONB,        -- Selectors, pagination, etc.
  scrape_frequency TEXT,      -- 'hourly', 'daily'
  is_active BOOLEAN DEFAULT true,
  last_scraped_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Raw scraped items (before processing)
CREATE TABLE raw_items (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  source_id UUID REFERENCES sources(id),
  external_id TEXT,           -- URL or unique ID from source
  title TEXT NOT NULL,
  content TEXT,
  url TEXT NOT NULL,
  published_at TIMESTAMPTZ,
  scraped_at TIMESTAMPTZ DEFAULT NOW(),
  processed BOOLEAN DEFAULT false,
  UNIQUE(source_id, external_id)
);

-- Processed/published articles
CREATE TABLE articles (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  raw_item_id UUID REFERENCES raw_items(id),

  -- Content
  title TEXT NOT NULL,
  slug TEXT UNIQUE NOT NULL,
  summary TEXT,               -- AI-generated summary
  content TEXT,               -- Full content or excerpt

  -- Metadata
  source_id UUID REFERENCES sources(id),
  source_url TEXT NOT NULL,
  author TEXT,
  published_at TIMESTAMPTZ,

  -- AI-generated
  category TEXT,              -- 'research', 'business', 'product', 'investment'
  subcategory TEXT,           -- 'batteries', 'electronics', etc.
  importance_score INTEGER,   -- 1-10 for ranking
  tags TEXT[],

  -- Status
  status TEXT DEFAULT 'published',
  featured BOOLEAN DEFAULT false,

  -- Engagement
  view_count INTEGER DEFAULT 0,

  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Wiki pages
CREATE TABLE wiki_pages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug TEXT UNIQUE NOT NULL,
  title TEXT NOT NULL,
  content TEXT NOT NULL,      -- Markdown
  parent_slug TEXT,           -- For hierarchy
  display_order INTEGER,
  meta_description TEXT,
  status TEXT DEFAULT 'published',
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Companies directory
CREATE TABLE companies (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  slug TEXT UNIQUE NOT NULL,
  description TEXT,
  logo_url TEXT,
  website TEXT,
  company_type TEXT,          -- 'manufacturer', 'startup', 'research'
  focus_areas TEXT[],         -- ['batteries', 'composites']
  founded_year INTEGER,
  headquarters TEXT,
  employee_count TEXT,
  funding_total TEXT,
  funding_stage TEXT,
  twitter TEXT,
  linkedin TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Newsletter subscribers
CREATE TABLE subscribers (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email TEXT UNIQUE NOT NULL,
  frequency TEXT DEFAULT 'weekly',
  subscribed_at TIMESTAMPTZ DEFAULT NOW(),
  confirmed BOOLEAN DEFAULT false,
  unsubscribed_at TIMESTAMPTZ
);

-- Newsletter issues
CREATE TABLE newsletter_issues (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  subject TEXT NOT NULL,
  content TEXT NOT NULL,
  article_ids UUID[],
  sent_at TIMESTAMPTZ,
  open_count INTEGER DEFAULT 0,
  click_count INTEGER DEFAULT 0,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Indexes
CREATE INDEX idx_articles_category ON articles(category);
CREATE INDEX idx_articles_published ON articles(published_at DESC);
CREATE INDEX idx_articles_status ON articles(status);
CREATE INDEX idx_raw_items_processed ON raw_items(processed);
CREATE INDEX idx_wiki_parent ON wiki_pages(parent_slug);
```

### URL Structure

```
graphenepulse.com/
├── /                           # Homepage (latest news + featured)
├── /news                       # All news (paginated, filterable)
├── /news/[slug]                # Individual article
├── /category/[category]        # News by category
│   ├── /category/research
│   ├── /category/business
│   ├── /category/products
│   └── /category/investment
├── /wiki                       # Wiki homepage
├── /wiki/[...slug]             # Wiki pages (nested)
│   ├── /wiki/what-is-graphene
│   ├── /wiki/properties/electrical
│   ├── /wiki/applications/batteries
│   └── ...
├── /companies                  # Company directory
├── /companies/[slug]           # Company profile
├── /newsletter                 # Newsletter signup
├── /newsletter/archive         # Past issues
├── /search                     # Search results
├── /about                      # About the site
└── /api/
    ├── /api/articles
    ├── /api/search
    └── /api/subscribe
```

---

## 4. Design System

### UI/UX IS OUR PRIMARY DIFFERENTIATOR

Existing graphene sites look like they were built in 2005. We build something stunning that makes visitors go "wow."

### Color Palette: Charcoal Dark + Silver

```
Background:     #0d0d0d (deep charcoal - primary bg)
Surface:        #1a1a1a (elevated surfaces, cards)
Surface Light:  #2a2a2a (hover states, borders)
Silver:         #c0c0c0 (primary accent - headings, highlights)
Silver Light:   #e0e0e0 (secondary text, subtle accents)
Silver Bright:  #f5f5f5 (primary text on dark)
Text Primary:   #f5f5f5 (main body text)
Text Secondary: #a0a0a0 (muted text, timestamps)
Text Muted:     #666666 (subtle labels)
Accent:         #c0c0c0 (silver for links, buttons)
Accent Hover:   #e0e0e0 (brighter on interaction)
Success:        #4ade80 (green for positive indicators)
Warning:        #facc15 (yellow for alerts)
```

### Design System Rules

- **Dark mode only** - No light mode. Commitment to the aesthetic.
- **Generous whitespace** (or "darkspace")
- **Subtle gradients** and glassmorphism effects
- **Micro-animations** on interactions
- **Consistent 4px/8px spacing grid**
- **Rounded corners** - 8px for cards, 4px for buttons

### Typography

| Use | Font | Notes |
|-----|------|-------|
| Headings | **Inter** or **Satoshi** | Clean, modern, geometric |
| Body | **Inter** | Highly readable at all sizes |
| Technical/Code | **JetBrains Mono** or **Fira Code** | Specs, formulas, data |

- Base size: 14px
- Line height: 1.6
- Responsive scaling

### Components to Nail

- **Article cards** - Elegant, scannable, beautiful hover states
- **Navigation** - Minimal, fixed, with subtle backdrop blur
- **Search** - Command palette style (⌘K), instant results
- **Wiki pages** - Magazine-quality layout, pull quotes, visualizations
- **Newsletter signup** - Tasteful, not desperate
- **Mobile** - Touch-optimized, gesture-friendly

### UX Principles

1. **Premium feel** - Every pixel intentional, no jank
2. **Speed first** - Sub-second page loads, instant interactions
3. **Scannable** - Headlines, summaries, then depth
4. **Keyboard accessible** - Power users can navigate without mouse
5. **Progressive disclosure** - Don't overwhelm, reveal on demand
6. **Delightful details** - Subtle animations, satisfying transitions
7. **Mobile-first** - Designed for phone, enhanced for desktop

### Inspiration Sites

- **Linear** - Dark mode done right, subtle animations
- **Stripe** - Attention to detail, premium feel
- **The Verge** - Bold design choices, clear hierarchy
- **Raycast** - Command palette, keyboard-first
- **Loom** - Clean, modern, SaaS-quality

### Anti-Patterns to Avoid

- Cluttered layouts (Graphene-Info's problem)
- Aggressive popups or interstitials
- Generic Bootstrap/template feel
- Tiny text or low contrast
- Slow animations that block interaction
- Cookie banners larger than the content
- Cheesy stock photos - NEVER

---

## 5. Implementation Plan

### Phase 1: Foundation + Manual Content ← CURRENT

**Goal:** Beautiful site with manually curated content to validate design and value prop.

**Deliverables:**
- [ ] Initialize Astro project with Tailwind
- [ ] Set up Supabase project and schema
- [ ] Build homepage (hero + latest articles + featured)
- [ ] Build article list page (with category filters)
- [ ] Build article detail page
- [ ] Build wiki structure (5-10 foundational pages)
- [ ] Manually add 20-30 seed articles
- [ ] Deploy to Railway
- [ ] Basic SEO (meta tags, OG images)

**Exit Criteria:** Site live with beautiful design, seed content, wiki foundation.

### Phase 2: Scraping Infrastructure

**Goal:** Automated content ingestion from multiple sources.

**Deliverables:**
- [ ] Build source configuration system
- [ ] Implement RSS scraper
- [ ] Implement HTML scraper (Cheerio)
- [ ] Implement headless scraper (Playwright) for JS sites
- [ ] Set up scheduled jobs (hourly/daily via BullMQ)
- [ ] Build raw items queue
- [ ] Add 10-15 sources (RSS feeds, press release sites, etc.)

**Exit Criteria:** Automated scraping running, raw items flowing in.

### Phase 3: AI Processing Pipeline

**Goal:** Automated filtering, classification, and summarization.

**Deliverables:**
- [ ] Integrate Claude API
- [ ] Build relevance filter (is this about graphene?)
- [ ] Build category classifier
- [ ] Build summarizer (press release → article)
- [ ] Build deduplication logic
- [ ] Build importance scorer
- [ ] Connect pipeline: raw → processed → published
- [ ] Build admin dashboard for monitoring

**Exit Criteria:** End-to-end automation: scrape → process → publish.

### Phase 4: Newsletter

**Goal:** Automated weekly newsletter.

**Deliverables:**
- [ ] Newsletter signup flow
- [ ] Email confirmation (double opt-in)
- [ ] Newsletter template design (matches site aesthetic)
- [ ] AI-powered issue generation (select top stories, write intro)
- [ ] Integrate with Buttondown
- [ ] Scheduled weekly send
- [ ] Unsubscribe handling

**Exit Criteria:** Weekly newsletter going out automatically.

### Phase 5: Search + Polish

**Goal:** Full-text search and UX refinements.

**Deliverables:**
- [ ] Integrate Meilisearch
- [ ] Search UI (command palette style, instant results)
- [ ] Company directory pages
- [ ] Related articles on article pages
- [ ] Wiki ↔ news cross-linking
- [ ] Performance optimization
- [ ] Mobile polish

**Exit Criteria:** Fast search, polished UX, ready for growth.

### Phase 6: Monetization

**Deliverables:**
- [ ] Sponsorship/ad placements (newsletter sponsors first)
- [ ] Premium tier (early access, research reports)
- [ ] Display ads (if traffic warrants - Mediavine at 50K sessions)
- [ ] Job board (graphene industry jobs)

---

## 6. Content Sources

### RSS Feeds
- arXiv (cond-mat, materials science)
- Nanowerk
- Phys.org (materials section)
- ScienceDaily (materials)
- EurekAlert (research news)

### Press Release Sites
- Business Wire (graphene keyword)
- PR Newswire (graphene keyword)
- GlobeNewswire

### Company Newsrooms
- Graphene Flagship (EU project)
- National Graphene Institute (Manchester)
- First Graphene
- Directa Plus
- Versarien

### Academic Journals
- Nature Materials
- Advanced Materials
- ACS Nano
- 2D Materials

### Patent Databases
- USPTO (graphene filings)
- EPO

---

## 7. Wiki Structure

```
/wiki
├── /what-is-graphene          # The basics, beautifully explained
├── /properties
│   ├── /electrical            # Conductivity, band gap
│   ├── /mechanical            # Strength, flexibility
│   ├── /thermal               # Heat conductivity
│   └── /optical               # Transparency, absorption
├── /production
│   ├── /cvd                   # Chemical vapor deposition
│   ├── /exfoliation           # Mechanical exfoliation
│   ├── /reduction             # Graphene oxide reduction
│   └── /comparison            # Methods compared
├── /applications
│   ├── /batteries             # Energy storage
│   ├── /electronics           # Transistors, displays
│   ├── /composites            # Stronger materials
│   ├── /medical               # Drug delivery, imaging
│   ├── /water-filtration      # Desalination, purification
│   ├── /sensors               # Chemical, biological
│   └── /coatings              # Anti-corrosion, conductive
├── /companies
│   ├── /manufacturers         # Who makes graphene
│   ├── /startups              # Emerging companies
│   └── /research-labs         # Academic institutions
├── /history
│   └── /timeline              # Discovery to today
└── /glossary                  # Technical terms
```

---

## 8. Critical Files Reference

```
graphenepulse/
├── src/
│   ├── components/
│   │   ├── ArticleCard.astro       # News article card
│   │   ├── WikiNav.astro           # Wiki sidebar navigation
│   │   ├── SearchPalette.astro     # Command palette search
│   │   ├── NewsletterSignup.astro  # Email capture
│   │   └── CompanyCard.astro       # Company directory card
│   ├── layouts/
│   │   ├── BaseLayout.astro        # Site-wide layout
│   │   ├── ArticleLayout.astro     # Single article layout
│   │   └── WikiLayout.astro        # Wiki page layout
│   ├── pages/
│   │   ├── index.astro             # Homepage
│   │   ├── news/
│   │   │   ├── index.astro         # News listing
│   │   │   └── [slug].astro        # Article detail
│   │   ├── wiki/
│   │   │   └── [...slug].astro     # Wiki pages (catch-all)
│   │   ├── companies/
│   │   │   ├── index.astro         # Company directory
│   │   │   └── [slug].astro        # Company profile
│   │   ├── category/
│   │   │   └── [category].astro    # Category filter
│   │   ├── newsletter.astro        # Newsletter signup
│   │   ├── search.astro            # Search results
│   │   └── about.astro             # About page
│   ├── lib/
│   │   ├── supabase.ts             # Supabase client
│   │   ├── search.ts               # Meilisearch client
│   │   └── newsletter.ts           # Buttondown API
│   └── styles/
│       └── global.css              # Tailwind + custom styles
├── workers/
│   ├── scraper/
│   │   ├── rss.ts                  # RSS feed scraper
│   │   ├── html.ts                 # HTML scraper (Cheerio)
│   │   └── headless.ts             # Playwright scraper
│   ├── processor/
│   │   ├── relevance.ts            # Is this about graphene?
│   │   ├── classifier.ts           # Category assignment
│   │   ├── summarizer.ts           # AI summarization
│   │   └── deduper.ts              # Duplicate detection
│   └── newsletter/
│       └── generator.ts            # Weekly newsletter builder
├── astro.config.mjs
├── tailwind.config.js
└── package.json
```

---

## 9. Context for AI Agents

### Instructions for New Sessions

1. **Read this entire document first** before taking any action
2. **Check project-tracker.md** in interstellar repo for current status
3. **Do not re-debate decided decisions** listed below
4. **Focus on current phase** deliverables only
5. **Update this document** at session end with progress

### Decisions Already Made (DO NOT CHANGE)

- **Astro** for framework (not SvelteKit) - better for content-heavy sites
- **Claude API** for AI processing (not OpenAI) - better quality
- **Meilisearch** for search (not Algolia) - cost effective, self-hosted
- **Buttondown** for newsletter (not ConvertKit) - simple, good API
- **Dark mode only** - no light mode, this is the brand
- **Charcoal + Silver** color scheme - #0d0d0d bg, #c0c0c0 accent
- **News first, wiki supports** - aggregation is the hook
- **Fully automated** - AI pipeline, minimal human intervention
- **No user accounts** - maximum passivity

### Open Questions (Can Still Decide)

- Exact scraper scheduling (hourly vs every 6 hours for different sources)
- Newsletter send day (Tuesday vs Thursday)
- Premium tier pricing and features
- Job board implementation details

### Common Pitfalls to Avoid

1. **Don't compromise on design** - This is our differentiator. Every detail matters.
2. **Don't over-engineer scrapers initially** - Start simple, add complexity as needed
3. **Don't forget mobile** - Design mobile-first, enhance for desktop
4. **Don't skip AI prompts tuning** - Invest time in relevance and classification prompts
5. **Don't publish low-quality summaries** - Better to have fewer, better articles
6. **Don't use light text on dark without checking contrast** - Accessibility matters

### Useful Commands

```bash
# Development
npm run dev          # Local dev server
npm run build        # Production build
npm run preview      # Preview production build

# Database
npx supabase start   # Local Supabase
npx supabase db push # Push schema changes

# Scrapers (when built)
npm run scrape:rss   # Run RSS scraper
npm run scrape:all   # Run all scrapers
npm run process      # Process raw items

# Newsletter
npm run newsletter:preview  # Preview next issue
npm run newsletter:send     # Send newsletter
```

---

## 10. Revenue Model

### Primary: Newsletter Sponsorships

- Build subscriber base first (target: 500 in 3 months)
- Graphene companies pay to sponsor weekly newsletter
- $200-500 per newsletter at small scale
- $1,000-2,000 per newsletter at scale

### Secondary: Premium Tier

- Early access to news (before public)
- Research report summaries
- Company deep dives
- $10-20/month or $100-150/year
- Target: 100 paying subscribers = $1,000-1,500/month

### Tertiary: Display Ads

- Only at scale (50K+ monthly sessions)
- Mediavine or similar premium network
- $500-1,500/month potential

### Future: Job Board

- Graphene industry job postings
- $100-200 per listing
- Passive once built

### Revenue Projections

| Phase | Traffic | Revenue |
|-------|---------|---------|
| Foundation | <5K/mo | $0 |
| Growth | 10K/mo | $200-500/mo (first sponsors) |
| Traction | 25K/mo | $1,000-2,000/mo |
| Scale | 50K+/mo | $3,000-5,000/mo |

---

## 11. Competitive Analysis

### Graphene-Info

| Strength | Weakness |
|----------|----------|
| Comprehensive news coverage | Dated design (looks like 2010) |
| Years of archive content | Cluttered, hard to navigate |
| Domain authority | No newsletter |
| | Slow page loads |

**How we beat them:** Better design, faster site, newsletter, wiki.

### The Graphene Council

| Strength | Weakness |
|----------|----------|
| Industry authority | Membership-gated content |
| Corporate connections | Corporate/stuffy feel |
| Event coverage | Sparse updates |
| | B2B only audience |

**How we beat them:** Open access, broader audience, daily updates.

### Our Position

**"The TechCrunch of graphene"** - authoritative but accessible, beautiful but substantive, automated but high-quality.

---

## 12. Passivity Analysis

| Factor | Score | Notes |
|--------|-------|-------|
| **Automation** | 9/10 | AI pipeline handles content |
| **Maintenance** | 7/10 | Monitor scrapers, tune prompts |
| **Support Burden** | 10/10 | No user accounts, no support |
| **Scaling** | 9/10 | More sources = more content automatically |
| **Technical** | 6/10 | Scrapers need monitoring |

**Overall Passivity Score: 8/10**

This is more complex than a static calculator site but the automation makes it highly passive once built.

---

## 13. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Scraping blocked | Medium | High | Multiple sources, respect robots.txt, rate limiting |
| AI summarization quality | Medium | Medium | Human review queue initially, fine-tune prompts |
| Low initial traffic | High | Medium | SEO focus, newsletter building, patience |
| Graphene-Info dominates SEO | Medium | Medium | Better content, better UX, niche down initially |
| Content licensing issues | Low | High | Link back, excerpt only, transform content |
| Scraping costs (API, compute) | Medium | Low | Efficient scheduling, caching, budget monitoring |

---

## 14. Session Log

### 2025-12-22 - In Development
- Repo created at github.com/BenTyson/pulse
- Development underway - see repo for current state
- For continued development, work in the pulse repo directly

### 2025-12-19 - Project Created
- Conceived as premiere graphene news hub
- Named "Graphene Pulse" - "The pulse of the graphene industry"
- Emphasized UI/UX as primary differentiator
- Established Charcoal Dark (#0d0d0d) + Silver (#c0c0c0) color scheme
- Defined 6-phase implementation plan
- Created comprehensive technical architecture with scraping pipeline
- Database schema designed for news aggregation workflow
- Added to High-Value Projects category in portfolio

---

## 15. About Graphene (Reference)

### What is Graphene?

Graphene is a single layer of carbon atoms arranged in a hexagonal lattice. Isolated in 2004 by Andre Geim and Konstantin Novoselov (Nobel Prize 2010), it's considered a "wonder material."

### Key Properties

- **200x stronger than steel** (by weight)
- **Best electrical conductor known** - electrons travel at 1/300 speed of light
- **Best thermal conductor known** - 5,000 W/mK
- **Nearly transparent** - 97.7% light transmission
- **Flexible and lightweight**
- **Impermeable to gases** - even helium

### Market Size

- 2023: ~$200 million globally
- 2030 projection: $1.5+ billion
- CAGR: ~30%

### Major Applications

- Batteries and supercapacitors
- Electronic components
- Composite materials
- Medical devices
- Water filtration
- Sensors
- Coatings

---

**Next Action:** Create Astro project and begin Phase 1 (Foundation)

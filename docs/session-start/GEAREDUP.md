# GearedUp - Session Start Document

> **Read this first.** This document contains everything needed to start a productive session on GearedUp.

---

## 1. Quick Context

| Field | Value |
|-------|-------|
| **Project** | GearedUp |
| **Tagline** | "Gear up for your hobby" |
| **What** | Curated "best X for Y" recommendations for hobby gear |
| **Stack** | Astro + Tailwind + Cloudflare Pages |
| **Revenue** | Affiliate links (Amazon, specialty retailers) |
| **Target** | $1-3K/month |
| **Status** | Planning Complete |
| **Repo** | Not yet created |

---

## 2. Full Vision

### What is GearedUp?

GearedUp is a curated recommendation site targeting hobbyists searching for gear. Every page answers a specific "best X for Y" query with honest, well-researched recommendations.

**Examples:**
- "Best rotary cutter for quilting"
- "Best resin printer for miniatures"
- "Best mechanical pencil for sketching"
- "Best storage solution for board games"
- "Best yarn for beginners"
- "Best wood carving knife set"

### Why This Will Work

1. **Low competition** - Major review sites (Wirecutter, etc.) ignore niche hobby gear
2. **High intent traffic** - People searching are ready to buy
3. **Passionate audience** - Hobbyists research purchases deeply and spend money
4. **Evergreen content** - Hobby gear doesn't change as fast as tech
5. **Long-tail SEO goldmine** - Thousands of specific queries with little competition
6. **Synergy with existing projects** - Overlaps with CraftCalc, Good Game audiences

### Target Users

| Persona | Example Search | Buying Behavior |
|---------|----------------|-----------------|
| **New Hobbyist** | "best sewing machine for beginners" | Needs guidance, appreciates curated picks |
| **Upgrading Hobbyist** | "best rotary cutter for heavy fabric" | Knows what they want, looking for validation |
| **Gift Buyer** | "best gifts for quilters" | High intent, needs quick answer |
| **Niche Enthusiast** | "best sleeves for MTG cards" | Very specific, will buy premium |

### Differentiators

| Us | Competitors |
|----|-------------|
| Hobby-focused, deep niche expertise | Generic "best X" sites spread thin |
| Clean, fast, no-nonsense UX | Bloated sites with popups and ads |
| Honest picks (not just highest commission) | Obvious affiliate plays |
| Specific use cases ("for beginners", "for small hands") | Generic recommendations |

---

## 3. Hobby Categories

### Tier 1: Launch Categories (synergy with existing projects)

| Category | Example Pages | Affiliate Partners |
|----------|---------------|-------------------|
| **Quilting & Sewing** | Rotary cutters, cutting mats, sewing machines, fabric scissors | Amazon, Joann, Fat Quarter Shop |
| **Knitting & Yarn Crafts** | Needles, yarn winders, blocking mats, project bags | Amazon, KnitPicks, Webs |
| **Board Gaming** | Card sleeves, storage solutions, playmats, organizers | Amazon, GameNerdz |
| **Miniature Painting** | Brushes, paints, wet palettes, magnifying lamps | Amazon, Miniature Market |

### Tier 2: Expansion Categories

| Category | Example Pages | Affiliate Partners |
|----------|---------------|-------------------|
| **Mountaineering & Hiking** | Ice axes, crampons, helmets, trekking poles, backpacks | REI, Backcountry, Amazon |
| **Woodworking** | Chisels, hand planes, carving knives, clamps | Amazon, Rockler, Woodcraft |
| **Resin Crafts** | Resin printers, UV resins, molds, pressure pots | Amazon, Elegoo |
| **Drawing & Illustration** | Pencils, sketchbooks, markers, drawing tablets | Amazon, Blick Art |
| **Calligraphy & Journaling** | Pens, inks, notebooks, wax seals | Amazon, JetPens, Goulet Pens |
| **Tabletop RPG** | Dice, dice trays, DM screens, battle mats | Amazon, Die Hard Dice |

**Note:** Mountaineering & Hiking is a strategic category that syncs with Summit58. See Section 16 for integration details.

### Tier 3: Future Categories

- Candle making
- Soap making
- Jewelry making
- Leatherworking
- Embroidery / Cross stitch
- Model building
- RC hobbies
- Aquariums
- Gardening tools

---

## 4. Content Structure

### Page Types

#### 1. Best X for Y (Primary - 80% of content)
**URL pattern:** `/best-[product]-for-[use-case]/`

**Examples:**
- `/best-rotary-cutter-for-beginners/`
- `/best-card-sleeves-for-mtg/`
- `/best-resin-printer-for-miniatures/`

**Template structure:**
```
# Best [Product] for [Use Case] (2025)

Quick Answer: [Top pick with affiliate link]

## Our Top Picks
1. Best Overall: [Product] - [1-line reason]
2. Best Budget: [Product] - [1-line reason]
3. Best Premium: [Product] - [1-line reason]

## Quick Comparison Table
[Product | Price | Key Feature | Best For]

## Detailed Reviews
[Each product: 150-300 words with pros/cons]

## How We Chose
[Methodology, what matters, what doesn't]

## FAQ
[3-5 common questions]
```

#### 2. Gift Guides (Seasonal - 10% of content)
**URL pattern:** `/gifts-for-[persona]/`

**Examples:**
- `/gifts-for-quilters/`
- `/gifts-for-board-gamers/`
- `/gifts-for-miniature-painters/`

#### 3. Category Hubs (Navigation - 10% of content)
**URL pattern:** `/[category]/`

**Examples:**
- `/quilting/` - Hub linking to all quilting gear pages
- `/board-gaming/` - Hub linking to all board game gear pages

---

## 5. Technical Architecture

### Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| **Framework** | Astro | SSG, fast, SEO-optimized |
| **Styling** | Tailwind CSS | Consistent with portfolio |
| **Hosting** | Cloudflare Pages | Free, fast, global CDN |
| **Analytics** | Plausible | Privacy-focused, no cookie banner |
| **Images** | Cloudflare Images or local optimized | Fast loading crucial for UX |

### URL Structure

```
gearedup.com/
├── /                                    # Homepage with category grid
├── /quilting/                          # Category hub
│   ├── /best-rotary-cutter-for-beginners/
│   ├── /best-cutting-mat-for-quilting/
│   ├── /best-sewing-machine-for-quilting/
│   └── ...
├── /board-gaming/                      # Category hub
│   ├── /best-card-sleeves-for-mtg/
│   ├── /best-board-game-storage/
│   └── ...
├── /miniature-painting/                # Category hub
│   ├── /best-brushes-for-miniatures/
│   ├── /best-wet-palette/
│   └── ...
├── /gifts-for-quilters/                # Gift guide
├── /gifts-for-board-gamers/            # Gift guide
└── /about/                             # About/methodology
```

### Data Model

```typescript
// Content stored as Astro content collections (Markdown + frontmatter)

interface Product {
  name: string;
  brand: string;
  price: number;           // Approximate, with "check price" CTA
  affiliateUrl: string;    // Amazon or specialty retailer
  image: string;
  pros: string[];
  cons: string[];
  bestFor: string;         // "beginners", "heavy use", "budget", etc.
  verdict: string;         // 1-2 sentence summary
}

interface BestXForYPage {
  slug: string;
  title: string;           // "Best Rotary Cutter for Beginners"
  category: string;        // "quilting"
  metaDescription: string;
  lastUpdated: Date;
  quickAnswer: Product;    // The #1 pick
  products: Product[];     // All reviewed products
  methodology: string;     // How we chose
  faqs: FAQ[];
}

interface CategoryHub {
  slug: string;
  name: string;            // "Quilting"
  description: string;
  pages: string[];         // Links to all pages in category
}
```

### Affiliate Strategy

| Partner | Commission | Best For |
|---------|------------|----------|
| **Amazon Associates** | 1-4% | Everything, convenience |
| **ShareASale** | Varies (5-15%) | Specialty retailers |
| **Direct Programs** | 5-20% | Brand-specific (Elegoo, etc.) |

**Link Strategy:**
- Primary CTA → Amazon (highest conversion)
- Secondary link → Specialty retailer (higher commission)
- Always disclose affiliate relationship

---

## 6. SEO Strategy

### Keyword Research Approach

Target format: `best [product] for [modifier]`

**Modifiers that work:**
- Skill level: "for beginners", "for professionals"
- Use case: "for quilting", "for miniatures"
- Constraint: "under $50", "for small spaces"
- Physical: "for large hands", "for arthritis"

### Content Prioritization

1. **High volume + low competition** - Do these first
2. **Medium volume + no good results** - Quick wins
3. **Gift guides before holidays** - Seasonal traffic spikes
4. **Category hubs** - Internal linking power

### On-Page SEO

- Title: "Best [Product] for [Use Case] (2025) | GearedUp"
- H1: "Best [Product] for [Use Case]"
- Quick answer in first 100 words (featured snippet bait)
- Comparison table (rich result potential)
- FAQ schema markup
- Product schema markup
- Last updated date (freshness signal)

### Link Building

- Minimal active link building needed
- Natural links from hobby forums/Reddit when helpful
- Internal linking between related pages

---

## 7. Implementation Plan

### Phase 1: Foundation (MVP)
- [ ] Create Astro project with Tailwind
- [ ] Build page templates (Best X for Y, Category Hub)
- [ ] Set up content collections
- [ ] Create 10 pilot pages across 2 categories:
  - Quilting (5 pages)
  - Board Gaming (5 pages)
- [ ] Deploy to Cloudflare Pages
- [ ] Set up Plausible analytics
- [ ] Apply for Amazon Associates

**Exit Criteria:** 10 pages live, indexed, affiliate links working

### Phase 2: Content Expansion
- [ ] Add 20 more pages (30 total)
- [ ] Add 2 more categories (Miniature Painting, Knitting)
- [ ] Create category hub pages
- [ ] Internal linking optimization
- [ ] Add FAQ schema markup

**Exit Criteria:** 30 pages, 4 categories, schema implemented

### Phase 3: Scale & Monetize
- [ ] Add 20 more pages (50 total)
- [ ] Create gift guide pages
- [ ] Apply for specialty affiliate programs
- [ ] Add comparison tables to all pages
- [ ] Monitor rankings, double down on winners

**Exit Criteria:** 50 pages, affiliate revenue started

### Phase 4: Optimize & Grow
- [ ] Expand to Tier 2 categories based on performance
- [ ] Update top-performing pages with more depth
- [ ] Add product schema markup
- [ ] Target 100+ pages
- [ ] Evaluate AdSense if traffic warrants

---

## 8. Pilot Pages (Phase 1)

### Quilting (5 pages)
1. Best Rotary Cutter for Beginners
2. Best Cutting Mat for Quilting
3. Best Sewing Machine for Quilting Under $500
4. Best Fabric Scissors for Quilting
5. Best Quilting Ruler Set

### Board Gaming (5 pages)
1. Best Card Sleeves for MTG
2. Best Board Game Storage Solutions
3. Best Playmat for Card Games
4. Best Dice Set for D&D
5. Best Board Game Table Topper

---

## 9. Sample Page Content

### Example: Best Rotary Cutter for Beginners

```markdown
---
title: "Best Rotary Cutter for Beginners (2025)"
description: "Find the perfect rotary cutter to start quilting. We tested 8 popular options and picked the best for new quilters."
category: "quilting"
lastUpdated: 2025-01-15
---

# Best Rotary Cutter for Beginners (2025)

**Quick Answer:** The [Fiskars 45mm Rotary Cutter] is our top pick for beginners.
It's comfortable, reliable, and the safety features prevent accidents while you learn.

## Our Top 3 Picks

| Pick | Product | Price | Best For |
|------|---------|-------|----------|
| Best Overall | Fiskars 45mm | ~$15 | Most beginners |
| Best Ergonomic | Olfa Ergonomic | ~$20 | Longer cutting sessions |
| Best Budget | DAFA 45mm | ~$8 | Trying quilting out |

## Detailed Reviews

### Fiskars 45mm Rotary Cutter - Best Overall
[Image]

The Fiskars 45mm has been the go-to beginner cutter for years, and for good reason...

**Pros:**
- Comfortable grip
- Easy blade changes
- Safety lock
- Widely available replacement blades

**Cons:**
- Not the sharpest out of the box
- Basic design

**Verdict:** The reliable choice. You can't go wrong starting here.

[Check Price on Amazon →]

...
```

---

## 10. Revenue Projections

### Assumptions
- 50 pages at maturity
- Average 500 pageviews/month per page = 25,000 monthly pageviews
- 5% click-through to affiliate links = 1,250 clicks
- 3% conversion rate = 37 purchases
- $40 average order value
- 4% commission = $1.60 per sale

### Projections

| Metric | Value |
|--------|-------|
| Monthly Pageviews | 25,000 |
| Affiliate Clicks | 1,250 |
| Purchases | 37 |
| Affiliate Revenue | ~$60/month |

**Wait, that's low.** Here's how it scales:

| Pages | Pageviews | Revenue |
|-------|-----------|---------|
| 50 | 25K | $60 |
| 100 | 50K | $120 |
| 200 | 100K | $240 |

**The real money:**
1. **Higher-ticket items** - Sewing machines ($300+) = $12+ per sale
2. **Specialty affiliate programs** - 10-15% commission
3. **Display ads at scale** - Mediavine at 50K sessions = $500-1K/month
4. **Compound traffic** - Top pages can get 5-10K views/month

**Realistic target:** $1-3K/month at 100K+ pageviews with mixed affiliate + ads

---

## 11. Passivity Analysis

| Factor | Score | Notes |
|--------|-------|-------|
| **Content Freshness** | 9/10 | Hobby gear doesn't change fast |
| **Maintenance** | 9/10 | Update prices/links occasionally |
| **Support Burden** | 10/10 | No users, no accounts |
| **Scaling** | 8/10 | More pages = more revenue (linear) |
| **Technical** | 10/10 | Static site, no backend |

**Overall Passivity Score: 9/10**

Only maintenance: Periodically check that products are still available and prices are accurate. Can be done quarterly.

---

## 12. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Amazon Associates rejection/termination | Medium | High | Diversify to specialty programs early |
| Content doesn't rank | Medium | High | Target low-competition keywords first |
| Competition enters niche | Low | Medium | First-mover advantage, build authority |
| Products go out of stock | Medium | Low | Monitor and update, have alternates |

---

## 13. AI Agent Instructions

### Do
- Keep pages focused and scannable
- Always include quick answer at top
- Use comparison tables
- Be honest about cons
- Include "last updated" dates
- Optimize images aggressively

### Don't
- Write fluff content to hit word counts
- Recommend products just for high commission
- Forget affiliate disclosures
- Ignore mobile experience
- Over-optimize for SEO at expense of UX

### Code Patterns
- Use Astro content collections for all pages
- Keep components simple and reusable
- Lazy load images below fold
- Preload critical CSS

### Decisions Already Made
- Astro over Next.js (simpler, faster builds)
- Tailwind over custom CSS (consistency)
- Cloudflare Pages over Vercel (free tier better)
- Amazon first, diversify later (highest conversion)
- Start with 2 categories, prove concept, expand

---

## 14. Session Log

### 2025-12-15 - Summit58 Integration Added
- Added Mountaineering & Hiking as Tier 2 category
- Created Section 16: Summit58 Integration with full synergy plan
- Defined 28 mountaineering gear pages for future expansion
- Mapped cross-linking strategy between sites
- Updated ecosystem diagram to show GearedUp as central hub
- Documented phased integration approach (simple links → embedded components → shared data)

### 2025-12-15 - Project Created
- Researched curated list / "best X for Y" model
- Evaluated verticals: chose Niche Hobbies for low competition + passionate buyers
- Named project GearedUp - "Gear up for your hobby"
- Created comprehensive session-start document
- Defined 4-phase implementation plan
- Selected pilot categories: Quilting + Board Gaming (synergy with CraftCalc, Good Game)

---

## 15. Quick Reference

### Key Files (Once Repo Created)
```
gearedup/
├── src/
│   ├── content/
│   │   ├── quilting/           # Quilting pages
│   │   ├── board-gaming/       # Board gaming pages
│   │   └── config.ts           # Content collection schema
│   ├── components/
│   │   ├── ProductCard.astro
│   │   ├── ComparisonTable.astro
│   │   ├── QuickAnswer.astro
│   │   └── AffiliateLink.astro
│   ├── layouts/
│   │   ├── BaseLayout.astro
│   │   └── BestXForYLayout.astro
│   └── pages/
│       ├── index.astro
│       ├── [category]/
│       │   └── index.astro     # Category hub
│       └── [...slug].astro     # Dynamic page routing
├── astro.config.mjs
├── tailwind.config.js
└── package.json
```

### Commands
```bash
npm run dev      # Local development
npm run build    # Production build
npm run preview  # Preview production build
```

### Links
- Astro Docs: https://docs.astro.build
- Amazon Associates: https://affiliate-program.amazon.com
- Plausible: https://plausible.io

---

## 16. Summit58 Integration

GearedUp serves as the gear recommendation engine for the Summit58 ecosystem. This creates cross-linking opportunities and shared audience benefits.

### Mountaineering & Hiking Category

This category is specifically designed to support Summit58 users researching gear for Colorado 14ers.

#### Priority Pages (Summit58 Synergy)

| Page | Summit58 Link Context |
|------|----------------------|
| **Best Ice Axe for Beginners** | Class 3+ routes, spring/early summer |
| **Best Crampons for 14ers** | Snow routes, Longs Peak, Capitol |
| **Best Hiking Boots for 14ers** | General gear page, all peaks |
| **Best Trekking Poles for Scrambling** | Class 2-3 routes |
| **Best Climbing Helmet for Mountaineering** | Class 3+ routes, rockfall zones |
| **Best Daypack for 14ers** | General gear page |
| **Best Microspikes for Hiking** | Spring conditions, snow travel |
| **Best Gaiters for Scree** | Loose rock routes |
| **Best Layers for Alpine Starts** | All peaks, weather page |
| **Best Headlamp for Mountain Climbing** | Alpine starts, long routes |

#### Cross-Linking Strategy

```
Summit58 Route Page                    GearedUp Page
─────────────────────────────────────────────────────────────
Longs Peak (Class 3)          →        Best Helmet for Mountaineering
  "Helmets recommended"                Best Ice Axe for Beginners

Capitol Peak (Class 4)        →        Best Climbing Helmet
  "Technical gear required"            Best Crampons for 14ers

Quandary Peak (Class 1)       →        Best Hiking Boots for 14ers
  "Gear checklist"                     Best Trekking Poles

Any peak conditions page      →        Best Microspikes for Hiking
  "Snow reported"                      Best Gaiters for Scree
```

#### URL Pattern for Mountaineering

```
gearedup.com/
├── /mountaineering/                    # Category hub
│   ├── /best-ice-axe-for-beginners/
│   ├── /best-crampons-for-14ers/
│   ├── /best-helmet-for-mountaineering/
│   ├── /best-trekking-poles-for-scrambling/
│   ├── /best-hiking-boots-for-14ers/
│   ├── /best-daypack-for-14ers/
│   ├── /best-microspikes-for-hiking/
│   └── ...
├── /gifts-for-hikers/                  # Gift guide
└── /gifts-for-mountaineers/            # Gift guide
```

### Integration Implementation

#### Phase 1: Foundation (No Integration)
- Build GearedUp MVP with Quilting + Board Gaming
- No mountaineering content yet
- Summit58 doesn't exist yet

#### Phase 2: Parallel Development
- When Summit58 launches, add Mountaineering category to GearedUp
- Start with 5 high-value gear pages
- Manual cross-links between sites

#### Phase 3: Deep Integration
- Summit58 gear checklists link directly to GearedUp recommendations
- GearedUp mountaineering pages reference Summit58 for route info
- Shared affiliate tracking (if using same Amazon Associates account)
- Consider embedded GearedUp components on Summit58

### Technical Integration Options

#### Option A: Simple Cross-Linking (Recommended for MVP)
```html
<!-- On Summit58 route page -->
<a href="https://gearedup.com/best-helmet-for-mountaineering/">
  Helmet recommendations →
</a>

<!-- On GearedUp mountaineering page -->
<p>Planning a 14er? Check <a href="https://summit58.co">Summit58</a>
for routes and conditions.</p>
```

#### Option B: Embedded Components (Future)
```html
<!-- Summit58 could embed GearedUp gear cards -->
<iframe src="https://gearedup.com/embed/best-helmet-for-mountaineering" />

<!-- Or use shared component library -->
<GearRecommendation product="helmet" context="class-3" />
```

#### Option C: Shared Data Layer (Future)
- Both sites pull from same product database
- Supabase shared schema for gear data
- Real-time price/availability updates

**Recommendation:** Start with Option A. Simple, works immediately, no technical debt. Evaluate B/C after both sites have traction.

### Affiliate Synergy

Both sites can use the same affiliate accounts:

| Program | GearedUp | Summit58 | Shared Benefit |
|---------|----------|----------|----------------|
| Amazon Associates | Primary | Gear links | Same account, combined volume |
| REI Affiliate | Mountaineering | Gear links | Higher tier faster |
| Backcountry | Mountaineering | Gear links | Combined volume |

**Important:** Use consistent affiliate tags or sub-tags to track which site drives conversions.

### Content Coordination

| Content Type | Lives On | Links To |
|--------------|----------|----------|
| "Best X for Y" gear reviews | GearedUp | Summit58 (context) |
| Route-specific gear lists | Summit58 | GearedUp (products) |
| Seasonal gear guides | GearedUp | Summit58 (conditions) |
| Peak gear checklists | Summit58 | GearedUp (each item) |

### Mountaineering Pages - Full List

#### Essential Gear (10 pages)
1. Best Ice Axe for Beginners
2. Best Crampons for 14ers
3. Best Climbing Helmet for Mountaineering
4. Best Hiking Boots for 14ers
5. Best Trekking Poles for Scrambling
6. Best Daypack for 14ers (30-40L)
7. Best Microspikes for Hiking
8. Best Gaiters for Scree and Snow
9. Best Headlamp for Alpine Starts
10. Best GPS Device for Mountain Navigation

#### Clothing (8 pages)
1. Best Base Layer for Mountain Climbing
2. Best Insulated Jacket for 14ers
3. Best Hardshell Jacket for Alpine Climbing
4. Best Softshell Pants for Mountaineering
5. Best Hiking Socks for Long Days
6. Best Sun Hat for High Altitude
7. Best Gloves for Scrambling
8. Best Buff/Neck Gaiter for Mountains

#### Safety & Navigation (5 pages)
1. Best Emergency Bivy for Day Hikers
2. Best First Aid Kit for Mountaineering
3. Best Sunscreen for High Altitude
4. Best Sunglasses for Snow/Mountains
5. Best Two-Way Radio for Group Climbs

#### Accessories (5 pages)
1. Best Water Bottle for Hiking
2. Best Hydration Bladder for Mountaineering
3. Best Trekking Pole Tips for Rock
4. Best Stuff Sacks for Organization
5. Best Bear Canister for Backcountry

**Total: 28 mountaineering pages** → significant content expansion

---

## 17. Sister Site Ecosystem (Updated)

```
┌─────────────────────────────────────────────────────────────┐
│                    GEAREDUP ECOSYSTEM                        │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│                    ┌──────────────┐                         │
│                    │   GearedUp   │ ← Hub site              │
│                    │ (all hobbies)│                         │
│                    └──────┬───────┘                         │
│                           │                                  │
│         ┌─────────────────┼─────────────────┐               │
│         │                 │                 │               │
│         ▼                 ▼                 ▼               │
│  ┌────────────┐   ┌────────────┐   ┌────────────┐          │
│  │  Summit58  │   │ Good Game  │   │  CraftCalc │          │
│  │  (14ers)   │   │  (boards)  │   │  (crafts)  │          │
│  └────────────┘   └────────────┘   └────────────┘          │
│         │                 │                 │               │
│         │                 │                 │               │
│  Mountaineering    Board Gaming      Quilting/Yarn         │
│  gear pages        gear pages        gear pages            │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

GearedUp becomes the central gear recommendation hub that powers multiple niche sites:

| Niche Site | GearedUp Category | Link Direction |
|------------|-------------------|----------------|
| Summit58 | Mountaineering & Hiking | Bidirectional |
| Good Game | Board Gaming | Bidirectional |
| CraftCalc | Quilting, Knitting, Crafts | Bidirectional |

This creates a flywheel:
1. Niche sites build authority in their vertical
2. GearedUp aggregates gear expertise across verticals
3. Cross-links boost SEO for both
4. Shared audience discovers related sites
5. Affiliate revenue compounds across network

---

**Next Action:** Create gearedup repo and begin Phase 1 (Foundation)

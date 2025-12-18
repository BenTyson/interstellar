# PetPicks - Session Start Document

> **Read this first.** This document contains everything needed to start a productive session on PetPicks.

---

## 1. Quick Context

| Field | Value |
|-------|-------|
| **Project** | PetPicks |
| **Tagline** | "Picks for your pet" |
| **What** | Curated "best X for Y" recommendations for pet products |
| **Stack** | Astro + Tailwind + Cloudflare Pages |
| **Revenue** | Affiliate links (Chewy, Amazon, brand programs) |
| **Target** | $2-5K/month |
| **Status** | Planning Complete |
| **Repo** | Not yet created |

---

## 2. Full Vision

### What is PetPicks?

PetPicks is a curated recommendation site for pet owners searching for products. Every page answers a specific "best X for Y" query with honest, well-researched recommendations.

**Examples:**
- "Best dog food for sensitive stomachs"
- "Best cat litter for odor control"
- "Best dog bed for large breeds"
- "Best aquarium filter for 20 gallon tank"
- "Best chew toys for aggressive chewers"
- "Best cat tree for small apartments"

### Why This Will Work

1. **Pet owners research obsessively** - They read reviews, compare products, want the best for their pets
2. **High recurring revenue** - Food, treats, litter = monthly purchases
3. **Emotional buyers** - Price is secondary to quality for pet health
4. **Affiliate goldmine** - Chewy 5-8%, direct brand programs up to 15%
5. **Evergreen with updates** - Products change but needs don't
6. **Underserved niches** - Generic sites exist but lack depth on specific conditions/breeds

### Target Users

| Persona | Example Search | Buying Behavior |
|---------|----------------|-----------------|
| **New Pet Owner** | "best puppy food for labs" | Needs guidance, will buy recommended |
| **Problem Solver** | "best dog food for allergies" | Urgent need, price insensitive |
| **Upgrader** | "best elevated dog bowl" | Knows category, wants best option |
| **Gift Buyer** | "best gifts for dog lovers" | Seasonal, high intent |
| **Aquarist** | "best filter for planted tank" | Niche, technical, research-heavy |

### Differentiators

| PetPicks | Generic Pet Sites |
|----------|-------------------|
| Specific use cases ("for sensitive stomachs", "for large breeds") | Generic "best dog food" |
| Clean, fast, no-nonsense | Ad-heavy, slow, cluttered |
| Honest cons listed | Affiliate-driven praise |
| Condition/breed specific | One-size-fits-all |

---

## 3. Pet Categories

### Tier 1: Launch Categories (highest volume + affiliate)

| Category | Example Pages | Volume | Affiliate Potential |
|----------|---------------|--------|---------------------|
| **Dog Food** | By breed, by condition, by age, by size | Very High | Very High (recurring) |
| **Cat Food** | By condition, by age, wet vs dry | High | Very High (recurring) |
| **Cat Litter** | By odor control, clumping, tracking | High | High (recurring) |
| **Dog Beds** | By size, by age, by condition (orthopedic) | High | High |

### Tier 2: Expansion Categories

| Category | Example Pages | Volume | Affiliate Potential |
|----------|---------------|--------|---------------------|
| **Dog Toys** | By chew strength, by size, interactive | High | Medium |
| **Cat Furniture** | Trees, scratchers, window perches | Medium-High | High |
| **Dog Crates** | By size, by use (travel, training) | Medium | High |
| **Pet Health** | Supplements, dental, grooming | Medium | High |
| **Aquariums** | Filters, heaters, tanks, lighting | Medium | Medium-High |

### Tier 3: Future Categories

- Small pets (hamsters, guinea pigs, rabbits)
- Birds
- Reptiles
- Pet tech (cameras, feeders, GPS)
- Travel gear
- Training tools

---

## 4. Content Structure

### Page Types

#### 1. Best X for Y (Primary - 80% of content)
**URL pattern:** `/best-[product]-for-[modifier]/`

**Examples:**
- `/best-dog-food-for-sensitive-stomachs/`
- `/best-cat-litter-for-odor-control/`
- `/best-dog-bed-for-large-breeds/`

**Template structure:**
```
# Best [Product] for [Modifier] (2025)

Quick Answer: [Top pick with affiliate link]

## Our Top Picks
1. Best Overall: [Product] - [1-line reason]
2. Best Budget: [Product] - [1-line reason]
3. Best Premium: [Product] - [1-line reason]

## Quick Comparison Table
[Product | Price | Key Feature | Best For]

## Detailed Reviews
[Each product: 150-300 words with pros/cons]

## What to Look For
[Buying guide specific to this need]

## FAQ
[3-5 common questions]
```

#### 2. Gift Guides (Seasonal - 10% of content)
**URL pattern:** `/gifts-for-[persona]/`

**Examples:**
- `/gifts-for-dog-lovers/`
- `/gifts-for-cat-owners/`
- `/gifts-for-new-puppy-owners/`

#### 3. Category Hubs (Navigation - 10% of content)
**URL pattern:** `/[category]/`

**Examples:**
- `/dog-food/` - Hub linking to all dog food pages
- `/cat-litter/` - Hub linking to all cat litter pages

---

## 5. Technical Architecture

### Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| **Framework** | Astro | SSG, fast, SEO-optimized |
| **Styling** | Tailwind CSS | Consistent with portfolio |
| **Hosting** | Cloudflare Pages | Free, fast, global CDN |
| **Analytics** | Plausible | Privacy-focused |
| **Images** | Cloudflare Images or optimized local | Product images need to be crisp |

### URL Structure

```
petpicks.com/
├── /                                    # Homepage with category grid
├── /dog-food/                          # Category hub
│   ├── /best-dog-food-for-sensitive-stomachs/
│   ├── /best-dog-food-for-large-breeds/
│   ├── /best-dog-food-for-puppies/
│   ├── /best-dog-food-for-senior-dogs/
│   └── ...
├── /cat-food/                          # Category hub
│   ├── /best-cat-food-for-indoor-cats/
│   ├── /best-wet-cat-food/
│   └── ...
├── /cat-litter/                        # Category hub
│   ├── /best-cat-litter-for-odor-control/
│   ├── /best-clumping-cat-litter/
│   └── ...
├── /dog-beds/                          # Category hub
│   ├── /best-dog-bed-for-large-breeds/
│   ├── /best-orthopedic-dog-bed/
│   └── ...
├── /gifts-for-dog-lovers/              # Gift guide
└── /about/                             # About/methodology
```

### Data Model

```typescript
// Content stored as Astro content collections (Markdown + frontmatter)

interface Product {
  name: string;
  brand: string;
  price: number;
  pricePerUnit?: string;      // "per lb", "per month"
  affiliateUrl: string;
  chewyUrl?: string;          // Chewy often has better commission
  amazonUrl?: string;
  image: string;
  rating: number;             // Our rating out of 5
  pros: string[];
  cons: string[];
  bestFor: string;
  ingredients?: string[];     // For food products
  verdict: string;
}

interface BestXForYPage {
  slug: string;
  title: string;
  category: string;           // "dog-food", "cat-litter"
  petType: string;            // "dog", "cat", "fish"
  metaDescription: string;
  lastUpdated: Date;
  quickAnswer: Product;
  products: Product[];
  buyingGuide: string;
  faqs: FAQ[];
}
```

### Affiliate Strategy

| Partner | Commission | Best For | Notes |
|---------|------------|----------|-------|
| **Chewy Affiliate** | 5-8% | Food, recurring purchases | Best conversion for pet products |
| **Amazon Associates** | 1-4% | Everything else | Fallback, convenience |
| **Direct Brand Programs** | 5-15% | Premium brands | Higher commission, more work |

**Link Strategy:**
- Primary CTA → Chewy (best commission + conversion for pet products)
- Secondary → Amazon (convenience, wider selection)
- Always disclose affiliate relationship
- Track which partner converts better per category

---

## 6. SEO Strategy

### Keyword Research Approach

Target format: `best [product] for [modifier]`

**High-value modifiers for pets:**
- **Conditions:** "for sensitive stomachs", "for allergies", "for joint pain"
- **Breeds/Sizes:** "for labs", "for small dogs", "for large breeds"
- **Life stages:** "for puppies", "for senior dogs", "for kittens"
- **Behaviors:** "for aggressive chewers", "for picky eaters"
- **Constraints:** "on a budget", "under $30", "grain free"

### Keyword Prioritization

| Priority | Criteria | Examples |
|----------|----------|----------|
| 1 | High volume + recurring purchase | "best dog food for sensitive stomach" |
| 2 | High volume + high ticket | "best dog bed for large breeds" |
| 3 | Medium volume + low competition | "best dog food for goldendoodles" |
| 4 | Seasonal | "best gifts for dog lovers" |

### On-Page SEO

- Title: "Best [Product] for [Modifier] (2025) | PetPicks"
- H1: "Best [Product] for [Modifier]"
- Quick answer in first 100 words
- Comparison table for featured snippets
- FAQ schema markup
- Product schema markup
- Last updated date prominently displayed

---

## 7. Implementation Plan

### Phase 1: Foundation (MVP)
- [ ] Create Astro project with Tailwind
- [ ] Build page templates (Best X for Y, Category Hub)
- [ ] Set up content collections
- [ ] Create 10 pilot pages:
  - Dog Food (5 pages)
  - Cat Litter (3 pages)
  - Dog Beds (2 pages)
- [ ] Deploy to Cloudflare Pages
- [ ] Set up Plausible analytics
- [ ] Apply for Chewy and Amazon Associates

**Exit Criteria:** 10 pages live, indexed, affiliate links working

### Phase 2: Content Expansion
- [ ] Add 20 more pages (30 total)
- [ ] Expand to Cat Food, Dog Toys
- [ ] Create category hub pages
- [ ] Internal linking optimization
- [ ] Add FAQ schema markup

**Exit Criteria:** 30 pages, 5 categories

### Phase 3: Scale & Monetize
- [ ] Add 30 more pages (60 total)
- [ ] Create gift guide pages
- [ ] Apply for direct brand programs
- [ ] Add comparison tables to all pages
- [ ] Monitor rankings, double down on winners

**Exit Criteria:** 60 pages, affiliate revenue started

### Phase 4: Optimize & Grow
- [ ] Expand to Tier 2 categories
- [ ] Target 100+ pages
- [ ] Evaluate display ads if traffic warrants
- [ ] Consider email list for deal alerts

---

## 8. Pilot Pages (Phase 1)

### Dog Food (5 pages)
1. Best Dog Food for Sensitive Stomachs
2. Best Dog Food for Large Breeds
3. Best Dog Food for Puppies
4. Best Dog Food for Senior Dogs
5. Best Grain-Free Dog Food

### Cat Litter (3 pages)
1. Best Cat Litter for Odor Control
2. Best Clumping Cat Litter
3. Best Cat Litter for Multiple Cats

### Dog Beds (2 pages)
1. Best Dog Bed for Large Breeds
2. Best Orthopedic Dog Bed for Senior Dogs

---

## 9. Revenue Projections

### Assumptions
- 60 pages at maturity
- Average 600 pageviews/month per page = 36,000 monthly pageviews
- 6% click-through to affiliate links = 2,160 clicks (pet owners click more)
- 4% conversion rate = 86 purchases (higher than general retail)
- $50 average order value
- 6% blended commission = $3 per sale

### Projections

| Phase | Pages | Pageviews | Revenue |
|-------|-------|-----------|---------|
| MVP | 10 | 6K | $50/mo |
| Phase 2 | 30 | 18K | $150/mo |
| Phase 3 | 60 | 36K | $300/mo |
| Scale | 100+ | 60K+ | $500-1K/mo |

**The multipliers:**
1. **Recurring purchases** - Dog food buyer returns monthly = LTV
2. **Higher commissions** - Direct brand programs 10-15%
3. **Display ads at scale** - Mediavine at 50K sessions adds $500-1K
4. **Compound traffic** - Top pages can get 5-10K views/month

**Realistic target:** $2-5K/month at 100K+ pageviews with mixed affiliate + ads

---

## 10. Competitive Landscape

### Existing Players

| Site | Strength | Weakness | Our Angle |
|------|----------|----------|-----------|
| **DogFoodAdvisor** | Trusted, in-depth | Dated design, slow | Better UX, faster |
| **Wirecutter Pets** | Authority | Generic, not pet-focused | Deeper niche |
| **Rover/Chewy blogs** | Built-in audience | Soft sell, not comparative | Hard recommendations |
| **Random affiliate sites** | Many exist | Thin content, sketchy | Honest, thorough |

### Our Differentiation
- **Condition-specific** - Not just "best dog food" but "best for sensitive stomach"
- **Fast, clean UX** - No popup hell, no slow loads
- **Honest cons** - Build trust by acknowledging downsides
- **Breed-specific** - "Best food for goldendoodles" (low competition)

---

## 11. Passivity Analysis

| Factor | Score | Notes |
|--------|-------|-------|
| **Content Freshness** | 8/10 | Products change, but needs don't |
| **Maintenance** | 8/10 | Update prices/availability periodically |
| **Support Burden** | 10/10 | No users, no accounts |
| **Scaling** | 8/10 | More pages = more revenue |
| **Technical** | 10/10 | Static site, no backend |

**Overall Passivity Score: 9/10**

Maintenance: Quarterly product availability checks, annual content refresh for top pages.

---

## 12. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Chewy affiliate rejection | Low | High | Apply early, have Amazon backup |
| Content doesn't rank | Medium | High | Target low-competition long-tail first |
| Products discontinued | Medium | Low | List alternatives, monitor quarterly |
| DogFoodAdvisor dominates | Medium | Medium | Go deeper on niches they ignore |

---

## 13. AI Agent Instructions

### Do
- Research actual products and ingredients
- Include specific breed/condition information
- Always list honest cons
- Use comparison tables
- Include "last updated" dates
- Optimize images (product photos matter)

### Don't
- Recommend products without research
- Ignore ingredient quality for pet food
- Forget affiliate disclosures
- Write generic content
- Skip mobile optimization

### Content Quality Standards
- Every food recommendation should consider ingredients
- Include price-per-pound or monthly cost estimates
- Note if products are available at Chewy AND Amazon
- For condition-specific pages, explain WHY certain features help

### Decisions Already Made
- Astro over Next.js (static, fast)
- Chewy as primary affiliate (better commission than Amazon for pets)
- Start with dogs/cats (highest volume), expand to aquariums later
- No user accounts (maximum passivity)

---

## 14. Session Log

### 2025-12-16 - Project Created
- Identified pet owners as underserved market with high affiliate potential
- Chose curated lists model over calculators (better fit for purchase-heavy audience)
- Named project PetPicks - "Picks for your pet"
- Created comprehensive session-start document
- Defined 4-phase implementation plan
- Selected pilot categories: Dog Food, Cat Litter, Dog Beds

---

## 15. Quick Reference

### Key Files (Once Repo Created)
```
petpicks/
├── src/
│   ├── content/
│   │   ├── dog-food/
│   │   ├── cat-food/
│   │   ├── cat-litter/
│   │   ├── dog-beds/
│   │   └── config.ts
│   ├── components/
│   │   ├── ProductCard.astro
│   │   ├── ComparisonTable.astro
│   │   ├── QuickAnswer.astro
│   │   ├── IngredientList.astro
│   │   └── AffiliateLink.astro
│   ├── layouts/
│   │   ├── BaseLayout.astro
│   │   └── BestXForYLayout.astro
│   └── pages/
│       ├── index.astro
│       ├── [category]/
│       │   └── index.astro
│       └── [...slug].astro
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

### Key Links
- Chewy Affiliate Program: https://www.chewy.com/app/content/affiliate
- Amazon Associates: https://affiliate-program.amazon.com
- Astro Docs: https://docs.astro.build

---

**Next Action:** Create petpicks repo and begin Phase 1 (Foundation)

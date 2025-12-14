# SIMMER - Session Start Document

> **Last Updated**: 2025-12-13
> **Current Phase**: Queued (After Crunch/Sift)
> **Project Repo**: Not yet created
> **Project Name**: Simmer
> **Tagline**: "Let it simmer"

---

## 1. Quick Context

**What**: A clean recipe aggregator that strips away the stories, ads, and fluff from recipe sites, presenting just the recipe with value-added features like shopping lists, scaling, and unit conversion.

**Revenue Model**: Affiliate links (Instacart, Amazon) + minimal display ads

**Why This Will Work**: Recipe sites are universally hated for their bloated content. We solve a real pain point by leveraging legally-published schema.org structured data while adding genuine value.

**Target Revenue**: $2-5K/month

**Passivity Score**: 8/10 - Automated scraping, minimal support, evergreen content

---

## 2. Full Project Vision

### What We're Building

A recipe search and aggregation platform that:
1. Indexes recipes from across the web using schema.org/Recipe structured data
2. Presents them in a clean, distraction-free format
3. Adds value through features the original sites don't offer
4. Always credits and links back to original sources

### The Problem We're Solving

Every recipe website follows the same frustrating pattern:
- 2000 words of life story before the recipe
- Aggressive popup ads
- Auto-playing videos
- "Jump to Recipe" buttons that barely work
- No way to scale ingredients
- No integrated shopping list

Users just want the recipe. We give them exactly that.

### Why It Will Succeed

1. **Universal Pain Point**: Everyone who cooks online experiences this frustration
2. **Legal & Ethical**: schema.org data is voluntarily published for indexing
3. **Clear Value-Add**: Features like shopping lists justify our existence
4. **SEO Potential**: Recipe searches are massive (billions/month)
5. **Affiliate-Friendly**: Ingredient purchases = natural affiliate opportunity
6. **Low Maintenance**: Automated scraping, no user-generated content

### Target Users

**Primary:**
- Home cooks frustrated with recipe site bloat
- Meal planners who need shopping lists
- Health-conscious cooks tracking nutrition
- International users needing unit conversion

**Secondary:**
- Professional chefs organizing recipes
- Food bloggers researching competitors
- Diet-specific searchers (keto, vegan, etc.)

### Key Differentiators

| Competitor | Their Approach | Simmer Advantage |
|------------|----------------|------------------|
| Paprika | Manual recipe saving | Auto-aggregation, no manual work |
| Copy Me That | Browser extension required | Native web experience |
| Recipe Filter | Chrome extension only | Full web app with search |
| Original Sites | Bloated, ad-heavy | Clean, focused, value-added |

### Success Metrics

| Metric | 6 Month | 12 Month |
|--------|---------|----------|
| Recipes Indexed | 500K | 2M |
| Monthly Visitors | 50K | 200K |
| Shopping List Clicks | 5K | 25K |
| Monthly Revenue | $500-1K | $2-5K |

---

## 3. Technical Architecture

### Stack Decisions (FINAL)

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Framework | **Next.js 14** | SSR for SEO, API routes for scraping |
| Database | **Supabase (PostgreSQL)** | Recipe storage, full-text search |
| Styling | **Tailwind CSS** | Rapid development, clean aesthetic |
| Hosting | **Vercel** | Easy deployment, edge functions |
| Search | **Supabase FTS** → **Meilisearch** | Start simple, upgrade if needed |
| Scraping | **Node.js + Cheerio** | schema.org extraction |
| Queue | **Supabase Edge Functions** | Background scraping jobs |
| Analytics | **Plausible** | Privacy-focused |

### Legal Compliance Strategy

**Why This Is Legal:**
1. **Recipes are not copyrightable** - Ingredient lists and basic instructions are facts
2. **schema.org is voluntary** - Sites explicitly publish structured data for indexing
3. **We add value** - Shopping lists, scaling, conversion = transformative use
4. **We credit sources** - Always link back to original

**What We DON'T Scrape:**
- Photos (copyrighted)
- Story content (creative expression)
- Unique prose in instructions (only structured data)

**Attribution Requirements:**
- Every recipe shows "From: [Original Site]" with link
- Clear disclaimer: "View original recipe for photos and full story"
- robots.txt compliance
- Respect rate limits

### Data Model

```typescript
interface Recipe {
  id: string;
  slug: string;

  // Core recipe data (from schema.org)
  name: string;
  description: string;
  ingredients: Ingredient[];
  instructions: Instruction[];

  // Metadata
  prepTime: number; // minutes
  cookTime: number;
  totalTime: number;
  servings: number;

  // Nutrition (if available)
  nutrition?: {
    calories: number;
    protein: number;
    carbs: number;
    fat: number;
    fiber: number;
  };

  // Categorization
  cuisine: string[];
  category: string[]; // breakfast, dinner, dessert
  diet: string[]; // vegan, keto, gluten-free

  // Source attribution
  sourceUrl: string;
  sourceDomain: string;
  sourceName: string;

  // Our additions
  scaleFactor: number;
  createdAt: Date;
  updatedAt: Date;
}

interface Ingredient {
  original: string; // "2 cups flour"
  parsed: {
    amount: number;
    unit: string;
    item: string;
  };
  affiliateLink?: string;
}

interface Instruction {
  step: number;
  text: string;
}
```

### URL Structure

```
simmer.recipes/ (or getsimmer.com, simmer.kitchen)
├── /                           # Homepage with search
├── /search?q=...               # Search results
├── /recipe/[slug]              # Individual recipe view
├── /category/[name]            # Category browse (dinner, dessert)
├── /cuisine/[name]             # Cuisine browse (italian, mexican)
├── /diet/[name]                # Diet filter (keto, vegan)
├── /list                       # Shopping list (localStorage)
└── /about                      # About + legal info
```

### Scraping Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Scraping Pipeline                     │
└─────────────────────────────────────────────────────────┘
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   Seed URLs     │ │  Sitemap        │ │   User Submit   │
│  (Top 100 sites)│ │  Discovery      │ │   (Future)      │
└────────┬────────┘ └────────┬────────┘ └────────┬────────┘
         │                   │                   │
         └───────────────────┼───────────────────┘
                             ▼
                  ┌─────────────────────┐
                  │    URL Queue        │
                  │  (Supabase table)   │
                  └──────────┬──────────┘
                             ▼
                  ┌─────────────────────┐
                  │   Edge Function     │
                  │   (Rate-limited)    │
                  └──────────┬──────────┘
                             ▼
                  ┌─────────────────────┐
                  │  Schema.org Parser  │
                  │  (JSON-LD extract)  │
                  └──────────┬──────────┘
                             ▼
                  ┌─────────────────────┐
                  │  Ingredient Parser  │
                  │  (NLP extraction)   │
                  └──────────┬──────────┘
                             ▼
                  ┌─────────────────────┐
                  │    PostgreSQL       │
                  │   (Supabase)        │
                  └─────────────────────┘
```

### Affiliate Integration

**Primary: Instacart**
- 3% commission on grocery orders
- "Add to Instacart" button on shopping list
- Deep linking to specific ingredients

**Secondary: Amazon Fresh / Pantry**
- Amazon Associates program
- Non-perishable ingredients
- Specialty items, equipment

**Implementation:**
```typescript
// Generate affiliate link for ingredient
function getAffiliateLink(ingredient: string): string {
  // Instacart API for groceries
  // Amazon for specialty items
  // Track clicks for analytics
}
```

---

## 4. Implementation Plan

### Phase 1: Foundation (Week 1-2)

**Deliverables:**
- [ ] Next.js project setup with Tailwind
- [ ] Supabase database schema
- [ ] Basic schema.org scraper (single URL)
- [ ] Recipe display page
- [ ] Simple search (title only)
- [ ] 100 seed recipes from 10 sites

**Definition of Done:**
- Can paste URL and extract recipe
- Can view recipe in clean format
- Basic search returns results

### Phase 2: Core Features (Week 3-4)

**Deliverables:**
- [ ] Ingredient scaling (2x, 0.5x, custom)
- [ ] Unit conversion (metric/imperial)
- [ ] Shopping list (localStorage)
- [ ] Ingredient parsing (amount, unit, item)
- [ ] Full-text search
- [ ] Category/cuisine/diet filtering

**Definition of Done:**
- Can scale any recipe
- Can toggle metric/imperial
- Can add ingredients to shopping list
- Search finds relevant recipes

### Phase 3: Scale Scraping (Week 5-6)

**Deliverables:**
- [ ] Automated sitemap discovery
- [ ] Queue-based scraping pipeline
- [ ] Rate limiting per domain
- [ ] Duplicate detection
- [ ] 50K+ recipes indexed
- [ ] robots.txt compliance

**Definition of Done:**
- Pipeline runs automatically
- Respects source site limits
- No duplicate recipes

### Phase 4: Monetization (Week 7-8)

**Deliverables:**
- [ ] Instacart affiliate integration
- [ ] Amazon Associates links
- [ ] Minimal ad placement (sidebar only)
- [ ] "Add all to cart" feature
- [ ] Click tracking/analytics

**Definition of Done:**
- Affiliate links generating clicks
- Ads displaying non-intrusively
- Revenue tracking in place

### Phase 5: Polish & Growth (Week 9+)

**Deliverables:**
- [ ] SEO optimization (recipe schema markup)
- [ ] Social sharing with preview
- [ ] Print-friendly view
- [ ] Meal planning feature (optional)
- [ ] User recipe submission (optional)
- [ ] Scale to 500K+ recipes

---

## 5. Critical Files Reference

```
simmer/
├── src/
│   ├── app/
│   │   ├── layout.tsx              # Root layout
│   │   ├── page.tsx                # Homepage with search
│   │   ├── search/
│   │   │   └── page.tsx            # Search results
│   │   ├── recipe/
│   │   │   └── [slug]/
│   │   │       └── page.tsx        # Recipe detail view
│   │   ├── category/
│   │   │   └── [name]/
│   │   │       └── page.tsx        # Category listing
│   │   ├── list/
│   │   │   └── page.tsx            # Shopping list
│   │   └── api/
│   │       ├── scrape/
│   │       │   └── route.ts        # Manual scrape endpoint
│   │       └── search/
│   │           └── route.ts        # Search API
│   ├── components/
│   │   ├── RecipeCard.tsx          # Recipe preview card
│   │   ├── RecipeView.tsx          # Full recipe display
│   │   ├── IngredientList.tsx      # Scalable ingredients
│   │   ├── Instructions.tsx        # Step-by-step view
│   │   ├── ShoppingList.tsx        # Shopping list manager
│   │   ├── ScaleControl.tsx        # Serving size adjuster
│   │   ├── UnitToggle.tsx          # Metric/imperial switch
│   │   └── SearchBar.tsx           # Search input
│   ├── lib/
│   │   ├── scraper/
│   │   │   ├── index.ts            # Main scraper
│   │   │   ├── schema-parser.ts    # JSON-LD extraction
│   │   │   └── ingredient-parser.ts # NLP ingredient parsing
│   │   ├── db/
│   │   │   ├── client.ts           # Supabase client
│   │   │   ├── recipes.ts          # Recipe CRUD
│   │   │   └── search.ts           # Search queries
│   │   ├── units.ts                # Unit conversion logic
│   │   ├── scale.ts                # Scaling calculations
│   │   └── affiliates.ts           # Affiliate link generation
│   └── store/
│       └── shopping-list.ts        # Zustand store for list
├── supabase/
│   └── migrations/
│       └── 001_initial_schema.sql  # Database schema
├── scripts/
│   ├── seed-urls.ts                # Initial URL seeding
│   └── run-scraper.ts              # Manual scraper trigger
├── tailwind.config.js
└── package.json
```

---

## 6. Context for AI Agents

### Instructions for New Sessions

1. **Read this entire document first**
2. **This project is QUEUED** - Don't start until other projects ship
3. **Check project-tracker.md** for current status
4. **Legal compliance is CRITICAL** - Always link to sources, never scrape photos
5. **Do not re-debate decided decisions**
6. **Update this document** at session end

### Decisions Already Made (DO NOT CHANGE)

- Aggregate via schema.org structured data only
- Always credit and link to original source
- No photo scraping (copyright violation)
- Stack: Next.js + Supabase + Tailwind
- Primary monetization: Affiliate links
- Minimal ads (non-intrusive)

### Open Questions (Decide Later)

- Exact affiliate program partnerships
- Whether to allow user submissions
- Meal planning feature scope
- Mobile app potential
- Premium tier features (if any)

### Common Pitfalls to Avoid

1. **Don't scrape photos** - They're copyrighted, link to original instead
2. **Don't copy story content** - Only structured recipe data
3. **Don't ignore robots.txt** - Respect crawl directives
4. **Don't hammer source sites** - Rate limit aggressively
5. **Don't skip attribution** - Always link back prominently
6. **Don't over-engineer parsing** - Start with schema.org, improve later

### Ingredient Parsing Approach

```typescript
// Start simple, improve iteratively
function parseIngredient(text: string): ParsedIngredient {
  // "2 cups all-purpose flour"
  // → { amount: 2, unit: "cups", item: "all-purpose flour" }

  // Use regex patterns first
  // Graduate to NLP library if needed (compromise, nlp.js)
}

// Common patterns to handle:
// "2 cups flour"
// "1/2 teaspoon salt"
// "3-4 cloves garlic, minced"
// "1 (14 oz) can tomatoes"
// "Salt and pepper to taste"
```

### Unit Conversion Reference

```typescript
const conversions = {
  // Volume
  cup: { ml: 236.588, tbsp: 16, tsp: 48 },
  tbsp: { ml: 14.787, tsp: 3 },
  tsp: { ml: 4.929 },

  // Weight
  oz: { g: 28.3495 },
  lb: { g: 453.592, oz: 16 },

  // Temperature
  fahrenheit: (f) => (f - 32) * 5/9, // to Celsius
  celsius: (c) => c * 9/5 + 32, // to Fahrenheit
};
```

---

## 7. Session Log

### 2025-12-13 - Initial Planning

- User presented problem: wife frustrated with recipe site bloat
- Researched legal aspects of recipe aggregation
- Confirmed: recipes not copyrightable, schema.org is fair game
- Designed full aggregator + search approach
- Named project "Simmer" - "Let it simmer"
- Created this session-start document
- Next: Begin after higher-priority projects ship

---

## Appendix: Top Recipe Sites for Seeding

### Tier 1 (High Quality schema.org)
1. AllRecipes.com
2. Food Network
3. Serious Eats
4. Bon Appetit
5. Epicurious
6. NYT Cooking (paywall - skip)
7. BBC Good Food
8. Taste of Home

### Tier 2 (Good Coverage)
9. Delish
10. Simply Recipes
11. Budget Bytes
12. Minimalist Baker
13. Cookie and Kate
14. Smitten Kitchen
15. Pioneer Woman

### Tier 3 (Niche/Diet-Specific)
16. Skinnytaste (healthy)
17. Diet Doctor (keto)
18. Oh She Glows (vegan)
19. King Arthur Baking (baking)
20. Serious Eats (technique)

### Schema.org Recipe Example

```json
{
  "@context": "https://schema.org/",
  "@type": "Recipe",
  "name": "Classic Chocolate Chip Cookies",
  "description": "Crispy on the outside, chewy on the inside.",
  "recipeIngredient": [
    "2 1/4 cups all-purpose flour",
    "1 tsp baking soda",
    "1 tsp salt",
    "1 cup butter, softened",
    "3/4 cup granulated sugar",
    "3/4 cup packed brown sugar",
    "2 large eggs",
    "2 tsp vanilla extract",
    "2 cups chocolate chips"
  ],
  "recipeInstructions": [
    {
      "@type": "HowToStep",
      "text": "Preheat oven to 375°F."
    },
    {
      "@type": "HowToStep",
      "text": "Combine flour, baking soda and salt in small bowl."
    }
  ],
  "prepTime": "PT15M",
  "cookTime": "PT12M",
  "totalTime": "PT27M",
  "recipeYield": "60 cookies",
  "nutrition": {
    "@type": "NutritionInformation",
    "calories": "110 calories"
  }
}
```

This structured data is what we extract - it's voluntarily published by sites specifically for search engines and aggregators to consume.

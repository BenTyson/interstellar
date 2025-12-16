# CRAFTCALC - Session Start Document

> **Last Updated**: 2025-12-14
> **Current Phase**: Queued
> **Project Repo**: Not yet created
> **Project Name**: CraftCalc
> **Tagline**: "Calculate your next creation"

---

## 1. Quick Context

**What**: A network of 50+ calculators for crafters - yarn, quilting, woodworking, cross stitch, resin, candle making, and more. One destination for all craft calculations.

**Revenue Model**: Affiliate links (craft stores 5-15%) + display ads

**Why This Will Work**: Passionate, engaged audience. Calculators exist but scattered across niche sites. No unified hub with modern UX.

**Target Revenue**: $500-2K/month

**Passivity Score**: 10/10 - Static calculators, loyal repeat visitors, zero maintenance

---

## 2. Full Project Vision

### What We're Building

A comprehensive calculator network for the crafting community:

- **Yarn Crafts** - Knitting, crochet yarn estimators, gauge calculators
- **Quilting & Sewing** - Fabric yardage, binding, backing calculators
- **Cross Stitch** - Fabric size, thread estimators, count converters
- **Woodworking** - Board feet, lumber costs, cut lists
- **Resin & Epoxy** - Volume, pigment ratios, mold fills
- **Candle Making** - Wax weight, fragrance loads, wick sizing
- **Soap Making** - Lye calculators, oil ratios, batch sizing
- **General Craft** - Paint coverage, bead counts, paper converters

### The Problem We're Solving

**For crafters:**
- Need to calculate materials before buying
- Want to avoid running out mid-project
- Hate wasting expensive supplies (yarn, fabric, resin)
- Current tools are scattered across different sites

**For beginners:**
- Don't know how to estimate materials
- Intimidated by craft math
- Need simple, friendly tools

### Why It Will Succeed

1. **Passionate audience** - Crafters are dedicated, engaged, repeat visitors
2. **High affiliate potential** - Craft stores pay 5-15% commission
3. **Underserved by tech** - Most craft sites are blogs, not tools
4. **Natural shopping intent** - Calculate → Buy supplies
5. **Loyal users** - Bookmark and return for every project
6. **Same proven model** - Identical to Crunch, different audience

### Target Users

**Primary:**
- Knitters and crocheters
- Quilters and sewers
- Cross stitchers and embroiderers
- Woodworkers (hobbyist)

**Secondary:**
- Resin artists
- Candle makers
- Soap makers
- General crafters and makers
- Etsy sellers (costing products)

### Key Differentiators

| Competitor | Their Focus | CraftCalc Advantage |
|------------|-------------|---------------------|
| YarnCalculator.com | Yarn only | All crafts |
| Quilter's Paradise | Quilting only | All crafts, modern UX |
| Woodworking-Calculators.com | Wood only | All crafts |
| Store calculators | Their products | Unbiased, comprehensive |

### Success Metrics

| Metric | 6 Month | 12 Month |
|--------|---------|----------|
| Calculators Live | 50 | 75 |
| Monthly Pageviews | 40K | 150K |
| Monthly Revenue | $300-600 | $1-2K |
| Return Visitor Rate | 30% | 40% |

---

## 3. Technical Architecture

### Stack Decisions (FINAL)

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Framework | **Astro** | SSG, same as portfolio |
| Styling | **Tailwind CSS** | Consistent with portfolio |
| Hosting | **Cloudflare Pages** | Free, fast |
| Analytics | **Plausible** | Privacy-focused |
| Ads | **Google AdSense** | Start simple |

### URL Structure

```
craftcalc.com/
├── /                              # Homepage with craft categories
├── /yarn/
│   ├── /yarn/yardage              # Yarn yardage estimator
│   ├── /yarn/weight-converter     # Yarn weight converter
│   ├── /yarn/gauge                # Gauge calculator
│   ├── /yarn/blanket              # Blanket yarn calculator
│   ├── /yarn/sweater              # Sweater yarn estimator
│   ├── /yarn/socks                # Sock yarn calculator
│   ├── /yarn/hat                  # Hat yarn calculator
│   └── /yarn/skein-converter      # Skein/ball converter
├── /quilting/
│   ├── /quilting/fabric           # Fabric yardage calculator
│   ├── /quilting/binding          # Binding calculator
│   ├── /quilting/backing          # Backing calculator
│   ├── /quilting/blocks           # Quilt block calculator
│   ├── /quilting/fat-quarters     # Fat quarter calculator
│   ├── /quilting/borders          # Border calculator
│   └── /quilting/batting          # Batting calculator
├── /sewing/
│   ├── /sewing/fabric             # Fabric estimator
│   ├── /sewing/seam-allowance     # Seam allowance calculator
│   ├── /sewing/pattern-resize     # Pattern resizing
│   └── /sewing/zipper             # Zipper length calculator
├── /cross-stitch/
│   ├── /cross-stitch/fabric-size  # Fabric size calculator
│   ├── /cross-stitch/thread       # Thread/floss estimator
│   ├── /cross-stitch/aida         # Aida count converter
│   ├── /cross-stitch/stitch-count # Stitch count calculator
│   └── /cross-stitch/frame        # Frame size calculator
├── /woodworking/
│   ├── /woodworking/board-feet    # Board feet calculator
│   ├── /woodworking/lumber-cost   # Lumber cost calculator
│   ├── /woodworking/plywood       # Plywood calculator
│   ├── /woodworking/stain         # Wood stain coverage
│   └── /woodworking/finish        # Finish calculator
├── /resin/
│   ├── /resin/volume              # Resin volume calculator
│   ├── /resin/pigment             # Pigment ratio calculator
│   ├── /resin/mold                # Mold fill calculator
│   └── /resin/coating             # Coating coverage calculator
├── /candles/
│   ├── /candles/wax               # Wax weight calculator
│   ├── /candles/fragrance         # Fragrance load calculator
│   ├── /candles/wick              # Wick size guide
│   ├── /candles/container         # Container fill calculator
│   └── /candles/cost              # Cost per candle calculator
├── /soap/
│   ├── /soap/lye                  # Lye calculator
│   ├── /soap/oil-ratio            # Oil ratio calculator
│   ├── /soap/batch                # Batch size calculator
│   └── /soap/cost                 # Cost calculator
└── /general/
    ├── /general/paint             # Paint coverage calculator
    ├── /general/beads             # Bead count calculator
    ├── /general/ribbon            # Ribbon/trim calculator
    └── /general/paper             # Paper size converter
```

### Calculator Component Architecture

```typescript
interface CraftCalculator {
  slug: string;
  name: string;
  description: string;
  category: CraftCategory;

  inputs: InputField[];
  calculate: (inputs: Record<string, number | string>) => CalculationResult;
  outputs: OutputField[];

  // SEO
  keywords: string[];
  relatedCalculators: string[];

  // Monetization
  affiliateLinks?: AffiliateLink[];
  supplySuggestions?: string[];
}

type CraftCategory =
  | 'yarn'
  | 'quilting'
  | 'sewing'
  | 'cross-stitch'
  | 'woodworking'
  | 'resin'
  | 'candles'
  | 'soap'
  | 'general';
```

---

## 4. Calculator Inventory

### Priority 1: Highest Volume (Build First - 15 calculators)

| Calculator | Category | Why Priority |
|------------|----------|--------------|
| Yarn yardage | Yarn | Most searched yarn calc |
| Blanket yarn | Yarn | Common project type |
| Fabric yardage | Quilting | Core quilting need |
| Binding calculator | Quilting | Complex math, high need |
| Cross stitch fabric | Cross Stitch | Essential for every project |
| Board feet | Woodworking | Industry standard calc |
| Resin volume | Resin | Expensive to get wrong |
| Wax calculator | Candles | Core candle making need |
| Lye calculator | Soap | Safety-critical calculation |
| Gauge calculator | Yarn | Every knitter needs this |
| Thread estimator | Cross Stitch | Avoid running out |
| Backing calculator | Quilting | Common question |
| Fragrance load | Candles | Key ratio |
| Paint coverage | General | Universal need |
| Lumber cost | Woodworking | Budget planning |

### Priority 2: Medium Volume (20 calculators)

| Calculator | Category |
|------------|----------|
| Sweater yarn estimator | Yarn |
| Sock yarn calculator | Yarn |
| Hat yarn calculator | Yarn |
| Weight converter | Yarn |
| Quilt block calculator | Quilting |
| Fat quarter calculator | Quilting |
| Border calculator | Quilting |
| Seam allowance | Sewing |
| Aida count converter | Cross Stitch |
| Frame size calculator | Cross Stitch |
| Plywood calculator | Woodworking |
| Stain coverage | Woodworking |
| Pigment ratio | Resin |
| Mold fill calculator | Resin |
| Wick size guide | Candles |
| Container fill | Candles |
| Oil ratio calculator | Soap |
| Batch size | Soap |
| Bead count | General |
| Ribbon calculator | General |

### Priority 3: Long Tail (15+ calculators)

| Calculator | Category |
|------------|----------|
| Skein converter | Yarn |
| Pattern resize | Sewing |
| Zipper length | Sewing |
| Stitch count | Cross Stitch |
| Finish calculator | Woodworking |
| Coating coverage | Resin |
| Cost per candle | Candles |
| Soap cost calculator | Soap |
| Paper size converter | General |
| Batting calculator | Quilting |

---

## 5. Implementation Plan

### Phase 1: Foundation + Top 15 (Week 1-2)

**Deliverables:**
- [ ] Astro project setup with Tailwind
- [ ] Base calculator component template
- [ ] Homepage with craft category grid
- [ ] Category landing pages
- [ ] 15 Priority 1 calculators:
  - Yarn: yardage, blanket, gauge
  - Quilting: fabric, binding, backing
  - Cross Stitch: fabric size, thread
  - Woodworking: board feet, lumber cost
  - Resin: volume
  - Candles: wax, fragrance
  - Soap: lye
  - General: paint

**Definition of Done:**
- Site deploys to Cloudflare Pages
- All 15 calculators functional
- Mobile responsive
- Lighthouse 90+

### Phase 2: Expand to 35 (Week 3-4)

**Deliverables:**
- [ ] 20 Priority 2 calculators
- [ ] Internal linking optimization
- [ ] Related calculators component
- [ ] Search functionality
- [ ] Print-friendly results

**Definition of Done:**
- 35 calculators live
- Full category coverage
- Strong internal linking

### Phase 3: Monetize + Polish (Week 5-6)

**Deliverables:**
- [ ] Affiliate link integration
  - Yarn stores (Jimmy Beans Wool, WEBS)
  - Fabric stores (Fat Quarter Shop)
  - Craft supplies (Amazon, Michaels)
- [ ] Google AdSense integration
- [ ] SEO optimization
- [ ] Sitemap submission

**Definition of Done:**
- Affiliate links on all calculators
- Ads displaying
- All pages indexed

### Phase 4: Scale (Week 7+)

**Deliverables:**
- [ ] Expand to 50+ calculators
- [ ] Monitor Search Console
- [ ] Add calculators based on demand
- [ ] Build email list (optional)

---

## 6. Critical Files Reference

```
craftcalc/
├── src/
│   ├── components/
│   │   ├── Calculator.astro        # Base calculator layout
│   │   ├── CalculatorForm.tsx      # Input form (React island)
│   │   ├── CalculatorResult.tsx    # Result display
│   │   ├── InputField.tsx          # Form inputs
│   │   ├── ResultCard.tsx          # Result display
│   │   ├── CategoryCard.astro      # Category preview
│   │   ├── RelatedCalcs.astro      # Related calculators
│   │   ├── AffiliateButton.astro   # Shop links
│   │   └── PrintResults.tsx        # Print-friendly output
│   ├── layouts/
│   │   ├── BaseLayout.astro        # Site-wide layout
│   │   ├── CalculatorLayout.astro  # Calculator page wrapper
│   │   └── CategoryLayout.astro    # Category listing
│   ├── pages/
│   │   ├── index.astro             # Homepage
│   │   ├── yarn/
│   │   │   ├── index.astro         # Yarn category
│   │   │   ├── yardage.astro
│   │   │   ├── blanket.astro
│   │   │   └── ...
│   │   ├── quilting/
│   │   ├── sewing/
│   │   ├── cross-stitch/
│   │   ├── woodworking/
│   │   ├── resin/
│   │   ├── candles/
│   │   ├── soap/
│   │   └── general/
│   ├── lib/
│   │   ├── calculators/            # Calculator logic
│   │   │   ├── yarn.ts
│   │   │   ├── quilting.ts
│   │   │   ├── cross-stitch.ts
│   │   │   ├── woodworking.ts
│   │   │   ├── resin.ts
│   │   │   ├── candles.ts
│   │   │   ├── soap.ts
│   │   │   └── general.ts
│   │   ├── conversions.ts          # Unit conversions
│   │   └── seo.ts                  # SEO utilities
│   └── data/
│       ├── calculators.json        # Calculator metadata
│       ├── categories.json         # Category definitions
│       └── affiliates.json         # Affiliate links
├── public/
│   ├── images/
│   │   └── categories/             # Category icons
│   └── og-images/
├── astro.config.mjs
├── tailwind.config.js
└── package.json
```

---

## 7. Context for AI Agents

### Instructions for New Sessions

1. **Read this entire document first**
2. **Check project-tracker.md** for current status
3. **Focus on friendly, approachable UX** - crafters aren't always tech-savvy
4. **Do not re-debate decided decisions**
5. **Focus on the current phase** deliverables
6. **Update this document** at session end

### Decisions Already Made (DO NOT CHANGE)

- Stack: Astro + Tailwind + Cloudflare Pages
- Multi-craft approach (not single-niche)
- No user accounts
- Affiliate + ads monetization
- Friendly, approachable design

### Open Questions (Decide Later)

- Exact domain (craftcalc.com availability)
- Specific affiliate programs to join
- Email list / newsletter
- Community features (probably not)
- Mobile app (probably not)

### Common Pitfalls to Avoid

1. **Don't make it too technical** - Use crafter-friendly language
2. **Don't forget metric/imperial** - Crafters use both
3. **Don't skip common yarn weights** - Include fingering, DK, worsted, bulky
4. **Don't ignore mobile** - Many crafters use phones
5. **Don't over-complicate** - Simple inputs, clear outputs
6. **Don't forget seam allowances** - Critical for sewing/quilting

### Craft-Specific Notes

**Yarn:**
- Yarn weights: Lace (0), Fingering (1), Sport (2), DK (3), Worsted (4), Bulky (5), Super Bulky (6)
- Always account for gauge variations
- Suggest 10-15% extra for safety

**Quilting:**
- Fat quarter = 18" x 22"
- Standard binding is cut 2.5" wide
- Backing needs 4-6" extra on all sides

**Cross Stitch:**
- Aida counts: 11, 14, 16, 18 (most common)
- Higher count = smaller stitches
- Add 3" margin for framing

**Woodworking:**
- Board foot = 1" x 12" x 12"
- Account for kerf (saw blade width)
- Hardwood vs softwood pricing differs

**Resin:**
- Always mix by volume, not weight
- Account for 2:1 or 1:1 ratios depending on brand
- Over-estimate slightly (better to have extra)

**Candles:**
- Fragrance load typically 6-10% of wax weight
- Wax has different densities (soy vs paraffin)
- Wick size depends on container diameter

**Soap:**
- Lye calculations are SAFETY CRITICAL
- Always use a lye discount (5-8%)
- Different oils have different SAP values

---

## 8. Session Log

### 2025-12-14 - Initial Planning

- Researched craft calculator landscape
- Identified opportunity for unified craft calculator hub
- Named project "CraftCalc"
- Created this session-start document
- Next: Begin development or queue behind other projects

---

## Appendix: Affiliate Programs

### Yarn & Fiber

| Store | Commission | Notes |
|-------|------------|-------|
| Jimmy Beans Wool | 5-8% | Popular, good selection |
| WEBS | 5% | Large inventory |
| LoveCrafts | 8% | International |
| KnitPicks | 5% | Budget-friendly |
| Amazon | 1-4% | Broad selection |

### Fabric & Quilting

| Store | Commission | Notes |
|-------|------------|-------|
| Fat Quarter Shop | 8% | Leading quilting store |
| Fabric.com | 5% | Large selection |
| Joann | 4-8% | Mass market |
| Missouri Star | 5% | Popular quilting |

### General Craft

| Store | Commission | Notes |
|-------|------------|-------|
| Amazon | 1-4% | Everything |
| Michaels | 2-4% | General craft |
| Hobby Lobby | 3-5% | General craft |
| Blick Art | 5-10% | Art supplies |

### Specialty

| Store | Commission | Notes |
|-------|------------|-------|
| Rockler | 4-8% | Woodworking |
| Woodcraft | 5% | Woodworking |
| CandleScience | 5% | Candle supplies |
| Bramble Berry | 5% | Soap supplies |

---

## Appendix: Sample Formulas

### Yarn Yardage (Blanket)

```typescript
// Standard yarn requirements per square inch at different gauges
const yarnPerSquareInch = {
  fingering: 2.5,  // yards
  sport: 2.0,
  dk: 1.5,
  worsted: 1.2,
  bulky: 0.9,
  superBulky: 0.7,
};

function calculateBlanketYarn(
  width: number,  // inches
  height: number,
  weight: YarnWeight
): number {
  const squareInches = width * height;
  const baseYards = squareInches * yarnPerSquareInch[weight];
  const withBuffer = baseYards * 1.15; // 15% buffer
  return Math.ceil(withBuffer);
}
```

### Quilting Binding

```typescript
function calculateBinding(
  quiltWidth: number,  // inches
  quiltHeight: number,
  bindingWidth: number = 2.5,  // cut width
  fabricWidth: number = 42     // usable fabric width
): { totalLength: number; stripsNeeded: number; fabricYards: number } {
  const perimeter = (quiltWidth + quiltHeight) * 2;
  const totalLength = perimeter + 12; // extra for corners and joining

  const stripsNeeded = Math.ceil(totalLength / fabricWidth);
  const fabricInches = stripsNeeded * bindingWidth;
  const fabricYards = fabricInches / 36;

  return {
    totalLength,
    stripsNeeded,
    fabricYards: Math.ceil(fabricYards * 8) / 8, // round to 1/8 yard
  };
}
```

### Cross Stitch Fabric Size

```typescript
function calculateFabricSize(
  stitchesWide: number,
  stitchesHigh: number,
  fabricCount: number,  // e.g., 14 for 14-count Aida
  margin: number = 3    // inches on each side
): { width: number; height: number } {
  const stitchedWidth = stitchesWide / fabricCount;
  const stitchedHeight = stitchesHigh / fabricCount;

  return {
    width: Math.ceil(stitchedWidth + (margin * 2)),
    height: Math.ceil(stitchedHeight + (margin * 2)),
  };
}
```

### Resin Volume

```typescript
function calculateResinVolume(
  length: number,   // inches
  width: number,
  depth: number,
  shape: 'rectangle' | 'circle' = 'rectangle'
): { ounces: number; cups: number } {
  let cubicInches: number;

  if (shape === 'rectangle') {
    cubicInches = length * width * depth;
  } else {
    // Circle: length is diameter
    const radius = length / 2;
    cubicInches = Math.PI * radius * radius * depth;
  }

  const ounces = cubicInches * 0.554; // fl oz per cubic inch
  const cups = ounces / 8;

  return {
    ounces: Math.ceil(ounces * 1.1), // 10% buffer
    cups: Math.ceil(cups * 10) / 10,
  };
}
```

### Candle Wax Weight

```typescript
function calculateWaxWeight(
  containerVolume: number,  // fluid ounces
  fragrancePercent: number = 8
): { waxOunces: number; fragranceOunces: number } {
  // Soy wax weighs ~7.5 oz per 8 fl oz
  const waxWeight = containerVolume * 0.9375;
  const fragranceWeight = waxWeight * (fragrancePercent / 100);

  return {
    waxOunces: Math.ceil(waxWeight * 10) / 10,
    fragranceOunces: Math.ceil(fragranceWeight * 10) / 10,
  };
}
```

### Soap Lye (Cold Process)

```typescript
// SAP values (amount of lye to saponify 1g of oil)
const sapValues = {
  oliveoil: 0.134,
  coconutoil: 0.178,
  palmoil: 0.141,
  shea: 0.128,
  castor: 0.128,
};

function calculateLye(
  oils: { type: keyof typeof sapValues; grams: number }[],
  lyeDiscount: number = 5  // percent
): { lyeGrams: number; waterGrams: number } {
  let totalLye = 0;
  let totalOil = 0;

  for (const oil of oils) {
    totalLye += oil.grams * sapValues[oil.type];
    totalOil += oil.grams;
  }

  // Apply lye discount (for skin-safe soap)
  const discountedLye = totalLye * (1 - lyeDiscount / 100);

  // Water is typically 2:1 ratio to lye (33% lye concentration)
  const water = discountedLye * 2;

  return {
    lyeGrams: Math.ceil(discountedLye),
    waterGrams: Math.ceil(water),
  };
}
```

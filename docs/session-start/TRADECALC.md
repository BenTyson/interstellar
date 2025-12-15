# TRADECALC - Session Start Document

> **Last Updated**: 2025-12-14
> **Current Phase**: Queued
> **Project Repo**: Not yet created
> **Project Name**: TradeCalc
> **Tagline**: "The contractor's calculator"

---

## 1. Quick Context

**What**: A network of 50+ construction and trade calculators - concrete, roofing, electrical, HVAC, landscaping, and more. Built for contractors, tradespeople, and DIYers.

**Revenue Model**: Display ads (premium rates) + affiliate links (Home Depot, Lowe's, Amazon) + lead gen potential

**Why This Will Work**: Massive search volume, underserved market, terrible existing UX. Trades are ignored by tech but represent huge, valuable traffic.

**Target Revenue**: $2-8K/month (higher ceiling due to premium ad rates)

**Passivity Score**: 10/10 - Static calculators, math doesn't change, zero maintenance

---

## 2. Full Project Vision

### What We're Building

A comprehensive calculator network for the construction and trades industry:

- **Concrete & Masonry** - Volume, bags, blocks, rebar, mortar
- **Landscaping** - Mulch, gravel, pavers, sod, fencing
- **Roofing** - Area, pitch, shingles, metal, underlayment
- **Electrical** - Load, wire sizing, voltage drop, conduit
- **HVAC** - BTU load, duct sizing, tonnage
- **Framing** - Deck boards, stairs, joists, lumber
- **Drywall & Paint** - Sheets, joint compound, gallons
- **Plumbing** - Pipe sizing, water heater, flow rates

### The Problem We're Solving

**For contractors:**
- Need quick estimates on job sites
- Existing tools are clunky or buried in supplier sites
- Want accuracy without pulling out the manual

**For DIYers:**
- Trying to figure out how much material to buy
- Don't want to over-order or make extra trips
- Need to verify contractor quotes

**For homeowners:**
- Getting quotes from contractors
- Want to sanity-check the numbers
- Planning project budgets

### Why It Will Succeed

1. **Massive search volume** - "concrete calculator" alone is 100K+ monthly searches
2. **Premium ad rates** - Construction/home improvement CPMs are $10-30
3. **Underserved market** - Big tech ignores blue collar, existing tools have bad UX
4. **Same proven model** - Identical playbook to Crunch, different audience
5. **Evergreen content** - Math formulas don't change
6. **Lead gen upside** - Contractors pay $20-100+ per lead

### Target Users

**Primary:**
- General contractors
- Specialty contractors (roofers, electricians, HVAC, plumbers)
- Carpenters and framers
- Landscapers

**Secondary:**
- DIY homeowners
- Property managers
- Home inspectors
- Architecture/engineering students

### Key Differentiators

| Competitor | Their Weakness | TradeCalc Advantage |
|------------|----------------|---------------------|
| Calculator.net | Dated design, generic | Trade-focused, modern UX |
| Inch Calculator | Cluttered, ad-heavy | Clean, fast, mobile-first |
| Home Depot | Sales-focused, limited | Comprehensive, neutral |
| Omni Calculator | Not trade-specific | Built for job sites |
| Supplier calculators | Biased to products | Independent, trustworthy |

### Success Metrics

| Metric | 6 Month | 12 Month |
|--------|---------|----------|
| Calculators Live | 50 | 80 |
| Monthly Pageviews | 75K | 300K |
| Monthly Revenue | $500-1K | $2-5K |
| Avg Session Duration | 2 min | 2.5 min |

---

## 3. Technical Architecture

### Stack Decisions (FINAL)

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Framework | **Astro** | SSG, same as Crunch, proven |
| Styling | **Tailwind CSS** | Consistent with portfolio |
| Hosting | **Cloudflare Pages** | Free, fast, edge-hosted |
| Analytics | **Plausible** | Privacy-focused |
| Ads | **Google AdSense** → Mediavine | Premium rates for construction |

### URL Structure

```
tradecalc.com/
├── /                              # Homepage with trade categories
├── /concrete/
│   ├── /concrete/volume           # Concrete volume (slabs, footings)
│   ├── /concrete/bags             # Bags needed (60lb, 80lb)
│   ├── /concrete/footings         # Footing calculator
│   ├── /concrete/columns          # Column/post calculator
│   ├── /concrete/steps            # Stair calculator
│   └── /concrete/cost             # Cost estimator
├── /masonry/
│   ├── /masonry/blocks            # CMU block calculator
│   ├── /masonry/bricks            # Brick calculator
│   ├── /masonry/mortar            # Mortar calculator
│   └── /masonry/rebar             # Rebar calculator
├── /landscaping/
│   ├── /landscaping/mulch         # Mulch calculator
│   ├── /landscaping/gravel        # Gravel/stone calculator
│   ├── /landscaping/topsoil       # Topsoil calculator
│   ├── /landscaping/sod           # Sod calculator
│   ├── /landscaping/pavers        # Paver calculator
│   ├── /landscaping/retaining-wall # Retaining wall calculator
│   └── /landscaping/fence         # Fence calculator
├── /roofing/
│   ├── /roofing/area              # Roof area calculator
│   ├── /roofing/pitch             # Roof pitch calculator
│   ├── /roofing/shingles          # Shingle calculator
│   ├── /roofing/metal             # Metal roofing calculator
│   └── /roofing/underlayment      # Underlayment calculator
├── /electrical/
│   ├── /electrical/load           # Electrical load calculator
│   ├── /electrical/wire-size      # Wire sizing calculator
│   ├── /electrical/voltage-drop   # Voltage drop calculator
│   ├── /electrical/conduit        # Conduit fill calculator
│   └── /electrical/breaker        # Breaker sizing calculator
├── /hvac/
│   ├── /hvac/load                 # HVAC load (BTU) calculator
│   ├── /hvac/duct-size            # Duct sizing calculator
│   ├── /hvac/tonnage              # AC tonnage calculator
│   └── /hvac/cfm                  # CFM calculator
├── /plumbing/
│   ├── /plumbing/pipe-size        # Pipe sizing calculator
│   ├── /plumbing/water-heater     # Water heater sizing
│   ├── /plumbing/flow-rate        # Flow rate calculator
│   └── /plumbing/drain            # Drain sizing calculator
├── /framing/
│   ├── /framing/deck              # Deck board calculator
│   ├── /framing/stairs            # Stair rise/run calculator
│   ├── /framing/joists            # Joist span calculator
│   ├── /framing/lumber            # Lumber calculator
│   ├── /framing/plywood           # Plywood/OSB calculator
│   └── /framing/studs             # Wall stud calculator
├── /drywall/
│   ├── /drywall/sheets            # Drywall sheet calculator
│   ├── /drywall/compound          # Joint compound calculator
│   └── /drywall/tape              # Tape calculator
├── /paint/
│   ├── /paint/gallons             # Paint calculator
│   ├── /paint/coverage            # Coverage calculator
│   └── /paint/primer              # Primer calculator
└── /general/
    ├── /general/square-footage    # Square footage calculator
    ├── /general/cubic-yards       # Cubic yard calculator
    ├── /general/material-cost     # Material cost estimator
    └── /general/labor-cost        # Labor cost calculator
```

### Calculator Component Architecture

```typescript
interface Calculator {
  slug: string;
  name: string;
  description: string;
  category: Category;

  // Input fields
  inputs: InputField[];

  // Calculation logic
  calculate: (inputs: Record<string, number>) => CalculationResult;

  // Output display
  outputs: OutputField[];

  // SEO
  keywords: string[];
  relatedCalculators: string[];

  // Monetization
  affiliateLinks?: AffiliateLink[];
  leadGenCTA?: boolean;
}

interface InputField {
  name: string;
  label: string;
  type: 'number' | 'select' | 'radio';
  unit?: string;
  options?: { value: string; label: string }[];
  defaultValue?: number;
  min?: number;
  max?: number;
  step?: number;
  helpText?: string;
}

interface CalculationResult {
  primary: { label: string; value: number; unit: string };
  secondary?: { label: string; value: number; unit: string }[];
  breakdown?: { label: string; value: number; unit: string }[];
}

interface OutputField {
  label: string;
  key: string;
  unit: string;
  format: 'number' | 'currency' | 'decimal';
  decimals?: number;
}
```

### Example Calculator: Concrete Volume

```typescript
const concreteVolumeCalculator: Calculator = {
  slug: 'concrete/volume',
  name: 'Concrete Volume Calculator',
  description: 'Calculate cubic yards of concrete needed for slabs, footings, and columns.',
  category: 'concrete',

  inputs: [
    {
      name: 'shape',
      label: 'Shape',
      type: 'select',
      options: [
        { value: 'slab', label: 'Rectangular Slab' },
        { value: 'footing', label: 'Footing' },
        { value: 'column', label: 'Round Column' },
      ],
    },
    { name: 'length', label: 'Length', type: 'number', unit: 'feet' },
    { name: 'width', label: 'Width', type: 'number', unit: 'feet' },
    { name: 'depth', label: 'Depth/Thickness', type: 'number', unit: 'inches' },
  ],

  calculate: (inputs) => {
    const { length, width, depth } = inputs;
    const cubicFeet = length * width * (depth / 12);
    const cubicYards = cubicFeet / 27;
    const bags60lb = Math.ceil(cubicFeet * 2.2); // ~0.45 cu ft per 60lb bag
    const bags80lb = Math.ceil(cubicFeet * 1.65); // ~0.6 cu ft per 80lb bag

    return {
      primary: { label: 'Concrete Needed', value: cubicYards, unit: 'cubic yards' },
      secondary: [
        { label: '60lb Bags', value: bags60lb, unit: 'bags' },
        { label: '80lb Bags', value: bags80lb, unit: 'bags' },
        { label: 'Cubic Feet', value: cubicFeet, unit: 'cu ft' },
      ],
    };
  },

  outputs: [
    { label: 'Cubic Yards', key: 'cubicYards', unit: 'yd³', format: 'decimal', decimals: 2 },
    { label: '60lb Bags Needed', key: 'bags60', unit: 'bags', format: 'number' },
    { label: '80lb Bags Needed', key: 'bags80', unit: 'bags', format: 'number' },
  ],

  keywords: ['concrete calculator', 'concrete volume', 'cubic yards concrete', 'how much concrete'],
  relatedCalculators: ['concrete/bags', 'concrete/footings', 'concrete/cost'],

  affiliateLinks: [
    { store: 'Home Depot', product: 'Quikrete 80lb', url: '...' },
    { store: 'Lowes', product: 'Sakrete 60lb', url: '...' },
  ],
};
```

---

## 4. Calculator Inventory

### Priority 1: Highest Volume (Build First - 15 calculators)

| Calculator | Category | Est. Monthly Searches |
|------------|----------|----------------------|
| Concrete volume | Concrete | 100K+ |
| Concrete bags | Concrete | 50K+ |
| Mulch calculator | Landscaping | 50K+ |
| Gravel calculator | Landscaping | 40K+ |
| Roofing calculator | Roofing | 40K+ |
| Fence calculator | Landscaping | 30K+ |
| Paint calculator | Paint | 30K+ |
| Deck board calculator | Framing | 25K+ |
| Drywall calculator | Drywall | 20K+ |
| HVAC load calculator | HVAC | 20K+ |
| Square footage | General | 50K+ |
| Cubic yard calculator | General | 30K+ |
| Roof pitch calculator | Roofing | 20K+ |
| Electrical load calculator | Electrical | 15K+ |
| Paver calculator | Landscaping | 15K+ |

### Priority 2: Medium Volume (20 calculators)

| Calculator | Category |
|------------|----------|
| Stair calculator | Framing |
| Block/CMU calculator | Masonry |
| Brick calculator | Masonry |
| Shingle calculator | Roofing |
| Wire size calculator | Electrical |
| Voltage drop calculator | Electrical |
| Duct sizing calculator | HVAC |
| Topsoil calculator | Landscaping |
| Sod calculator | Landscaping |
| Retaining wall calculator | Landscaping |
| Joist span calculator | Framing |
| Lumber calculator | Framing |
| Stud calculator | Framing |
| Plywood calculator | Framing |
| Mortar calculator | Masonry |
| Rebar calculator | Masonry |
| Pipe sizing calculator | Plumbing |
| Water heater sizing | Plumbing |
| Joint compound calculator | Drywall |
| Material cost estimator | General |

### Priority 3: Long Tail (15+ calculators)

| Calculator | Category |
|------------|----------|
| Concrete footing calculator | Concrete |
| Concrete column calculator | Concrete |
| Concrete step calculator | Concrete |
| Metal roofing calculator | Roofing |
| Underlayment calculator | Roofing |
| Conduit fill calculator | Electrical |
| Breaker sizing calculator | Electrical |
| AC tonnage calculator | HVAC |
| CFM calculator | HVAC |
| Flow rate calculator | Plumbing |
| Drain sizing calculator | Plumbing |
| Primer calculator | Paint |
| Tape calculator | Drywall |
| Labor cost calculator | General |
| Concrete cost calculator | Concrete |

---

## 5. Implementation Plan

### Phase 1: Foundation + Top 15 (Week 1-2)

**Deliverables:**
- [ ] Astro project setup with Tailwind
- [ ] Base calculator component template
- [ ] Homepage with category grid
- [ ] Calculator page layout
- [ ] 15 Priority 1 calculators:
  - Concrete volume, Concrete bags
  - Mulch, Gravel, Pavers, Fence
  - Roofing area, Roof pitch
  - Paint, Drywall sheets
  - HVAC load, Electrical load
  - Square footage, Cubic yards
  - Deck boards

**Definition of Done:**
- Site deploys to Cloudflare Pages
- All 15 calculators functional and accurate
- Mobile responsive
- Lighthouse 90+

### Phase 2: Expand to 35 (Week 3-4)

**Deliverables:**
- [ ] 20 Priority 2 calculators
- [ ] Category landing pages
- [ ] Internal linking optimization
- [ ] Search functionality
- [ ] Related calculators component
- [ ] Print-friendly results

**Definition of Done:**
- 35 calculators live
- Full category coverage
- Strong internal linking

### Phase 3: Monetize + Polish (Week 5-6)

**Deliverables:**
- [ ] Google AdSense integration
- [ ] Affiliate links (Home Depot, Lowe's, Amazon)
- [ ] SEO optimization (meta, schema)
- [ ] Sitemap submission
- [ ] Lead gen CTA testing
- [ ] 15 Priority 3 calculators (50 total)

**Definition of Done:**
- Ads displaying
- Affiliate links tracking
- All pages indexed

### Phase 4: Scale (Week 7+)

**Deliverables:**
- [ ] Expand to 80+ calculators
- [ ] Monitor Search Console for opportunities
- [ ] Explore lead gen partnerships
- [ ] Add regional variations (metric system)
- [ ] Consider contractor directory add-on

---

## 6. Critical Files Reference

```
tradecalc/
├── src/
│   ├── components/
│   │   ├── Calculator.astro        # Base calculator layout
│   │   ├── CalculatorForm.tsx      # Input form (React island)
│   │   ├── CalculatorResult.tsx    # Result display
│   │   ├── InputField.tsx          # Form input component
│   │   ├── ResultCard.tsx          # Single result display
│   │   ├── RelatedCalcs.astro      # Related calculators
│   │   ├── CategoryCard.astro      # Category preview card
│   │   ├── AffiliateLink.astro     # Affiliate button
│   │   └── PrintResults.tsx        # Print-friendly output
│   ├── layouts/
│   │   ├── BaseLayout.astro        # Site-wide layout
│   │   ├── CalculatorLayout.astro  # Calculator page wrapper
│   │   └── CategoryLayout.astro    # Category listing wrapper
│   ├── pages/
│   │   ├── index.astro             # Homepage
│   │   ├── concrete/
│   │   │   ├── index.astro         # Concrete category
│   │   │   ├── volume.astro        # Volume calculator
│   │   │   ├── bags.astro          # Bags calculator
│   │   │   └── ...
│   │   ├── landscaping/
│   │   ├── roofing/
│   │   ├── electrical/
│   │   ├── hvac/
│   │   ├── plumbing/
│   │   ├── framing/
│   │   ├── drywall/
│   │   ├── paint/
│   │   └── general/
│   ├── lib/
│   │   ├── calculators/            # Calculator logic (pure functions)
│   │   │   ├── concrete.ts
│   │   │   ├── landscaping.ts
│   │   │   ├── roofing.ts
│   │   │   ├── electrical.ts
│   │   │   ├── hvac.ts
│   │   │   └── ...
│   │   ├── conversions.ts          # Unit conversions
│   │   ├── formulas.ts             # Common formulas
│   │   └── seo.ts                  # SEO utilities
│   └── data/
│       ├── calculators.json        # Calculator metadata
│       ├── categories.json         # Category definitions
│       └── affiliates.json         # Affiliate link data
├── public/
│   ├── images/
│   │   └── categories/             # Category icons
│   └── og-images/                  # Social share images
├── astro.config.mjs
├── tailwind.config.js
└── package.json
```

---

## 7. Context for AI Agents

### Instructions for New Sessions

1. **Read this entire document first**
2. **Check project-tracker.md** for current status
3. **Accuracy is critical** - These calculators must be mathematically correct
4. **Do not re-debate decided decisions**
5. **Focus on the current phase** deliverables
6. **Update this document** at session end

### Decisions Already Made (DO NOT CHANGE)

- Stack: Astro + Tailwind + Cloudflare Pages (same as Crunch)
- Calculator-first approach (not a contractor directory)
- No user accounts for MVP
- Ad + affiliate monetization
- Static site, all calculations client-side

### Open Questions (Decide Later)

- Exact domain (tradecalc.com availability)
- Lead gen partnership specifics
- Metric/imperial toggle (probably yes)
- Contractor directory add-on (maybe later)
- Mobile app (probably not needed)

### Common Pitfalls to Avoid

1. **Don't get formulas wrong** - Verify all calculations against industry standards
2. **Don't forget units** - Construction uses feet/inches/yards, be consistent
3. **Don't over-complicate inputs** - Keep forms simple and fast
4. **Don't skip mobile** - Contractors use phones on job sites
5. **Don't ignore print** - Results should print cleanly
6. **Don't forget waste factors** - Most materials need 10-15% extra

### Industry Standards Reference

**Concrete:**
- 1 cubic yard = 27 cubic feet
- 60lb bag ≈ 0.45 cubic feet
- 80lb bag ≈ 0.60 cubic feet
- Add 10% for waste

**Roofing:**
- 1 square = 100 square feet
- Standard shingle bundle covers ~33 sq ft
- 3 bundles per square

**Drywall:**
- Standard sheet: 4' x 8' = 32 sq ft
- Add 10-15% for waste and cuts

**Paint:**
- 1 gallon covers ~350-400 sq ft (one coat)
- Two coats typical

**Mulch:**
- 1 cubic yard covers ~100 sq ft at 3" depth
- 1 cubic yard = 27 cubic feet

**Electrical:**
- NEC code references for wire sizing
- Voltage drop should be <3% for branch circuits

---

## 8. Session Log

### 2025-12-14 - Initial Planning

- Researched trades/construction calculator landscape
- Identified massive search volume opportunity
- Analyzed competitors (Calculator.net, Inch Calculator, etc.)
- Named project "TradeCalc"
- Created this session-start document
- Next: Begin development or queue behind other projects

---

## Appendix: Competitor Analysis

### Calculator.net
- **Strengths**: High domain authority, comprehensive
- **Weaknesses**: Dated design, generic feel, not trade-focused
- **Traffic**: Millions monthly across all calculators

### Inch Calculator
- **Strengths**: Good coverage, decent content
- **Weaknesses**: Cluttered UI, ad-heavy, slow
- **Traffic**: High - ranks well for many terms

### Omni Calculator
- **Strengths**: Modern design, good UX
- **Weaknesses**: Not trade-specific, academic feel
- **Traffic**: High - broad calculator site

### Home Depot / Lowe's
- **Strengths**: Brand trust, buying integration
- **Weaknesses**: Limited calculators, sales-focused
- **Traffic**: Massive but not calculator-focused

### Our Positioning
"The contractor's calculator" - fast, accurate, mobile-first, built for the job site. No BS, no signup, just results.

---

## Appendix: Affiliate Programs

### Home Depot
- Commission: 2-8% depending on category
- Cookie: 1 day (short!)
- Good for: Power tools, materials

### Lowe's
- Commission: 2-4%
- Cookie: 1 day
- Good for: Materials, appliances

### Amazon
- Commission: 1-4% (tools category)
- Cookie: 24 hours
- Good for: Hand tools, safety equipment

### Specialty Suppliers
- Research: Toolbarn, Acme Tools, etc.
- Often better commissions than big box
- More relevant to professional contractors

---

## Appendix: Lead Gen Potential

### Contractor Lead Services
- **HomeAdvisor/Angi**: Pay per lead model
- **Thumbtack**: Contractor marketplace
- **Porch**: Home service leads

### How It Would Work
1. User calculates concrete needed
2. CTA: "Get quotes from local concrete contractors"
3. Lead form collects: name, email, phone, zip, project details
4. Sell lead to contractor networks

### Revenue Potential
- Concrete/roofing leads: $20-50 each
- HVAC leads: $50-100 each
- Electrical leads: $30-60 each
- At 1% conversion on 100K visits = 1000 leads/month = $20-50K potential

This is the big upside - calculators are the traffic engine, leads are the money machine.

---

## Appendix: Sample Formulas

### Concrete Volume
```typescript
// Rectangular slab
cubicYards = (length_ft * width_ft * (depth_in / 12)) / 27

// Round column
cubicYards = (Math.PI * (radius_ft ** 2) * height_ft) / 27

// Add 10% waste factor
totalNeeded = cubicYards * 1.10
```

### Mulch Coverage
```typescript
// Depth in inches, area in square feet
cubicYards = (area_sqft * (depth_in / 12)) / 27

// Coverage per cubic yard at different depths
// 2" depth: 162 sq ft per cubic yard
// 3" depth: 108 sq ft per cubic yard
// 4" depth: 81 sq ft per cubic yard
```

### Roof Area
```typescript
// For pitched roofs
roofArea = footprint_sqft * pitchMultiplier[pitch]

// Pitch multipliers (approximate)
// 4/12: 1.054
// 5/12: 1.083
// 6/12: 1.118
// 8/12: 1.202
// 10/12: 1.302
// 12/12: 1.414
```

### Paint Coverage
```typescript
// Wall area minus windows/doors
paintableArea = (perimeter_ft * height_ft) - windowArea - doorArea

// Gallons needed (350 sq ft per gallon, 2 coats)
gallons = Math.ceil((paintableArea * 2) / 350)
```

### Electrical Load (Simplified)
```typescript
// General lighting: 3 VA per sq ft
// Small appliance circuits: 1500 VA each (min 2)
// Laundry circuit: 1500 VA
// Add specific appliance loads

totalVA = (sqft * 3) + (smallApplianceCircuits * 1500) + 1500 + applianceLoads
amps = totalVA / 240 // For 240V service
```

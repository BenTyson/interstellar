# SEO Checklist & Playbook

> Technical and content SEO best practices for passive income projects. Reference when building for organic traffic.

---

## Pre-Launch Checklist

### Technical Foundation

- [ ] **HTTPS enabled** - Required for rankings
- [ ] **Mobile responsive** - Mobile-first indexing
- [ ] **Fast load times** - Target <2.5s LCP
- [ ] **XML sitemap** - `/sitemap.xml` or `/sitemap-index.xml`
- [ ] **Robots.txt** - `/robots.txt` with sitemap reference
- [ ] **Canonical URLs** - Prevent duplicate content
- [ ] **404 page** - Custom, helpful error page
- [ ] **Clean URLs** - `/tool-name` not `/page?id=123`

### Google Search Console Setup

- [ ] **Verify ownership** - DNS or HTML verification
- [ ] **Submit sitemap** - Point to sitemap URL
- [ ] **Request indexing** - For key pages
- [ ] **Check coverage** - Review excluded pages

### Analytics Setup

- [ ] **Google Analytics** or **Plausible/Umami**
- [ ] **Goal tracking** - Conversions, signups
- [ ] **UTM parameters** - Track traffic sources

---

## On-Page SEO Checklist

### Every Page Must Have

```html
<!-- Title Tag: 50-60 characters -->
<title>Primary Keyword - Secondary | Brand</title>

<!-- Meta Description: 150-160 characters -->
<meta name="description" content="Compelling description with keyword">

<!-- Canonical URL -->
<link rel="canonical" href="https://example.com/page-url">

<!-- Open Graph -->
<meta property="og:title" content="Page Title">
<meta property="og:description" content="Description">
<meta property="og:image" content="https://example.com/og-image.jpg">
<meta property="og:url" content="https://example.com/page-url">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Page Title">
<meta name="twitter:description" content="Description">
<meta name="twitter:image" content="https://example.com/twitter-image.jpg">
```

### Content Structure

```html
<!-- One H1 per page with primary keyword -->
<h1>Freelancer Tax Calculator - Estimate Your Quarterly Taxes</h1>

<!-- H2s for major sections -->
<h2>How to Calculate Quarterly Estimated Taxes</h2>
<h2>Self-Employment Tax Explained</h2>

<!-- H3s for subsections -->
<h3>Federal vs State Taxes</h3>

<!-- Keyword-rich paragraphs -->
<p>This <strong>freelancer tax calculator</strong> helps you estimate...</p>
```

### Internal Linking

- [ ] Every page links to 3-5 related pages
- [ ] Use descriptive anchor text (not "click here")
- [ ] Category/hub pages link to all child pages
- [ ] Child pages link back to category/hub

---

## Schema Markup

### WebApplication (for tools/calculators)

```json
{
  "@context": "https://schema.org",
  "@type": "WebApplication",
  "name": "Freelancer Tax Calculator",
  "description": "Calculate your quarterly estimated taxes as a freelancer",
  "url": "https://calcverse.com/freelance/tax-calculator",
  "applicationCategory": "FinanceApplication",
  "operatingSystem": "Any",
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "USD"
  }
}
```

### FAQPage (for featured snippets)

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "How do I calculate quarterly taxes?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "To calculate quarterly taxes, estimate your annual income..."
      }
    }
  ]
}
```

### SoftwareApplication (for tools)

```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "AI Tool Directory",
  "applicationCategory": "BusinessApplication",
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.8",
    "ratingCount": "1024"
  }
}
```

---

## Core Web Vitals Targets

| Metric | Good | Needs Work | Poor |
|--------|------|------------|------|
| **LCP** (Largest Contentful Paint) | <2.5s | 2.5-4s | >4s |
| **INP** (Interaction to Next Paint) | <200ms | 200-500ms | >500ms |
| **CLS** (Cumulative Layout Shift) | <0.1 | 0.1-0.25 | >0.25 |

### How to Achieve Good CWV

1. **Optimize images**: WebP format, lazy loading, explicit dimensions
2. **Minimize JS**: Code split, defer non-critical
3. **Preload fonts**: Font-display: swap
4. **Reserve space**: Explicit width/height for dynamic content
5. **Edge caching**: Use CDN (Cloudflare, Vercel)

---

## Keyword Research Process

### Step 1: Seed Keywords

Start with broad terms related to your niche:
- "freelancer tax"
- "youtube calculator"
- "ai tool comparison"

### Step 2: Expand with Tools

**Free Tools:**
- Google Keyword Planner
- Ubersuggest (limited free)
- Google Autocomplete
- "People Also Ask" boxes
- Related Searches

**Paid Tools:**
- Ahrefs
- SEMrush
- Moz

### Step 3: Evaluate Keywords

| Factor | Ideal | Avoid |
|--------|-------|-------|
| **Search Volume** | 500-5000/mo | <100 or >50K |
| **Keyword Difficulty** | <30 | >50 for new sites |
| **Search Intent** | Transactional/Informational | Navigational |
| **Competition** | Few quality results | Major brands dominating |

### Step 4: Prioritize

```
Priority Score = (Search Volume × Intent Match) / Difficulty

Example:
- "freelancer quarterly tax calculator" (800 vol, low diff, high intent) ✅
- "tax calculator" (100K vol, high diff, broad intent) ❌
```

---

## Content Templates

### Calculator Page Structure

```markdown
# [Calculator Name] - Free [Use Case] Calculator

## Quick Calculator
[Interactive tool here]

## How to Use This Calculator
[Step-by-step instructions]

## Understanding [Topic]
[Educational content with keywords]

## [Related Concept 1]
[More content]

## [Related Concept 2]
[More content]

## Frequently Asked Questions

### [Question 1]?
[Answer]

### [Question 2]?
[Answer]

## Related Calculators
- [Link 1]
- [Link 2]
- [Link 3]
```

### Comparison Page Structure

```markdown
# [Tool A] vs [Tool B]: [Year] Comparison

## Quick Comparison Table
| Feature | Tool A | Tool B |
|---------|--------|--------|
| Price | | |
| Feature 1 | | |

## Overview
[Brief intro to both tools]

## [Tool A] Review
### Pros
### Cons
### Pricing
### Best For

## [Tool B] Review
### Pros
### Cons
### Pricing
### Best For

## Head-to-Head Comparison
[Detailed comparison by category]

## Verdict: Which Should You Choose?
[Recommendation with affiliate links]

## FAQ
[Questions specific to the comparison]
```

---

## Programmatic SEO

### When to Use

- 100+ similar pages possible
- Clear template structure
- Data source available (API, database, spreadsheet)

### Examples

| Pattern | Pages Generated |
|---------|-----------------|
| `/best-[tool]-for-[use-case]` | 200+ pages |
| `/[city]-[service]` | 1000+ pages |
| `/[product]-vs-[product]` | 500+ pages |
| `/[tool]-pricing-[year]` | 100+ pages |
| `/[tool]-alternatives` | 200+ pages |

### Implementation

1. Define template structure
2. Create data source (database, JSON, CMS)
3. Generate pages at build time (SSG) or runtime (SSR)
4. Unique content per page (not just swapped keywords)
5. Internal linking between related pages

### Quality Requirements

- Each page must provide unique value
- Avoid thin content (<300 words)
- Unique meta titles/descriptions
- Include relevant data/stats
- Link to related pages

---

## Link Building Strategies

### Passive Link Building

1. **Create linkable assets**: Tools, calculators, original research
2. **Embeddable widgets**: "Embed this calculator" with backlink
3. **Resource pages**: Comprehensive guides people reference
4. **Statistics posts**: "50 Freelancer Statistics 2025"

### Active Link Building (Optional)

1. **Guest posting**: Write for niche blogs
2. **HARO**: Help A Reporter Out
3. **Broken link building**: Find broken links, offer replacement
4. **Podcast appearances**: Easy backlinks + exposure

### Avoid

- Buying links
- Link farms
- Excessive link exchanges
- Irrelevant directories

---

## Local SEO (If Applicable)

Not needed for most passive income projects, but if targeting local:

- [ ] Google Business Profile
- [ ] NAP consistency (Name, Address, Phone)
- [ ] Local schema markup
- [ ] Location-specific pages

---

## SEO Monitoring

### Weekly Checks

- [ ] Google Search Console - Errors, crawl issues
- [ ] Rankings for target keywords
- [ ] Organic traffic trends

### Monthly Checks

- [ ] Core Web Vitals report
- [ ] Backlink profile (Ahrefs/Moz)
- [ ] Competitor rankings

### Quarterly Reviews

- [ ] Content audit - Update old content
- [ ] Keyword opportunities - New targets
- [ ] Technical audit - Full site crawl

---

## Common SEO Mistakes

### Technical

- ❌ Blocking search engines in robots.txt
- ❌ No XML sitemap
- ❌ Slow page loads (>3s)
- ❌ Not mobile friendly
- ❌ Duplicate content without canonicals
- ❌ Broken internal links

### Content

- ❌ Thin content (<300 words)
- ❌ Keyword stuffing
- ❌ Duplicate meta titles/descriptions
- ❌ No internal linking
- ❌ Ignoring search intent

### Strategy

- ❌ Targeting impossible keywords
- ❌ Ignoring long-tail keywords
- ❌ No content updates
- ❌ Expecting instant results

---

## Timeline Expectations

| Timeframe | What to Expect |
|-----------|----------------|
| Month 1-2 | Indexing, minimal traffic |
| Month 3-4 | Early rankings, some organic traffic |
| Month 5-6 | Rankings improve, traffic grows |
| Month 7-12 | Steady growth, keyword expansion |
| Year 2+ | Authority builds, compound growth |

**Key Insight**: SEO is slow. Focus on quality, be patient, compound wins.

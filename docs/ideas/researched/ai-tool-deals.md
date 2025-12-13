# AI Tool Deals Aggregator - Research Summary

> Research completed: 2025-12-13
> Decision: QUEUED as secondary project (after Calcverse)
> Full session doc: /docs/session-start/AI-DEALS.md

---

## Concept

"Slickdeals for AI Tools" - A directory tracking 500+ AI tools with real-time deal aggregation, pricing comparisons, and affiliate monetization.

---

## Why This Concept

### Market Opportunity
- AI tool landscape is exploding and overwhelming users
- No dominant "deals aggregator" for AI tools exists
- LTD (Lifetime Deal) hunters are a passionate, vocal community
- Affiliate programs are extremely generous (20-50% recurring)

### Revenue Model
- Primary (60%): Affiliate commissions
- Secondary (25%): Featured listings from tool makers
- Tertiary (15%): Newsletter sponsorships

### Passivity Score: 9/10
- Mostly automated via scrapers
- Community submissions reduce curation burden
- ~2-3 hours/week maintenance once established

---

## Research Findings

### Competitive Landscape

| Site | Approach | Gap |
|------|----------|-----|
| ProductHunt | Launch-focused | No ongoing deals |
| G2/Capterra | Enterprise/reviews | Not prosumer-focused |
| FutureTools | Good directory | No deal aggregation |
| AppSumo | Curated deals | Only their platform |

**Gap**: Nobody aggregates ALL AI tool deals from everywhere.

### Affiliate Economics

| Tool Type | Typical Commission |
|-----------|-------------------|
| AI Writing | 20-45% recurring |
| Image Gen | 15-30% |
| Video/Audio | 20-40% |
| Dev Tools | 20-30% |
| LTD Platforms | 10-20% per sale |

### Traffic Potential
- Comparison pages rank well: "Jasper vs Copy.ai" (18K searches)
- Deal seekers are highly engaged
- Newsletter can drive repeat traffic

---

## Technical Approach

### Stack Selected
- Next.js 14 (App Router) - SSR for SEO + API routes
- Supabase - PostgreSQL + Auth + Realtime
- Tailwind CSS - Rapid development
- Vercel - Easy deployment
- Meilisearch - Fast search
- Puppeteer - Scraping deal sources

### Scraper Architecture
```
Daily cron → Scrape sources → Normalize data → Insert/update
  ↓
AppSumo, StackSocial, PitchGround, Twitter, Reddit
  ↓
Alert matching users → Auto-post social → Weekly digest
```

---

## Implementation Plan Summary

1. **Phase 1 (Week 1-2)**: Foundation + tool directory
2. **Phase 2 (Week 3-4)**: Deals engine + scrapers
3. **Phase 3 (Week 5-6)**: Comparison pages + SEO
4. **Phase 4 (Week 7-8)**: Community + alerts
5. **Phase 5 (Week 9+)**: Monetization optimization

---

## Deal Sources to Scrape

1. AppSumo - Largest LTD platform
2. StackSocial - Tech deals
3. PitchGround - AppSumo competitor
4. DealMirror - Smaller deals
5. Direct tool announcements (Twitter/X)
6. Reddit (r/AppSumo, r/SideProject)

---

## Risk Assessment

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Affiliate terms change | Medium | Diversify across 50+ programs |
| Competition enters | Medium | First-mover + community moat |
| AI hype cools | Low | AI tools aren't going away |
| Scrapers break | High | Alert system, manual fallback |

---

## Decision

**QUEUED** as secondary project because:
- Slightly more complex than Calcverse
- More ongoing maintenance (scrapers)
- Higher revenue ceiling but also higher effort
- Better to nail simple project first

Start after Calcverse MVP ships.

Project name: **AI-Deals** (or rebrand later)

# Summit58 - Session Start Document

> **Read this first.** This document contains everything needed to start a productive session on Summit58.

---

## 1. Quick Context

| Field | Value |
|-------|-------|
| **Project** | Summit58 |
| **Tagline** | "The modern guide to Colorado's 14ers" |
| **What** | Beautiful, mobile-first guide to all 58 Colorado fourteeners |
| **Stack** | SvelteKit + Supabase + Railway |
| **Revenue** | Affiliate + Printables + Membership (minimal ads) |
| **Target** | $2-5K/month |
| **Status** | Planning Complete |
| **Repo** | Not yet created |
| **Domain** | summit58.co (ideal - Colorado reference) |

---

## 2. Full Vision

### What is Summit58?

Summit58 is a modern, mobile-first guide to Colorado's 58 fourteeners (peaks over 14,000 feet). It replaces the outdated 14ers.com with a beautiful, fast, offline-capable experience designed for climbers on the mountain.

**Core features:**
- Clean peak/route pages with essential info at a glance
- User-submitted conditions reports
- Personal peak tracking (climbed, saved, want to do)
- Printable route cards with GPS waypoints
- PWA with offline support
- Gear checklists by route class/season

### Why This Will Work

1. **Incumbent is terrible** - 14ers.com has great data but awful UX, especially mobile
2. **Passionate audience** - 14er baggers are obsessive completionists who research deeply
3. **You're the target user** - You climb these peaks and know the pain points
4. **Mobile-first gap** - No one has nailed the on-mountain experience
5. **Clear monetization** - Gear affiliate, printables, membership without ad overload
6. **Defensible** - User conditions reports create a moat

### Target Users

| Persona | Needs | Behavior |
|---------|-------|----------|
| **First-timer** | Which peak? How hard? What gear? | Researches extensively before first 14er |
| **Peak bagger** | Track progress, find next peak, conditions | Returns repeatedly, wants to complete all 58 |
| **Weekend warrior** | Quick conditions check, route beta | Mobile-heavy, checks morning of climb |
| **Visiting climber** | Which peaks in a week trip? Logistics | Trip planning mode |

### Differentiators vs 14ers.com

| 14ers.com | Summit58 |
|-----------|----------|
| Desktop-first, mobile broken | Mobile-first, works offline |
| Cluttered, ad-heavy | Clean, minimal ads |
| Info buried in text walls | Key stats at a glance |
| Forums mixed with routes | Focused conditions reports only |
| Dated 2005 design | Modern, photography-forward |
| No offline capability | PWA with downloaded routes |

---

## 3. Feature Set

### MVP (Phase 1)

| Feature | Description |
|---------|-------------|
| **Peak pages** | All 58 peaks with stats, photos, routes |
| **Route pages** | Standard route for each peak with description |
| **Quick stats bar** | Distance, gain, class, time - visible immediately |
| **Mobile-first design** | Touch-friendly, fast, responsive |
| **Basic SEO** | Peak/route pages rank for searches |

### Phase 2

| Feature | Description |
|---------|-------------|
| **User accounts** | Supabase auth (email, Google) |
| **Peak tracking** | Mark peaks as climbed, saved, want to do |
| **Conditions reports** | User-submitted recent conditions |
| **Printable route cards** | PDF download with key info |

### Phase 3

| Feature | Description |
|---------|-------------|
| **PWA/Offline** | Download routes for offline access |
| **GPS waypoints** | GPX file downloads |
| **Gear checklists** | By class, by season |
| **Supporter membership** | Ad-free, premium printables |

### Phase 4 (Scale)

| Feature | Description |
|---------|-------------|
| **Photo galleries** | User-submitted peak photos |
| **Trip reports** | Optional longer-form trip logs |
| **Weather integration** | Mountain-specific forecasts |
| **Notifications** | Conditions alerts for saved peaks |

---

## 4. Technical Architecture

### Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| **Framework** | SvelteKit | Fast, light bundles, great PWA support, simpler than React |
| **Database** | Supabase (Postgres) | Auth, DB, storage in one, familiar CLI |
| **Auth** | Supabase Auth | Email + Google, built-in |
| **Hosting** | Railway | Easy deploys, scales, familiar |
| **Storage** | Supabase Storage | User photos, GPX files |
| **Maps** | Mapbox or MapTiler | Custom styling, potential offline tiles |
| **PWA** | SvelteKit + Workbox | Offline support |
| **Analytics** | Plausible | Privacy-focused |

### Project Structure

```
summit58/
├── src/
│   ├── lib/
│   │   ├── components/
│   │   │   ├── PeakCard.svelte
│   │   │   ├── StatsBar.svelte
│   │   │   ├── ConditionReport.svelte
│   │   │   ├── RouteMap.svelte
│   │   │   └── GearChecklist.svelte
│   │   ├── server/
│   │   │   ├── supabase.ts
│   │   │   └── peaks.ts
│   │   └── utils/
│   │       ├── gpx.ts
│   │       └── pdf.ts
│   ├── routes/
│   │   ├── +page.svelte              # Homepage
│   │   ├── +layout.svelte            # App shell
│   │   ├── peaks/
│   │   │   ├── +page.svelte          # All peaks list
│   │   │   └── [slug]/
│   │   │       ├── +page.svelte      # Peak detail
│   │   │       └── [route]/
│   │   │           └── +page.svelte  # Route detail
│   │   ├── conditions/
│   │   │   └── +page.svelte          # Recent conditions feed
│   │   ├── account/
│   │   │   ├── +page.svelte          # User dashboard
│   │   │   ├── login/+page.svelte
│   │   │   └── my-peaks/+page.svelte
│   │   └── api/
│   │       ├── conditions/+server.ts
│   │       └── gpx/[route]/+server.ts
│   ├── app.html
│   └── app.css
├── static/
│   ├── images/peaks/
│   └── gpx/
├── supabase/
│   └── migrations/
├── svelte.config.js
├── tailwind.config.js
└── package.json
```

### Database Schema

```sql
-- Peaks (core data, seeded)
CREATE TABLE peaks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  slug TEXT UNIQUE NOT NULL,
  elevation INTEGER NOT NULL,
  rank INTEGER, -- 1-58 by elevation
  range TEXT, -- "Sawatch", "Sangre de Cristo", etc.
  latitude DECIMAL(9,6) NOT NULL,
  longitude DECIMAL(9,6) NOT NULL,
  hero_image_url TEXT,
  description TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Routes (multiple per peak possible)
CREATE TABLE routes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  peak_id UUID REFERENCES peaks(id),
  name TEXT NOT NULL, -- "East Slopes", "Kelso Ridge"
  slug TEXT NOT NULL,
  is_standard BOOLEAN DEFAULT false,
  distance_miles DECIMAL(4,1), -- round trip
  elevation_gain_ft INTEGER,
  difficulty_class INTEGER, -- 1, 2, 3, 4
  exposure TEXT, -- "Low", "Moderate", "High"
  typical_time_hours TEXT, -- "4-6"
  trailhead_name TEXT,
  trailhead_latitude DECIMAL(9,6),
  trailhead_longitude DECIMAL(9,6),
  trailhead_elevation INTEGER,
  gpx_file_url TEXT,
  description TEXT,
  gear_notes TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  UNIQUE(peak_id, slug)
);

-- Users (Supabase auth handles core, this extends)
CREATE TABLE profiles (
  id UUID PRIMARY KEY REFERENCES auth.users(id),
  display_name TEXT,
  is_supporter BOOLEAN DEFAULT false,
  supporter_since TIMESTAMPTZ,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- User peak tracking
CREATE TABLE user_peaks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES profiles(id),
  peak_id UUID REFERENCES peaks(id),
  status TEXT CHECK (status IN ('climbed', 'saved', 'want')),
  climbed_date DATE,
  climbed_route_id UUID REFERENCES routes(id),
  notes TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  UNIQUE(user_id, peak_id)
);

-- Conditions reports
CREATE TABLE conditions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  route_id UUID REFERENCES routes(id),
  user_id UUID REFERENCES profiles(id),
  report_date DATE NOT NULL,
  content TEXT NOT NULL,
  snow_line_ft INTEGER,
  trail_status TEXT, -- "Clear", "Muddy", "Snow-covered"
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Condition photos
CREATE TABLE condition_photos (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  condition_id UUID REFERENCES conditions(id),
  url TEXT NOT NULL,
  caption TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Indexes
CREATE INDEX idx_routes_peak ON routes(peak_id);
CREATE INDEX idx_conditions_route ON conditions(route_id);
CREATE INDEX idx_conditions_date ON conditions(report_date DESC);
CREATE INDEX idx_user_peaks_user ON user_peaks(user_id);
```

### URL Structure

```
summit58.co/
├── /                           # Homepage - featured peaks, recent conditions
├── /peaks                      # All 58 peaks (sortable, filterable)
├── /peaks/quandary-peak        # Peak detail page
├── /peaks/quandary-peak/east-slopes  # Route detail page
├── /conditions                 # Recent conditions feed
├── /gear                       # Gear checklists (by class)
├── /account                    # User dashboard
├── /account/my-peaks           # Personal peak tracker
├── /about                      # About, methodology
└── /support                    # Become a supporter
```

---

## 5. UI/UX Specifications

### Design Principles

1. **Mobile-first** - Design for phone, enhance for desktop
2. **Stats at a glance** - Key info visible without scrolling
3. **Photography-forward** - Beautiful peak images set the tone
4. **Fast** - No spinners, instant navigation feel
5. **Offline-ready** - Core info accessible without signal
6. **Touch-friendly** - Large tap targets, swipe gestures

### Key UI Components

#### Stats Bar (visible on every peak/route page)
```
┌─────────┬─────────┬─────────┬─────────┐
│  6.75   │  2,975  │  Class  │   4-6   │
│  miles  │   ft    │    1    │  hours  │
│   RT    │  gain   │         │         │
└─────────┴─────────┴─────────┴─────────┘
```

#### Peak Card (for lists)
```
┌────────────────────────────────────────┐
│ ┌──────────────┐  Quandary Peak        │
│ │              │  14,265' · #13        │
│ │    Photo     │  Class 1 · 6.75mi     │
│ │              │  ✓ Climbed 6/15/24    │
│ └──────────────┘                       │
└────────────────────────────────────────┘
```

#### Conditions Report Card
```
┌────────────────────────────────────────┐
│ Quandary Peak · East Slopes            │
│ Dec 14, 2024 · @mountainuser           │
├────────────────────────────────────────┤
│ Snow line around 12,800'. Postholing   │
│ above treeline. Microspikes helpful.   │
│ Trail mostly packed below.             │
│                                        │
│ ❄️ Snow: 12,800' · Trail: Snow-packed  │
└────────────────────────────────────────┘
```

### Color Palette

```
Primary:    #1a365d (deep mountain blue)
Secondary:  #2d3748 (slate)
Accent:     #ed8936 (sunrise orange)
Success:    #38a169 (climbed green)
Background: #f7fafc (light) / #1a202c (dark)
```

### Typography

- **Headings**: Inter or system-ui (clean, modern)
- **Body**: Same, optimized for readability
- **Stats**: Tabular numerals for alignment

### Responsive Breakpoints

- **Mobile**: < 640px (primary target)
- **Tablet**: 640-1024px
- **Desktop**: > 1024px

---

## 6. Monetization Strategy

### Revenue Streams (by priority)

#### 1. Affiliate Links (Primary)
| Partner | Commission | Integration |
|---------|------------|-------------|
| REI | 5% | Gear checklists, contextual links |
| Backcountry.com | 5-7% | Gear recommendations |
| Amazon | 1-4% | Fallback, books, misc gear |

**Approach:** Contextual, helpful recommendations. "Class 3 routes need a helmet - [here's what we recommend]". Not banner ads.

#### 2. Printable Route Cards ($2-3 each or included in membership)
- One-page PDF with route map, stats, waypoints, gear checklist
- Beautiful design worth printing
- Free basic version, premium version with topo

#### 3. Supporter Membership ($20/year)
| Benefit | Value |
|---------|-------|
| Ad-free experience | Clean browsing |
| Premium printables | All route cards included |
| Early conditions | See reports before public |
| Offline downloads | Priority PWA features |
| Supporter badge | Recognition in community |

#### 4. Minimal Display Ads
- Only after significant traffic (50K+ sessions)
- Tasteful placement, never intrusive
- Consider Mediavine/AdThrive over AdSense for outdoor niche rates

#### 5. Lead Generation (Future)
- Guide service referrals
- Gear shop partnerships
- Shuttle service commissions

### Revenue Projections

| Phase | Traffic | Revenue Mix | Monthly |
|-------|---------|-------------|---------|
| MVP | 5K sessions | Affiliate only | $50-100 |
| Growth | 25K sessions | Affiliate + printables | $300-500 |
| Scale | 100K sessions | Full mix | $2-5K |

---

## 7. Sister Site Ecosystem

Summit58 anchors a potential network of related outdoor sites:

```
Summit58 (anchor)
    │
    ├── GearedUp (exists in portfolio)
    │   └── Expand mountaineering category
    │   └── "Best ice axe for 14ers" links back
    │
    ├── AlpineGear (future)
    │   └── Deep mountaineering gear reviews
    │   └── Summit58 links out for gear recs
    │
    ├── PeakList (future expansion)
    │   └── State highpoints
    │   └── Colorado 13ers
    │   └── Other peak lists
    │
    └── TrailSnacks (future)
        └── Hiking/climbing nutrition
        └── "What to eat on a 14er" content
```

**Near-term synergy:** GearedUp can add a mountaineering/hiking category. Summit58 gear pages link to GearedUp reviews. Cross-pollination.

---

## 8. Content: The 58 Peaks

### By Range

| Range | Count | Notable Peaks |
|-------|-------|---------------|
| Sawatch | 15 | Mt. Elbert (#1), Mt. Massive (#2) |
| Sangre de Cristo | 10 | Blanca Peak, Crestone Needle |
| Elk Mountains | 6 | Maroon Bells, Capitol Peak |
| San Juan | 13 | Uncompahgre, Sneffels |
| Mosquito | 5 | Mt. Lincoln, Mt. Democrat |
| Front Range | 6 | Longs Peak, Mt. Evans |
| Tenmile | 2 | Quandary Peak |
| La Garita | 1 | San Luis Peak |

### By Difficulty Class

| Class | Count | Description |
|-------|-------|-------------|
| Class 1 | 18 | Hiking, no hands needed |
| Class 2 | 25 | Scrambling, hands for balance |
| Class 3 | 12 | Climbing, exposure, hands required |
| Class 4 | 3 | Technical, rope recommended |

### Pilot Peaks (Phase 1 MVP)

Start with 10 peaks across difficulty spectrum:

1. **Quandary Peak** - Class 1, most popular, close to Denver
2. **Mt. Elbert** - Class 1, highest in Colorado
3. **Mt. Bierstadt** - Class 1, beginner favorite
4. **Grays Peak** - Class 1, easy access
5. **Torreys Peak** - Class 2, pairs with Grays
6. **Mt. Democrat** - Class 2, DeCaLiBron circuit
7. **Longs Peak** - Class 3, iconic, challenging
8. **Capitol Peak** - Class 4, most difficult
9. **Mt. Sneffels** - Class 3, beautiful San Juans
10. **Handies Peak** - Class 1, remote but accessible

---

## 9. Implementation Plan

### Phase 1: Foundation (MVP)
- [ ] Initialize SvelteKit project with Tailwind
- [ ] Set up Supabase project and CLI
- [ ] Create database schema and seed 10 pilot peaks
- [ ] Build core components (StatsBar, PeakCard, etc.)
- [ ] Create peak list page with filtering
- [ ] Create peak detail page
- [ ] Create route detail page
- [ ] Mobile-first responsive design
- [ ] Deploy to Railway
- [ ] Basic SEO (meta tags, sitemap)

**Exit Criteria:** 10 peaks live, mobile-friendly, deployed

### Phase 2: User Features
- [ ] Implement Supabase auth (email + Google)
- [ ] Create user profiles
- [ ] Build peak tracking (climbed/saved/want)
- [ ] Add conditions report submission
- [ ] Display conditions on route pages
- [ ] User dashboard with peak progress

**Exit Criteria:** Users can sign up, track peaks, submit conditions

### Phase 3: Full Content + PWA
- [ ] Add remaining 48 peaks
- [ ] Multiple routes per peak where applicable
- [ ] Implement PWA with offline support
- [ ] Add GPX download functionality
- [ ] Create printable route card PDFs
- [ ] Gear checklists by class/season
- [ ] Apply for affiliate programs

**Exit Criteria:** All 58 peaks, offline works, printables available

### Phase 4: Scale & Monetize
- [ ] Supporter membership system
- [ ] Premium printables
- [ ] Photo galleries
- [ ] Weather integration
- [ ] Performance optimization
- [ ] Evaluate display ads if traffic warrants

**Exit Criteria:** Revenue generating, 50K+ sessions

---

## 10. Data Sourcing

### Peak/Route Data
- Public domain information (elevations, coordinates)
- Personal experience and notes
- USGS data for coordinates and elevations
- Trailhead locations from Forest Service

### Photography
- Personal photos (you climb these)
- Unsplash/Pexels for initial stock
- User submissions (with permission)
- Consider reaching out to outdoor photographers

### GPX Files
- Create from personal GPS tracks
- USGS topo data
- User contributions

**Important:** Do not scrape 14ers.com. Create original content.

---

## 11. SEO Strategy

### Target Keywords

| Keyword Pattern | Example | Volume |
|-----------------|---------|--------|
| "[peak name]" | "quandary peak" | High |
| "[peak] trail" | "quandary peak trail" | Medium |
| "[peak] conditions" | "longs peak conditions" | Medium |
| "[peak] route" | "capitol peak route" | Medium |
| "14ers colorado" | - | High |
| "easiest 14ers" | - | Medium |
| "14er checklist" | - | Medium |

### Content Strategy
- Every peak gets a dedicated page (58 pages minimum)
- Every route gets a page (100+ pages)
- Conditions reports add fresh content
- Gear checklists target long-tail queries

### Technical SEO
- Clean URLs (/peaks/quandary-peak)
- Schema markup (Place, HikingTrail)
- Fast load times (SvelteKit advantage)
- Mobile-first indexing ready
- XML sitemap
- Internal linking between related peaks

---

## 12. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| 14ers.com has SEO dominance | High | Medium | Better UX drives shares, backlinks; target underserved queries |
| Low initial traffic | High | Medium | Expected; focus on quality, let SEO compound |
| Liability for route info | Medium | High | Clear disclaimers, no "beta guarantees", link to official sources |
| Seasonal traffic dips | High | Low | Expected; winter content, gear guides |
| Supabase/Railway issues | Low | Medium | Standard infrastructure, can migrate if needed |
| User-generated spam | Medium | Low | Require auth, moderation tools |

---

## 13. AI Agent Instructions

### Do
- Prioritize mobile experience in all UI work
- Keep components small and focused
- Use SvelteKit conventions (load functions, form actions)
- Leverage Supabase RLS for security
- Test offline functionality
- Optimize images aggressively
- Write semantic HTML for accessibility

### Don't
- Over-engineer early - MVP first
- Add features not in current phase
- Forget dark mode support
- Neglect loading/error states
- Skip mobile testing
- Copy any content from 14ers.com

### SvelteKit Patterns
```svelte
<!-- Use load functions for data -->
// +page.server.ts
export async function load({ params }) {
  const peak = await getPeak(params.slug);
  return { peak };
}

<!-- Keep components reactive -->
<script>
  export let data;
  $: peak = data.peak;
</script>

<!-- Use form actions for mutations -->
// +page.server.ts
export const actions = {
  submitCondition: async ({ request, locals }) => {
    // handle form
  }
};
```

### Supabase Patterns
```typescript
// Use typed client
import { createClient } from '@supabase/supabase-js';
import type { Database } from '$lib/database.types';

const supabase = createClient<Database>(url, key);

// RLS policies handle auth
const { data } = await supabase
  .from('peaks')
  .select('*, routes(*)');
```

### Decisions Already Made
- SvelteKit over Next.js (performance, PWA support, learning opportunity)
- Supabase over custom backend (familiar, all-in-one)
- Railway over Vercel (familiar, more control)
- Minimal ads, affiliate-first (differentiation)
- Mobile-first always (target use case)
- Conditions reports over full forums (avoid moderation burden)

---

## 14. Passivity Analysis

| Factor | Score | Notes |
|--------|-------|-------|
| **Content Freshness** | 7/10 | Peaks don't change, but conditions do (user-generated) |
| **Maintenance** | 6/10 | More than calculator sites - moderation, updates |
| **Support Burden** | 7/10 | User accounts = some support needs |
| **Scaling** | 8/10 | Content scales linearly, traffic can compound |
| **Technical** | 6/10 | Backend requires monitoring |

**Overall Passivity Score: 7/10**

This is intentionally less passive than the calculator sites. It's more defensible, more sticky, and more personally rewarding. The user-generated conditions create a moat but require light moderation.

---

## 15. Session Log

### 2025-12-15 - Project Created
- Identified opportunity: 14ers.com is terrible, especially mobile
- Decided on narrow focus: Colorado 14ers only (58 peaks)
- Named project Summit58 (summit58.co = Colorado reference)
- Designed monetization without ad overload (affiliate + printables + membership)
- Mapped sister site ecosystem (GearedUp synergy)
- Chose SvelteKit over Next.js for performance/PWA benefits
- Confirmed Railway + Supabase as infrastructure
- Created comprehensive session-start document
- Defined 4-phase implementation plan

---

## 16. Quick Reference

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
- SvelteKit Docs: https://kit.svelte.dev/docs
- Supabase Docs: https://supabase.com/docs
- Railway Docs: https://docs.railway.app
- Tailwind Docs: https://tailwindcss.com/docs

### Environment Variables
```
PUBLIC_SUPABASE_URL=
PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
```

---

**Next Action:** Create summit58 repo and begin Phase 1 (Foundation)

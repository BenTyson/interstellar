# Evermore - Session Start Document

> **Read this first.** This document contains everything needed to start a productive session on Evermore.

---

## 1. Quick Context

| Field | Value |
|-------|-------|
| **Project** | Evermore |
| **Tagline** | "Their memory lives evermore" |
| **What** | Beautiful, permanent memorial sites for families |
| **Stack** | SvelteKit + Supabase + Railway |
| **Revenue** | B2C: $99-199 one-time | B2B: $99-249/mo SaaS for funeral homes |
| **Target** | $5-10K/month |
| **Status** | Planning Complete |
| **Repo** | Not yet created |
| **Domain** | evermore.io, evermore.co (TBD) |

---

## 2. Full Vision

### What is Evermore?

Evermore is a platform for creating beautiful, permanent memorial sites. When someone dies, a family member can create a dignified online memorial in 10 minutes - a single place to share the obituary, photos, service details, and collect tributes from loved ones.

**The problem we solve:**
- Newspaper obituaries cost $500-2000+ and disappear
- Funeral home sites are ugly templates that expire in a year
- Legacy.com feels exploitative and ad-heavy
- Facebook isn't dignified for death
- DIY sites (Squarespace) require too much work during grief

**Our solution:**
- Beautiful by default (no design skills needed)
- Permanent (site lives forever)
- Shareable (one link for everything)
- Dignified (no ads, no upsells during grief)
- Useful (service details, donations, livestream, guest book)

### Why This Will Work

1. **Universal need** - 2.8 million deaths/year in US, every family needs this
2. **Current options are bad** - Legacy.com is hated, funeral home sites are garbage
3. **Emotional willingness to pay** - Families will pay for quality during grief
4. **One-time revenue** - No churn, each sale is permanent
5. **Word of mouth** - Every memorial is shared with 50-200 people
6. **B2B expansion** - Funeral homes are natural distribution partners
7. **Meaningful work** - Helping families during hardest time

### Target Users

**B2C: Families**
| Persona | Trigger | Needs |
|---------|---------|-------|
| **Adult Child** | Parent dies | Quick setup, share with extended family |
| **Spouse** | Partner dies | Dignified tribute, collect memories |
| **Sibling** | Brother/sister dies | Coordinate with family, preserve legacy |
| **Friend** | Close friend dies | Help family, organize tributes |

**B2B: Funeral Homes**
| Persona | Pain Point | Needs |
|---------|------------|-------|
| **Owner** | Differentiate from competitors | Modern offering, recurring revenue |
| **Director** | Families ask for better online presence | Easy tool to offer families |
| **Marketing** | Need digital presence | Branded memorials spread their name |

### Key Differentiators

| Evermore | Legacy.com | Funeral Home Sites |
|----------|-----------|-------------------|
| Beautiful, modern design | Dated, cluttered | Template garbage |
| Permanent (forever) | Ads, upsells | Expires in 1 year |
| One-time fair price | Nickel-and-dime | Included but limited |
| Single shareable link | Hard to navigate | Buried in their site |
| Guest book + tributes | Basic comments | None or limited |
| Donation integration | Flower upsells | Separate process |

---

## 3. Product Features

### Memorial Site Structure

```
evermore.io/john-smith
├── Hero Section
│   ├── Photo (or photo carousel)
│   ├── Name, dates (1945-2024)
│   └── Short epitaph
├── Life Story
│   ├── Obituary text (rich text)
│   └── Timeline (optional milestones)
├── Photo Gallery
│   ├── Uploaded by family
│   └── Contributed by visitors
├── Tributes
│   ├── Written memories from loved ones
│   ├── Moderated by family
│   └── Photo attachments optional
├── Service Details
│   ├── Date, time, location
│   ├── Map integration
│   ├── Livestream link (if applicable)
│   └── Dress code / special instructions
├── Give
│   ├── Charity donations (in lieu of flowers)
│   ├── Flower delivery (affiliate)
│   ├── Meal train link
│   └── Family fund (GoFundMe-style, optional)
├── Guest Book
│   ├── Who visited
│   ├── Contact info for thank-you notes
│   └── Private to family
└── Footer
    ├── Share buttons
    ├── Print obituary
    └── "Powered by Evermore" (free tier)
```

### Creation Flow

```
Step 1: Basic Info
  → Name, dates, relationship to deceased
  → Upload main photo

Step 2: Life Story
  → Paste/write obituary
  → AI assist: "Help me write this" (optional)

Step 3: Photos
  → Upload gallery
  → Drag to reorder

Step 4: Service Details
  → Date, time, location
  → Add livestream link

Step 5: Giving
  → Link charity for donations
  → Enable/disable flower option

Step 6: Publish
  → Choose URL (evermore.io/john-smith)
  → Share link
```

**Time to complete: 10-15 minutes**

### Family Dashboard

After creation, families can:
- Edit memorial content
- Moderate tributes (approve/reject)
- View guest book (who visited, contact info)
- Download tribute book (PDF)
- Invite other family admins
- Upgrade to paid tier

---

## 4. Revenue Model

### Phase 1: B2C Direct to Families

| Tier | Price | Features |
|------|-------|----------|
| **Free** | $0 | Basic memorial, 30-day limit, 10 photos, "Powered by Evermore" |
| **Forever** | $99 one-time | Permanent site, custom URL, unlimited photos, no watermark |
| **Legacy** | $199 one-time | + Physical tribute book, QR code for gravestone, priority support |

**Pricing rationale:**
- Newspaper obits cost $500-2000+
- $99 feels fair during grief
- One-time removes subscription guilt
- "Forever" tier name reinforces permanence

### Phase 2: B2B Funeral Home SaaS

| Tier | Price | Features |
|------|-------|----------|
| **Starter** | $99/mo | 10 memorials/month, funeral home branding |
| **Professional** | $249/mo | Unlimited memorials, custom domain, family handoff |
| **Enterprise** | Custom | Multi-location, API, white-label app, integrations |

**Value prop for funeral homes:**
- "Every memorial you create stays online forever with your branding"
- "Families share it with 50-200 people - free marketing for you"
- "Differentiate from competitors stuck in 2005"
- "Add $50-100 to each service package"

### Revenue Projections

**B2C Phase:**
| Metric | Conservative | Optimistic |
|--------|--------------|------------|
| Memorials/month | 100 | 500 |
| Paid conversion | 20% | 30% |
| Avg revenue | $120 | $140 |
| Monthly revenue | $2,400 | $21,000 |

**B2B Addition:**
| Metric | Year 1 | Year 2 |
|--------|--------|--------|
| Funeral home clients | 20 | 100 |
| Avg MRR per client | $150 | $180 |
| Monthly revenue | $3,000 | $18,000 |

---

## 5. Technical Architecture

### Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| **Framework** | SvelteKit | SSR for SEO, fast, familiar |
| **Database** | Supabase (Postgres) | Auth, DB, storage, RLS |
| **Hosting** | Railway | Familiar, scalable |
| **Image Storage** | Supabase Storage or Cloudinary | Need reliable long-term storage |
| **Payments** | Stripe | One-time + subscriptions |
| **Email** | Resend or Postmark | Transactional (share notifications) |
| **Analytics** | Plausible | Privacy-focused |
| **PDF Generation** | Puppeteer or react-pdf | Tribute book export |

### Project Structure

```
evermore/
├── src/
│   ├── lib/
│   │   ├── components/
│   │   │   ├── Memorial/
│   │   │   │   ├── Hero.svelte
│   │   │   │   ├── LifeStory.svelte
│   │   │   │   ├── PhotoGallery.svelte
│   │   │   │   ├── Tributes.svelte
│   │   │   │   ├── ServiceDetails.svelte
│   │   │   │   ├── GiveSection.svelte
│   │   │   │   └── GuestBook.svelte
│   │   │   ├── Creator/
│   │   │   │   ├── StepBasicInfo.svelte
│   │   │   │   ├── StepLifeStory.svelte
│   │   │   │   ├── StepPhotos.svelte
│   │   │   │   ├── StepService.svelte
│   │   │   │   └── StepPublish.svelte
│   │   │   ├── Dashboard/
│   │   │   │   ├── MemorialList.svelte
│   │   │   │   ├── TributeModeration.svelte
│   │   │   │   └── GuestBookView.svelte
│   │   │   └── common/
│   │   │       ├── Button.svelte
│   │   │       ├── Card.svelte
│   │   │       └── ImageUpload.svelte
│   │   ├── server/
│   │   │   ├── supabase.ts
│   │   │   ├── stripe.ts
│   │   │   └── email.ts
│   │   └── utils/
│   │       ├── slugify.ts
│   │       └── dates.ts
│   ├── routes/
│   │   ├── +page.svelte                    # Homepage
│   │   ├── +layout.svelte                  # App shell
│   │   ├── [slug]/
│   │   │   └── +page.svelte                # Memorial page (public)
│   │   ├── create/
│   │   │   └── +page.svelte                # Memorial creator
│   │   ├── dashboard/
│   │   │   ├── +page.svelte                # My memorials
│   │   │   ├── [id]/+page.svelte           # Edit memorial
│   │   │   └── [id]/tributes/+page.svelte  # Moderate tributes
│   │   ├── pricing/
│   │   │   └── +page.svelte                # Pricing page
│   │   ├── for-funeral-homes/
│   │   │   └── +page.svelte                # B2B landing
│   │   └── api/
│   │       ├── memorials/+server.ts
│   │       ├── tributes/+server.ts
│   │       ├── upload/+server.ts
│   │       └── webhooks/stripe/+server.ts
│   ├── app.html
│   └── app.css
├── supabase/
│   └── migrations/
├── static/
│   └── images/
├── svelte.config.js
├── tailwind.config.js
└── package.json
```

### Database Schema

```sql
-- Memorial sites
CREATE TABLE memorials (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug TEXT UNIQUE NOT NULL,

  -- Basic info
  name TEXT NOT NULL,
  birth_date DATE,
  death_date DATE,
  epitaph TEXT,

  -- Content
  obituary TEXT,
  timeline JSONB, -- [{year, event}]

  -- Service details
  service_date TIMESTAMPTZ,
  service_location TEXT,
  service_address TEXT,
  service_livestream_url TEXT,
  service_notes TEXT,

  -- Giving
  charity_name TEXT,
  charity_url TEXT,
  enable_flowers BOOLEAN DEFAULT false,
  family_fund_url TEXT,

  -- Settings
  allow_photo_uploads BOOLEAN DEFAULT true,
  require_tribute_approval BOOLEAN DEFAULT true,

  -- Ownership
  created_by UUID REFERENCES auth.users(id),
  tier TEXT DEFAULT 'free', -- 'free', 'forever', 'legacy'
  expires_at TIMESTAMPTZ, -- null for paid tiers

  -- Meta
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Memorial photos
CREATE TABLE memorial_photos (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  memorial_id UUID REFERENCES memorials(id) ON DELETE CASCADE,
  url TEXT NOT NULL,
  caption TEXT,
  uploaded_by UUID REFERENCES auth.users(id),
  is_hero BOOLEAN DEFAULT false,
  display_order INTEGER,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Tributes (memories from loved ones)
CREATE TABLE tributes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  memorial_id UUID REFERENCES memorials(id) ON DELETE CASCADE,

  -- Author
  author_name TEXT NOT NULL,
  author_email TEXT,
  author_relationship TEXT, -- "Friend", "Coworker", "Neighbor"

  -- Content
  content TEXT NOT NULL,
  photo_url TEXT,

  -- Moderation
  status TEXT DEFAULT 'pending', -- 'pending', 'approved', 'rejected'

  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Guest book (who visited)
CREATE TABLE guest_book (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  memorial_id UUID REFERENCES memorials(id) ON DELETE CASCADE,

  name TEXT NOT NULL,
  email TEXT,
  message TEXT, -- Optional short message

  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Memorial admins (family members who can edit)
CREATE TABLE memorial_admins (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  memorial_id UUID REFERENCES memorials(id) ON DELETE CASCADE,
  user_id UUID REFERENCES auth.users(id),
  role TEXT DEFAULT 'admin', -- 'owner', 'admin'

  created_at TIMESTAMPTZ DEFAULT NOW(),
  UNIQUE(memorial_id, user_id)
);

-- Funeral home accounts (B2B)
CREATE TABLE funeral_homes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  slug TEXT UNIQUE,
  logo_url TEXT,
  website TEXT,

  -- Subscription
  stripe_customer_id TEXT,
  subscription_tier TEXT DEFAULT 'starter',
  subscription_status TEXT,

  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Link memorials to funeral homes
CREATE TABLE funeral_home_memorials (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  funeral_home_id UUID REFERENCES funeral_homes(id),
  memorial_id UUID REFERENCES memorials(id),

  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Indexes
CREATE INDEX idx_memorials_slug ON memorials(slug);
CREATE INDEX idx_memorials_created_by ON memorials(created_by);
CREATE INDEX idx_tributes_memorial ON tributes(memorial_id);
CREATE INDEX idx_tributes_status ON tributes(status);
CREATE INDEX idx_guest_book_memorial ON guest_book(memorial_id);
CREATE INDEX idx_photos_memorial ON memorial_photos(memorial_id);
```

### URL Structure

```
evermore.io/
├── /                           # Homepage
├── /create                     # Create memorial wizard
├── /pricing                    # Pricing page
├── /for-funeral-homes          # B2B landing page
├── /dashboard                  # My memorials
├── /dashboard/[id]             # Edit specific memorial
├── /dashboard/[id]/tributes    # Moderate tributes
├── /[slug]                     # Public memorial page
└── /api/
    ├── /api/memorials
    ├── /api/tributes
    ├── /api/upload
    └── /api/webhooks/stripe
```

---

## 6. Implementation Plan

### Phase 1: MVP (Core Memorial)

**Goal:** Create and view beautiful memorial pages.

**Deliverables:**
- [ ] Initialize SvelteKit project with Tailwind
- [ ] Set up Supabase project
- [ ] Build memorial creation wizard (5 steps)
- [ ] Build public memorial page (responsive, beautiful)
- [ ] Photo upload and gallery
- [ ] Basic tribute submission
- [ ] Deploy to Railway
- [ ] Landing page with value prop

**Exit Criteria:** User can create memorial, share link, friends can leave tributes.

### Phase 2: Monetization

**Goal:** Accept payments, enforce tiers.

**Deliverables:**
- [ ] Stripe integration (one-time payments)
- [ ] Tier enforcement (free expires after 30 days)
- [ ] Upgrade flow from free to paid
- [ ] Email reminders before expiration
- [ ] Payment success/receipt emails

**Exit Criteria:** Users can pay $99/$199 for permanent memorials.

### Phase 3: Family Dashboard

**Goal:** Full memorial management for families.

**Deliverables:**
- [ ] Dashboard with memorial list
- [ ] Edit memorial content
- [ ] Tribute moderation (approve/reject)
- [ ] Guest book view with contact export
- [ ] Invite family members as co-admins
- [ ] Download tribute book (PDF)

**Exit Criteria:** Families can fully manage their memorial.

### Phase 4: B2B (Funeral Homes)

**Goal:** SaaS offering for funeral homes.

**Deliverables:**
- [ ] Funeral home signup and onboarding
- [ ] Funeral home branding on memorials
- [ ] Bulk memorial creation
- [ ] Stripe subscriptions
- [ ] Funeral home dashboard
- [ ] Handoff flow (funeral home → family)

**Exit Criteria:** Funeral homes can subscribe and create branded memorials.

### Phase 5: Growth & Polish

**Goal:** Optimize acquisition and retention.

**Deliverables:**
- [ ] SEO optimization (obituary searches)
- [ ] Social sharing optimization (OG images)
- [ ] AI obituary writing assistant
- [ ] Physical tribute book fulfillment
- [ ] QR code generator for gravestones
- [ ] Grief resources / next steps guide

**Exit Criteria:** Organic growth, high satisfaction.

---

## 7. Design Principles

### Visual Design

**Mood:** Dignified, warm, peaceful, timeless

**Color Palette:**
```
Primary:    #1a1a2e (deep navy - dignified)
Secondary:  #4a4a6a (muted purple-gray)
Accent:     #d4af37 (muted gold - warmth)
Background: #faf9f7 (warm white)
Text:       #2d2d2d (soft black)
```

**Typography:**
- Headings: Serif (Playfair Display, Cormorant) - traditional, dignified
- Body: Sans-serif (Inter, Source Sans) - readable, modern
- Names/Dates: Serif, slightly larger

**Imagery:**
- Soft, high-quality photography
- Ample white space
- Subtle borders, no harsh lines
- Gentle shadows

### UX Principles

1. **Simplicity during grief** - Minimize decisions, smart defaults
2. **Progress visible** - "Step 2 of 5" - user knows they're almost done
3. **Save progress** - Auto-save, can return later
4. **Preview before publish** - See exactly what others will see
5. **Share-first** - Make sharing dead simple (copy link, share buttons)
6. **Mobile-first** - Many will view on phone

### Tone of Voice

- Warm but not saccharine
- Helpful but not pushy
- Respectful, never sales-y
- "Create a memorial" not "Buy a memorial"
- "Their memory lives on" not "Preserve memories forever!"

---

## 8. Competitive Landscape

### Direct Competitors

| Competitor | Pricing | Strengths | Weaknesses |
|------------|---------|-----------|------------|
| **Legacy.com** | Free + upsells | Market leader, newspaper partnerships | Dated, ad-heavy, feels predatory |
| **Everloved** | $99-299 | Modern design | Limited free tier |
| **Echovita** | Free | Wide reach | Aggregator, not creator |
| **ForeverMissed** | $49/year | Affordable | Subscription model, dated |
| **MyKeeper** | $79 one-time | One-time pricing | Limited features |

### Indirect Competitors

| Type | Examples | Why We're Different |
|------|----------|-------------------|
| Funeral home sites | Each funeral home | We're permanent, beautiful, shareable |
| Facebook memorials | Facebook | Dedicated, dignified, no algorithm |
| CaringBridge | CaringBridge | They're for illness journey, we're for after |
| Newspapers | Local papers | We're free/cheap, multimedia, permanent |

### Our Positioning

**"The memorial site that actually respects families."**

- No ads ever
- No upsells during creation
- One fair price for forever
- Beautiful by default
- Share one link for everything

---

## 9. Go-to-Market Strategy

### B2C Acquisition

**SEO (Primary):**
- Target: "[name] obituary", "how to write obituary", "memorial website"
- Content: Obituary writing guides, grief resources
- Each memorial page is SEO-optimized

**Word of Mouth:**
- Every memorial shared with 50-200 people
- "Powered by Evermore" on free tier
- Easy sharing tools

**Partnerships:**
- Hospice organizations
- Grief counselors
- Estate attorneys

### B2B Acquisition

**Outbound:**
- Direct outreach to funeral home owners
- LinkedIn, email
- Trade shows (NFDA annual convention)

**Inbound:**
- "For Funeral Homes" landing page
- Case studies from early adopters
- Demo videos

**Pilot Program:**
- Offer free 3-month trial to 10 funeral homes
- Gather testimonials and case studies
- Refine B2B product based on feedback

---

## 10. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Emotional support burden | High | Medium | Clear self-service, gentle email support, grief resources |
| Photo storage costs | Medium | Medium | Compress images, set limits per tier, monitor costs |
| Legacy.com competes | Low | Medium | They're too big to pivot fast; we're nimble |
| Funeral homes slow to adopt | Medium | Medium | Prove B2C first, then bring data |
| Sensitive data handling | Medium | High | Strong security, GDPR compliance, clear privacy |
| Seasonal demand spikes | Medium | Low | Stateless architecture, auto-scaling |

---

## 11. Passivity Analysis

| Factor | Score | Notes |
|--------|-------|-------|
| **Content Freshness** | 10/10 | User-generated, eternal |
| **Maintenance** | 7/10 | Photo storage, uptime critical |
| **Support Burden** | 5/10 | Emotional users need gentle support |
| **Scaling** | 9/10 | Each sale is one-time, sites are static |
| **Technical** | 7/10 | Photo storage, backups critical |

**Overall Passivity Score: 7/10**

Less passive than calculators due to support burden and data responsibility, but:
- One-time sales = no churn management
- Static sites = low server costs
- User-generated content = no content creation
- Funeral home SaaS = recurring revenue

---

## 12. AI Agent Instructions

### Do
- Prioritize simplicity - users are grieving, minimize cognitive load
- Make defaults beautiful - users shouldn't need to customize
- Auto-save everything - don't lose their work
- Test mobile thoroughly - many will view on phones
- Use warm, respectful copy throughout
- Optimize images aggressively - storage costs matter at scale

### Don't
- Use dark patterns or urgency tactics
- Show ads or upsells during creation flow
- Require account before starting creation
- Use generic stock photos of sad people
- Over-engineer - keep it simple and dignified

### Decisions Already Made
- SvelteKit over Next.js (familiar, fast)
- Supabase for everything (auth, DB, storage)
- One-time pricing primary (not subscription)
- B2C first, B2B second
- No ads ever on memorial pages

### Open Questions
- Physical tribute book fulfillment partner?
- AI obituary writing: OpenAI vs Anthropic?
- Gravestone QR code: partner or DIY?
- International expansion (language, payment)?

### Common Pitfalls to Avoid

1. **Don't be morbid** - Celebrate life, don't dwell on death
2. **Don't be pushy** - Free tier should be genuinely useful
3. **Don't lose data** - Backups are critical, families trust us with memories
4. **Don't over-automate support** - These users need human touch sometimes
5. **Don't forget mobile** - Memorial links shared via text, viewed on phones

---

## 13. Session Log

### 2025-12-18 - Project Created
- Identified memorial sites as meaningful, underserved opportunity
- Decided on hybrid B2C → B2B approach (validate with consumers first)
- Named project Evermore - "Their memory lives evermore"
- Designed 5-phase implementation plan
- Confirmed SvelteKit + Supabase + Railway stack
- Created comprehensive session-start document

---

## 14. Quick Reference

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
- Legacy.com (competitor): https://www.legacy.com
- Everloved (competitor): https://everloved.com
- SvelteKit Docs: https://kit.svelte.dev/docs
- Supabase Docs: https://supabase.com/docs
- Stripe Docs: https://stripe.com/docs

### Environment Variables
```
PUBLIC_SUPABASE_URL=
PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
RESEND_API_KEY=
```

---

**Next Action:** Create evermore repo and begin Phase 1 (MVP)

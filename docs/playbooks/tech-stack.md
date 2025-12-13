# Tech Stack Playbook

> Standard tech decisions for passive income projects. Reference this when starting new projects.

---

## Decision Framework

For passive income projects, optimize for:

1. **Low Maintenance** - Fewer moving parts = fewer things to break
2. **Low/Zero Cost** - Generous free tiers for bootstrapping
3. **SEO Performance** - Fast load times, good Core Web Vitals
4. **Developer Experience** - Build fast, iterate fast
5. **Scalability** - Can handle growth without re-architecture

---

## Recommended Stacks by Project Type

### Static Sites (Calculators, Tools, Directories)

```
Framework:    Astro (SSG)
Styling:      Tailwind CSS
Hosting:      Cloudflare Pages
Analytics:    Plausible
```

**When to use**: Content-heavy, SEO-focused, minimal interactivity

**Pros**:
- Maximum performance
- Zero server costs
- Perfect Core Web Vitals
- Simple deployment

**Cons**:
- No server-side logic
- Static = rebuild for content changes

---

### Dynamic Apps (SaaS, Scrapers, User Auth)

```
Framework:    Next.js 14 (App Router)
Database:     Supabase (PostgreSQL + Auth)
Styling:      Tailwind CSS
Hosting:      Vercel
Email:        Resend
```

**When to use**: Need auth, database, API routes, real-time features

**Pros**:
- Full-stack in one framework
- Supabase free tier is generous
- Great DX with Vercel

**Cons**:
- More complex than static
- Potential for higher costs at scale

---

### Scraper/Automation Projects

```
Runtime:      Node.js or Python
Scraping:     Puppeteer / Playwright
Scheduling:   Vercel Cron / GitHub Actions / Railway
Database:     Supabase or SQLite
```

**When to use**: Data aggregation, price monitoring, deal tracking

**Pros**:
- Can run on free tiers
- Flexible scheduling

**Cons**:
- Can get blocked
- Maintenance when sites change

---

## Component Recommendations

### Hosting

| Provider | Best For | Free Tier | Notes |
|----------|----------|-----------|-------|
| **Cloudflare Pages** | Static sites | Unlimited | Best performance |
| **Vercel** | Next.js apps | 100GB bandwidth | Easy deployment |
| **Netlify** | Static + Functions | 100GB bandwidth | Good alternative |
| **Railway** | Backend services | $5 credit | For workers/crons |

**Recommendation**: Cloudflare Pages for static, Vercel for dynamic

---

### Databases

| Provider | Best For | Free Tier | Notes |
|----------|----------|-----------|-------|
| **Supabase** | Full-stack apps | 500MB, 50K MAU | PostgreSQL + Auth + Realtime |
| **PlanetScale** | MySQL apps | 1B row reads | Good scaling |
| **Turso** | Edge SQLite | 500 DBs, 9GB | Lightweight |
| **None** | Static projects | N/A | Use URL params/localStorage |

**Recommendation**: Supabase for most projects, skip DB if possible

---

### Authentication

| Provider | Best For | Free Tier | Notes |
|----------|----------|-----------|-------|
| **Supabase Auth** | Supabase projects | Included | Magic link, OAuth |
| **Clerk** | Complex auth needs | 10K MAU | Beautiful UI |
| **NextAuth** | DIY approach | Free | More setup required |
| **None** | Anonymous tools | N/A | Don't add auth unless needed |

**Recommendation**: Supabase Auth if using Supabase, otherwise avoid auth

---

### Analytics

| Provider | Best For | Free Tier | Notes |
|----------|----------|-----------|-------|
| **Plausible** | Privacy-focused | $9/mo (or self-host) | No cookie banner needed |
| **Umami** | Self-hosted | Free | Open source |
| **Vercel Analytics** | Vercel apps | Included | Basic metrics |
| **Google Analytics** | Enterprise needs | Free | Privacy concerns |

**Recommendation**: Plausible or Umami for simplicity

---

### Email

| Provider | Best For | Free Tier | Notes |
|----------|----------|-----------|-------|
| **Resend** | Transactional | 3K/mo | Developer-friendly |
| **Loops** | Marketing + Trans | 1K contacts | Good for newsletters |
| **Mailchimp** | Large lists | 500 contacts | Clunky but powerful |
| **ConvertKit** | Creators | 1K subs | Newsletter focused |

**Recommendation**: Resend for transactional, Loops or ConvertKit for newsletters

---

### Payments

| Provider | Best For | Fees | Notes |
|----------|----------|------|-------|
| **Stripe** | Most payments | 2.9% + $0.30 | Industry standard |
| **Lemon Squeezy** | Digital products | 5% | Handles VAT/sales tax |
| **Gumroad** | Quick setup | 10% | Highest fees, easiest setup |

**Recommendation**: Stripe for control, Lemon Squeezy for simplicity

---

### Search

| Provider | Best For | Free Tier | Notes |
|----------|----------|-----------|-------|
| **Meilisearch** | Self-hosted | Free | Fast, typo-tolerant |
| **Algolia** | Hosted search | 10K searches | Easy setup |
| **Pagefind** | Static sites | Free | Build-time indexing |

**Recommendation**: Pagefind for static, Meilisearch for dynamic

---

### Ad Networks

| Network | Requirements | RPM Range | Notes |
|---------|--------------|-----------|-------|
| **Google AdSense** | None | $1-10 | Easy approval |
| **Mediavine** | 50K sessions/mo | $10-30 | Worth the wait |
| **AdThrive** | 100K pageviews/mo | $15-35 | Premium tier |
| **Ezoic** | 10K visits/mo | $5-15 | Aggressive ads |

**Recommendation**: Start AdSense, graduate to Mediavine at 50K sessions

---

## Anti-Patterns to Avoid

### Don't Over-Engineer

```
❌ Kubernetes for a calculator site
❌ Microservices for MVP
❌ Custom auth when Supabase works
❌ Self-hosted everything
```

### Don't Pay Before You Need To

```
❌ Paid hosting before 100K visitors
❌ Premium analytics before product-market fit
❌ Email service before you have subscribers
```

### Don't Add Complexity

```
❌ Database when localStorage works
❌ Auth when anonymous works
❌ Real-time when polling works
❌ Mobile app when responsive web works
```

---

## Quick Start Commands

### Astro Project

```bash
npm create astro@latest my-project
cd my-project
npx astro add tailwind
npm run dev
```

### Next.js + Supabase Project

```bash
npx create-next-app@latest my-project --typescript --tailwind --app
cd my-project
npm install @supabase/supabase-js @supabase/ssr
npm run dev
```

### Cloudflare Pages Deployment

```bash
npm run build
npx wrangler pages deploy dist
```

### Vercel Deployment

```bash
npm i -g vercel
vercel
```

---

## Cost Estimation Template

For budgeting new projects:

| Service | Monthly Cost (0-10K users) | Monthly Cost (10K-100K) |
|---------|----------------------------|-------------------------|
| Hosting | $0 (free tier) | $0-20 |
| Database | $0 (free tier) | $25-50 |
| Email | $0 (free tier) | $20-50 |
| Analytics | $0-9 | $9-19 |
| Domain | ~$1 | ~$1 |
| **Total** | **$0-10** | **$55-140** |

Revenue should exceed costs before scaling beyond free tiers.

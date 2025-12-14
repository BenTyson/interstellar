# HUEGO - Session Start Document

> **Last Updated**: 2025-12-13
> **Current Phase**: Queued (After Crunch)
> **Project Repo**: Not yet created
> **Project Name**: HueGo
> **Tagline**: "Ready, set, HueGo"

---

## 1. Quick Context

**What**: A modular color palette generator with 4 distinct UI modes - Immersive, Context, Mood, and Playground - that adapts to how designers want to work.

**Revenue Model**: Display ads (primary) + Premium subscription ($3-5/mo) for ad-free, unlimited saves, advanced exports

**Why This Will Work**: Competitors are functional but boring. We differentiate on *delightful UX* with a mode-switching architecture that no one else has.

**Target Revenue**: $1-5K/month

**Passivity Score**: 9/10 - Static tool, no accounts required for core use, ads = passive

---

## 2. Full Project Vision

### What We're Building

A color palette generator that transforms based on how you want to work:

1. **Immersive Mode** - Full-screen, meditative color exploration
2. **Context Mode** - See palettes applied to real designs instantly
3. **Mood Mode** - Start with feelings, get colors that match
4. **Playground Mode** - Gamified discovery, swipe-based learning

One tool, four experiences. Switch seamlessly between them.

### Why It Will Succeed

1. **UX is the moat** - Coolors is fast but sterile; we're fast AND beautiful
2. **Mode-switching is novel** - No competitor offers this flexibility
3. **Mobile-first** - Most palette tools are desktop-focused
4. **Emotional connection** - Mood mode creates stickiness
5. **Viral mechanics** - Playground mode encourages sharing

### Target Users

**Primary:**
- UI/UX designers
- Web developers
- Graphic designers
- Brand designers

**Secondary:**
- Content creators (thumbnails, social posts)
- Hobbyist designers
- Students learning design
- Anyone picking colors for anything

### Key Differentiators

| Competitor | Their Approach | HueGo Advantage |
|------------|----------------|-----------------|
| Coolors | Fast spacebar generation | Fast + Beautiful + Multiple modes |
| Adobe Color | Color theory focused | More accessible, not locked to ecosystem |
| PaletteMaker | Context preview | Multiple contexts + 3 other modes |
| Khroma | AI trained preferences | AI + immediate gratification + flexibility |
| Color Hunt | Community browse | Active creation + community + modes |

### Success Metrics

| Metric | 6 Month | 12 Month |
|--------|---------|----------|
| Monthly Visitors | 30K | 100K |
| Palettes Generated | 500K | 2M |
| Premium Subscribers | 200 | 1,000 |
| Monthly Revenue | $500-1K | $2-5K |

---

## 3. Technical Architecture

### Stack Decisions (FINAL)

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Framework | **Next.js 14** | App router, great for interactive + SEO |
| Styling | **Tailwind CSS** | Rapid development, easy theming |
| State | **Zustand** | Simple, fast, persists palette across modes |
| Animation | **Framer Motion** | Smooth mode transitions, micro-interactions |
| Hosting | **Vercel** | Easy deployment, edge functions |
| Analytics | **Plausible** | Privacy-focused |
| Storage | **localStorage** | No backend needed for MVP |

### Why No Database for MVP

- Palettes stored in localStorage
- Share via URL params (encoded palette)
- Premium/accounts can come later
- Keeps it maximally passive

### Core Data Model

```typescript
interface Palette {
  id: string;
  colors: Color[];
  locked: boolean[];
  createdAt: Date;
  mode: 'immersive' | 'context' | 'mood' | 'playground';
}

interface Color {
  hex: string;
  rgb: { r: number; g: number; b: number };
  hsl: { h: number; s: number; l: number };
  name: string; // "Coral Red", etc.
  locked: boolean;
}

interface UserPreferences {
  defaultMode: Mode;
  soundEnabled: boolean;
  darkMode: boolean;
  recentPalettes: Palette[];
  likedColors: string[]; // For Playground learning
}
```

### URL Structure

```
huego.app/
├── /                    # Landing → redirects to default mode
├── /immersive           # Immersive mode
├── /context             # Context mode
├── /mood                # Mood mode
├── /play                # Playground mode
├── /p/[encoded]         # Shared palette view
└── /export              # Export options
```

### Mode Switching Architecture

```
┌─────────────────────────────────────────┐
│         Global Palette State            │
│  (Zustand store, persisted to localStorage)
└────────────────────┬────────────────────┘
                     │
     ┌───────────────┼───────────────┬───────────────┐
     │               │               │               │
┌────▼────┐    ┌────▼────┐    ┌────▼────┐    ┌────▼────┐
│Immersive│    │ Context │    │  Mood   │    │Playground│
│  View   │    │  View   │    │  View   │    │  View   │
└─────────┘    └─────────┘    └─────────┘    └─────────┘
```

- Palette persists when switching modes
- Each mode is a route with distinct layout
- Smooth animated transitions between modes
- Mode toggle always visible in header

---

## 4. Mode Specifications

### Mode 1: Immersive

**Purpose**: Fast, meditative color exploration

**Interface**:
- Full-screen color swatches (5 columns)
- Minimal chrome - just colors
- Spacebar = generate new palette
- Click color = lock/unlock
- Hover = show hex code
- Optional: ambient sound, subtle animations

**Key Interactions**:
- `Space` - Generate new palette
- `Click` - Lock/unlock color
- `Arrow keys` - Adjust individual color
- `S` - Save palette
- `E` - Export
- `C` - Copy all hex codes

**Visual Style**:
- Colors fill the screen edge-to-edge
- Subtle gradient transitions between colors
- Smooth generation animation
- Dark UI chrome (doesn't compete with colors)

### Mode 2: Context

**Purpose**: See palette applied to real designs

**Interface**:
- Split view: palette (left 30%) + preview (right 70%)
- Context selector: Website, Mobile App, Logo, Dashboard, Social Post
- Real-time updates as colors change
- Role assignment: Primary, Secondary, Accent, Background, Text

**Contexts Available**:
1. **Website**: Hero section, cards, buttons, navigation
2. **Mobile App**: iOS-style UI with your colors
3. **Logo**: Simple logomark with color variations
4. **Dashboard**: Data visualization, charts, cards
5. **Social Post**: Instagram/Twitter post mockup

**Key Interactions**:
- Drag colors to assign roles
- Toggle between contexts
- Generate variations within context
- Export context as image

### Mode 3: Mood

**Purpose**: Start with a feeling, get matching colors

**Interface**:
- Mood selector: grid of feeling words
- Refinement sliders
- Natural language input
- Image upload for inspiration

**Mood Options**:
```
Row 1: Calm | Bold | Playful | Professional
Row 2: Warm | Cool | Retro | Futuristic
Row 3: Natural | Urban | Luxurious | Minimal
```

**Refinement Sliders**:
- Warmer ↔ Cooler
- Subtle ↔ Vibrant
- Light ↔ Dark
- Simple ↔ Complex

**AI Integration** (Future):
- Natural language: "sunset over ocean"
- Image analysis: extract mood from uploaded photo
- Style matching: "like Spotify" or "like Stripe"

### Mode 4: Playground

**Purpose**: Gamified color discovery

**Interface**:
- Tinder-style card swipe
- Building palette through choices
- Progress indicator
- Achievements/streaks (light gamification)

**Mechanics**:
1. Show single color card
2. Swipe right = add to palette
3. Swipe left = skip
4. Build until 5 colors
5. Option to regenerate any slot
6. Share completed palette as "color card"

**Gamification Elements**:
- Daily palette challenge
- Streak counter
- "Color personality" based on preferences
- Shareable results cards

---

## 5. Implementation Plan

### Phase 1: Foundation (Week 1-2)

**Deliverables**:
- [ ] Next.js project setup
- [ ] Zustand store for palette state
- [ ] Color generation algorithms
- [ ] Mode toggle component
- [ ] Basic Immersive mode (MVP)
- [ ] URL sharing (encoded palettes)

**Definition of Done**:
- Can generate palettes in Immersive mode
- Palette persists across page refresh
- Can share palette via URL

### Phase 2: All Modes (Week 3-4)

**Deliverables**:
- [ ] Context mode with 3 preview contexts
- [ ] Mood mode with mood grid + sliders
- [ ] Playground mode with swipe mechanics
- [ ] Smooth transitions between modes
- [ ] Mobile responsive for all modes

**Definition of Done**:
- All 4 modes functional
- Seamless mode switching
- Works on mobile

### Phase 3: Polish & Export (Week 5-6)

**Deliverables**:
- [ ] Export: CSS, Tailwind, Figma, PNG, PDF
- [ ] Accessibility checker
- [ ] Color blindness preview
- [ ] Keyboard shortcuts
- [ ] Sound design (optional ambient)
- [ ] Micro-interactions and animations

**Definition of Done**:
- Professional-quality UX
- All export formats working
- Accessibility features complete

### Phase 4: Monetization (Week 7)

**Deliverables**:
- [ ] Google AdSense integration
- [ ] Premium gate for advanced exports
- [ ] Stripe integration for premium
- [ ] Ad-free premium experience

**Definition of Done**:
- Ads displaying for free users
- Premium subscription working
- Revenue tracking in place

### Phase 5: Growth (Week 8+)

**Deliverables**:
- [ ] SEO optimization
- [ ] Social sharing cards
- [ ] Community palette gallery (optional)
- [ ] Additional contexts for Context mode
- [ ] AI mood analysis (optional)

---

## 6. Critical Files Reference

```
huego/
├── src/
│   ├── app/
│   │   ├── layout.tsx           # Root layout with mode toggle
│   │   ├── page.tsx             # Landing/redirect
│   │   ├── immersive/
│   │   │   └── page.tsx         # Immersive mode
│   │   ├── context/
│   │   │   └── page.tsx         # Context mode
│   │   ├── mood/
│   │   │   └── page.tsx         # Mood mode
│   │   ├── play/
│   │   │   └── page.tsx         # Playground mode
│   │   └── p/[id]/
│   │       └── page.tsx         # Shared palette view
│   ├── components/
│   │   ├── ModeToggle.tsx       # Mode switcher
│   │   ├── ColorSwatch.tsx      # Individual color display
│   │   ├── PaletteBar.tsx       # Horizontal palette view
│   │   ├── ExportModal.tsx      # Export options
│   │   └── contexts/            # Context mode previews
│   │       ├── WebsitePreview.tsx
│   │       ├── MobilePreview.tsx
│   │       └── LogoPreview.tsx
│   ├── lib/
│   │   ├── colors.ts            # Color manipulation utilities
│   │   ├── generate.ts          # Palette generation algorithms
│   │   ├── export.ts            # Export format generators
│   │   └── mood.ts              # Mood → color mapping
│   └── store/
│       └── palette.ts           # Zustand store
├── public/
│   └── sounds/                  # Ambient sounds (optional)
├── tailwind.config.js
└── package.json
```

---

## 7. Context for AI Agents

### Instructions for New Sessions

1. **Read this entire document first**
2. **This project is QUEUED** - Don't start until Crunch MVP is done
3. **Check project-tracker.md** for current status
4. **Do not re-debate decided decisions**
5. **The 4-mode architecture is FINAL** - focus on execution
6. **Update this document** at session end

### Decisions Already Made (DO NOT CHANGE)

- Four modes: Immersive, Context, Mood, Playground
- Stack: Next.js + Tailwind + Zustand + Framer Motion
- No database for MVP (localStorage + URL params)
- Freemium model (ads + premium subscription)
- Mode toggle always visible

### Open Questions (Decide Later)

- Exact premium pricing ($3 vs $5/mo)
- Which contexts to include in Context mode at launch
- Whether to include sound design
- AI integration for Mood mode (or keep it simple)
- Community gallery feature (or skip)

### Common Pitfalls to Avoid

1. **Don't over-engineer generation** - Simple algorithms first
2. **Don't add accounts too early** - localStorage is fine for MVP
3. **Don't skip mobile** - Many users will be on mobile
4. **Don't neglect transitions** - Mode switching should feel magical
5. **Don't make it slow** - Performance is critical for this type of tool

### Color Generation Approaches

```typescript
// Simple complementary
function generateComplementary(baseHue: number): Color[] { }

// Analogous (adjacent hues)
function generateAnalogous(baseHue: number): Color[] { }

// Triadic (evenly spaced)
function generateTriadic(baseHue: number): Color[] { }

// Split-complementary
function generateSplitComplementary(baseHue: number): Color[] { }

// Random with constraints (most common)
function generateRandom(locked: Color[]): Color[] { }
```

---

## 8. Session Log

### 2025-12-13 - Initial Planning
- Researched competitive landscape (Coolors, Adobe Color, etc.)
- Identified UX as key differentiator
- Designed 4-mode architecture
- Named project "HueGo"
- Created this session-start document
- Next: Begin after Crunch MVP ships

---

## Appendix: Competitive Research

### Coolors (Market Leader)
- **Strengths**: Fast, spacebar generation, large library, good exports
- **Weaknesses**: Utilitarian UI, no context preview, no mood-based
- **Monetization**: Freemium ($3/mo), ads

### Adobe Color
- **Strengths**: Color theory tools, Adobe integration
- **Weaknesses**: Locked to Adobe ecosystem, complex
- **Monetization**: Free (drives Adobe CC)

### Khroma
- **Strengths**: AI trained on preferences
- **Weaknesses**: Learning curve, narrow use case
- **Monetization**: Free

### PaletteMaker
- **Strengths**: Context preview feature
- **Weaknesses**: Limited contexts, basic generation
- **Monetization**: Free

### Our Positioning
**"The color palette tool that adapts to you"** - combining the speed of Coolors, the context preview of PaletteMaker, the AI of Khroma, and the fun of a discovery app.

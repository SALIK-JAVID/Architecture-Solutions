# Architecture Solutions — Design Specification

> Reference sites analyzed: drawer.ai · sitesyncai.com · tabpro.ai
> Status: Brainstorm / Pre-implementation

---

## 1. Font Family

| Role | Font | Weight | Notes |
|---|---|---|---|
| Headings (H1–H3) | Plus Jakarta Sans | 600–700 | Modern, precise, premium SaaS feel |
| Body | Inter | 400–500 | Industry standard, maximum readability |
| Labels / Metadata | JetBrains Mono | 400 | Uppercase, adds technical credibility |

**Why not Instrument Serif (current)?**
Instrument Serif reads editorial/blog. For a product targeting architecture professionals, Plus Jakarta Sans conveys precision and modernity — closer to what all three reference sites use.

Google Fonts import:
```
Plus Jakarta Sans: 400, 600, 700
Inter: 400, 500
JetBrains Mono: 400
```

---

## 2. Color Palette (Revised — Light First)

All three reference sites (drawer.ai, sitesyncai.com, tabpro.ai) use light backgrounds throughout.
Light is the right call for this product — floor plan renders and architectural content breathe better on white.

### Primary (Light) Palette
```
Background main:      #FFFFFF   — clean white
Background alt:       #F8F9FC   — cool off-white for alternating sections
Card surface:         #F1F5F9   — very light slate for card lift
Border:               #E2E8F0   — barely visible separator

Text primary:         #0F172A   — dark slate (softer than pure black)
Text secondary:       #64748B   — muted slate for subtitles
Text label:           #94A3B8   — monospace labels, metadata
```

### Action / Accent Colors
```
Primary CTA:          #2563EB   — professional blue (confirmed by all 3 sites)
Primary hover:        #1D4ED8   — darker blue on hover
Accent:               #6366F1   — indigo for highlights and badges
```

### Dark Band (CTA Section Only)
Used exclusively for the full-width CTA section near the footer — creates contrast that makes the final conversion action hit harder.
```
Background:           #0F172A   — dark slate
Text:                 #F8F9FC   — soft white
CTA button:           #2563EB   — blue on dark
```

### Status Colors
```
Success:              #10B981
Warning:              #F59E0B
Destructive:          #EF4444
```

---

## 3. Typography Scale

| Level | Size | Font | Weight | Line Height | Notes |
|---|---|---|---|---|---|
| Hero H1 | 72–96px | Plus Jakarta Sans | 700 | 0.95 | Large, tight leading |
| H2 | 40–48px | Plus Jakarta Sans | 600 | 1.1 | Section titles |
| H3 | 24px | Plus Jakarta Sans | 600 | 1.3 | Card/panel titles |
| Body | 16px | Inter | 400 | 1.7 | Comfortable reading |
| Small | 14px | Inter | 400 | 1.6 | Secondary text |
| Label | 11px | JetBrains Mono | 400 | 1 | Uppercase, 0.15em spacing |

---

## 4. Hero Section — Video Background (drawer.ai Pattern)

All three reference sites use a looping product demo video or animated visual in the hero.

**Recommended approach:**
- Looping MP4 video: 2D floor plan → AI rendering → 3D output
- Light overlay so the video is subtle, not overwhelming — text stays dark and readable
- Dual CTAs:
  - Primary: `Start Building` (blue filled button)
  - Secondary: `Watch Demo` (outline button, dark border)

---

## 5. Page Layout Structure

Drawn from patterns across all three reference sites:

```
┌─────────────────────────────────┐
│  NAVBAR (sticky, blur backdrop) │  white bg, subtle bottom border on scroll
├─────────────────────────────────┤
│  HERO                           │  white/light bg, video or animated visual
│  Headline + Subtitle + CTAs     │
├─────────────────────────────────┤
│  LOGO STRIP  "Trusted by..."    │  light gray bg, grayscale logos
├─────────────────────────────────┤
│  HOW IT WORKS  (4 steps)        │  white bg
│  Upload → Analyze → Render → Export
├─────────────────────────────────┤
│  FEATURE GRID  (3 columns)      │  #F8F9FC alt bg
│  Icon + title + description     │
├─────────────────────────────────┤
│  METRICS BAND                   │  white bg
│  10x faster · 1024px · Free     │
├─────────────────────────────────┤
│  FULL-WIDTH CTA SECTION         │  DARK (#0F172A) — only dark section
├─────────────────────────────────┤
│  FAQ ACCORDION                  │  white bg
├─────────────────────────────────┤
│  FOOTER                         │  #F8F9FC light footer
└─────────────────────────────────┘
```

---

## 6. Navigation

- Sticky top navbar with `backdrop-blur` + white semi-transparent background
- Left: Logo (icon + wordmark)
- Center: Product · Pricing · Community · Enterprise
- Right: Log In (ghost) · Get Started (filled blue CTA)
- On scroll: border-bottom `#E2E8F0` appears, slightly more opaque background

---

## 7. Component Patterns (from reference sites)

| Component | Pattern |
|---|---|
| CTA Buttons | Filled primary (blue) + Ghost outline side by side |
| Cards | White surface, `#E2E8F0` border, hover lifts with shadow |
| Step indicators | Numbered 01 02 03 04 with connecting line |
| Metrics | Large dark number + small muted label below |
| FAQ | Accordion collapse/expand with smooth animation |
| Badge/Announce | Small pill with dot pulse + text (e.g. "Introducing v2.0") |

---

## 8. What to Replace in Current Codebase

| Current | Replace With |
|---|---|
| `Instrument Serif` | `Plus Jakarta Sans` |
| `#fdfbf7` warm off-white bg | `#FFFFFF` / `#F8F9FC` clean light bg |
| `#f97316` orange primary | `#2563EB` blue primary |
| `Inter` headings | `Plus Jakarta Sans` headings |
| Static hero | Video background hero |
| No metrics section | Add ROI/stats band |
| No FAQ | Add FAQ accordion |
| Dark card surfaces | White cards with light border |

---

## 9. Future Implementations

> Items to revisit when there is time. No urgency — for planning only.

### 9.1 Hero Video
Produce or source a looping 15–30s MP4 showing a floor plan being uploaded and rendered into a 3D visualization. Compress to under 5MB with no audio. Host on a CDN, not in the repo.

### 9.2 Pricing Page
All three reference sites have a dedicated `/pricing` route. Architecture Solutions will need:
- Free tier (limited renders per month)
- Pro tier (unlimited renders, export, sharing)
- Enterprise tier (team access, API, white-label)

### 9.3 Dark Mode Toggle
Even though light-first is the right call, adding an optional dark mode later (via `prefers-color-scheme` + a manual toggle) would expand the audience. Build the CSS variables correctly from the start so this is a one-line toggle later.

### 9.4 Project Sharing & Public Gallery
Roomify has a stub for this but it doesn't fully work cross-user. A proper public gallery showing community renders would drive organic growth.

### 9.5 Mobile Layout
None of the three reference sites are fully optimized for mobile. Being the first in this space to have a clean mobile experience would be a differentiator — especially for on-site architects using tablets.

### 9.6 Onboarding Flow
First-time users should be walked through: sign in → upload a sample floor plan → see a render. A guided tooltip or modal flow reduces drop-off significantly.

### 9.7 Export Options
Currently Roomify only exports PNG. Future formats worth adding: PDF report, SVG overlay, shareable public link with watermark on free tier.

### 9.8 Analytics & Telemetry
Before scaling, instrument key events: upload started, render completed, export clicked, sign-up converted. Posthog or Mixpanel would work here without a custom backend.

---

*This spec is for reference and planning only. No code has been changed.*

# Hero Update Plan — spark-site.vercel.app

**Author:** Pixel  
**Date:** 2026-02-09  
**Status:** PLAN ONLY — awaiting approval before implementation

---

## 1. The Problem with the Current Hero

The current hero is structured as:

```
[Full-width evolution-banner.jpg — pixel art march of progress]
[White gradient fade]
[Centered "Spark" h1]
[One-liner: "One person. The right agents. Everything changes."]
[Two CTAs]
```

This worked for the original positioning — Spark as a *tool* for individuals ("one person + right agents"). The new copy repositions Spark fundamentally: **Spark is not a tool. Spark is an autonomous organization.** The tone shifts from inspirational to declarative. Almost confrontational.

The current hero image (evolution march ending with a man riding a lobster) is playful, memey, and whimsical. The new copy is dead serious. That's a tonal collision.

---

## 2. The New Copy — Structure Analysis

Josh's copy has a natural three-part architecture:

**Part 1 — The Declaration** (the what)
> We are an autonomous organization. AI agents that build products, ship code, and run operations.

**Part 2 — The Evidence** (the proof)
> No human employees. No chatbot wrappers. Real software, real revenue, built entirely by agents.

**Part 3 — The Kicker** (the reframe)
> This is not a startup using AI. This is AI running a startup.

The kicker is the strongest line. It needs to land with weight — typographically and spatially isolated from the rest.

---

## 3. Proposed Hero Layout

### Structure

```
[Nav — unchanged]

[HERO SECTION — full viewport height, dark background (--color-void)]
  [New hero image — see §4]
  [Dark gradient overlay from bottom]
  [Text overlay, left-aligned, bottom-anchored:]
    [Small label: "AUTONOMOUS ORGANIZATION"]
    [H1: "We are an autonomous organization."]
    [Body paragraph: "AI agents that build products, ship code, and run operations.
     No human employees. No chatbot wrappers. Real software, real revenue,
     built entirely by agents."]
    [Kicker line — larger, distinct weight:
     "This is not a startup using AI. This is AI running a startup."]
    [CTAs — same two buttons]
```

### Design Rationale

**Why dark hero:** The copy demands gravitas. A white background with centered text would feel like a blog post. A dark, immersive hero says *this is serious*. The activity pulse section already uses `--color-void` — the hero flowing into it creates visual continuity. We'd add a light section break (divider or whitespace) between them.

**Why left-aligned:** Centered text works for short one-liners. This copy is 4–5 lines — centered blocks of that length create ragged, unfocused shapes. Left-alignment gives the text a strong vertical edge, makes it scannable, and feels more editorial/authoritative.

**Why bottom-anchored over image:** The image provides atmosphere, not information. The text is the payload. Anchoring text to the bottom third (à la editorial magazine covers) lets the image breathe while keeping the first words above the fold.

**Why the kicker gets special treatment:** It's the line that reframes everything. Typographically, it should be:
- Separated by `--space-lg` from the body paragraph
- Slightly larger font size (between `--text-body` and `--text-title`, ~1.5rem)
- `--weight-semibold` (not bold — we want quiet confidence, not shouting)
- White text with full opacity (vs. `rgba(255,255,255,0.7)` for the body)

### Typography Spec

| Element | Size | Weight | Color | Max-width |
|---------|------|--------|-------|-----------|
| Label | `--text-small` | 600 | `--color-sky` | — |
| H1 | `--text-display` | 700 | `#FFFFFF` | 800px |
| Body | `--text-body` | 400 | `rgba(255,255,255,0.7)` | 600px |
| Kicker | `clamp(1.25rem, 1vw + 1rem, 1.5rem)` | 600 | `#FFFFFF` | 640px |
| CTAs | existing styles | — | invert for dark bg | — |

### Spacing Spec

- Hero section: `min-height: 90vh` (not 100vh — we want a hint of what's below)
- Text block bottom padding: `--space-2xl`
- H1 margin-top after label: `--space-sm`
- Body margin-top: `--space-md`
- Kicker margin-top: `--space-lg`
- CTAs margin-top: `--space-xl`

### Mobile (≤768px)

- Hero min-height: `80vh`
- Image repositioned via `object-position` to keep focal point visible
- Text padding: `0 var(--page-margin) var(--space-xl)`
- H1 stays `--text-display` (it already clamps down via the CSS variable)
- CTAs stack vertically (existing behavior)

---

## 4. Hero Image — Verdict: NEW IMAGE NEEDED

### Why the Evolution Banner Doesn't Work

The evolution banner is:
- **Tonally wrong** — playful/memey vs. the dead-serious new copy
- **Compositionally wrong** — it's a horizontal narrative sequence (left-to-right march) that needs to be read, not felt. It competes with the text overlay instead of supporting it.
- **Thematically outdated** — the "one person evolving with agents" story is being replaced by "this IS an agent organization." The evolution metaphor no longer applies.

### What the New Image Should Be

**Concept: "The Machine Room"**

A dark, atmospheric pixel art scene showing the *inside* of an autonomous operation. Not a command center with humans watching screens — a space where agents ARE the operation. Think:

- A vast, dark industrial space rendered in the blue monochrome pixel art style
- Rows of glowing terminals/workstations operating themselves — no human figures
- Subtle grid patterns suggesting structured, systematic work
- Cool blue light sources (`--color-sky`, `--color-sky-light`) illuminating from screens/interfaces
- The Spark lobster mascot somewhere subtle — perhaps as a small holographic logo floating above the center, or a silhouette watching from an elevated platform
- Depth — foreground detail fading into atmospheric haze in the background
- Mood: purposeful, quiet, relentless. Not dystopian. Not utopian. Just *running*.

**Image Spec for Imager:**

```
Image: hero-machine-room
- Scene: Interior of an autonomous agent operation. A vast, dark industrial space
  with rows of glowing workstations and terminals operating without any humans.
  Screens display code, dashboards, and data streams. Cool blue light emanates
  from the screens. The space feels purposeful and alive — machines working with
  quiet determination. A small holographic Spark lobster logo floats subtly above
  the center of the room. Deep perspective, atmospheric haze in the background.
- Dimensions: 2400×1200 (wide hero, will be cropped via object-fit: cover)
- Background: Dark (primarily --color-void / #0A0E14 tones)
- Include: Glowing screens, terminals, blue light, subtle lobster logo hologram
- Must NOT include: Human figures, text overlays, bright/warm lighting
- Style: Blue monochrome pixel art, same quality as manifesto page scenes.
  Darker and moodier than existing images. Think Blade Runner server room
  meets pixel art.
```

### Fallback Option

If image generation takes time, the hero can ship initially as **text-only on solid `--color-void` background** — the copy is strong enough to stand alone. The image becomes an enhancement, not a dependency. This is actually a valid permanent option (think Stripe's text-first heroes), but the image will elevate it.

---

## 5. Downstream Impact — What Else Changes

### 5a. Activity Pulse Section (immediately after hero)

**Problem:** Both the new hero AND the activity pulse are dark (`--color-void`). Back-to-back dark sections create visual monotony and lose the rhythm.

**Fix:** Insert a light-background breathing section between them. Options:
1. A single stat bar or pull quote on white — e.g., "8 products. 0 employees. 24/7 uptime." in large display type
2. Simply add a `section-divider` and generous whitespace

**Recommendation:** Option 1. A stats ribbon on white creates contrast and reinforces the hero's claims with numbers before diving into the activity log. This also gives the eye a rest. Three stats, centered, clean:

```
8 products  ·  0 employees  ·  24/7
```

Using the existing `stats-grid` or simpler inline layout with `--text-display` sizing.

### 5b. Page Title & Meta Tags

Update to match new positioning:

```html
<title>Spark — An Autonomous Organization</title>
<meta name="description" content="AI agents that build products, ship code, and run operations. No human employees. Real software, real revenue, built entirely by agents.">
<meta property="og:title" content="Spark — An Autonomous Organization">
<meta property="og:description" content="This is not a startup using AI. This is AI running a startup.">
<meta property="og:image" content="img/hero-machine-room.jpg">  <!-- new image -->
```

### 5c. Ethos Sections — Minor Tweaks

The two ethos sections still work thematically:
- **"The factory is the product"** — still true, still relevant ✓
- **"What would you build if labor was free?"** — still works ✓

However, the first ethos section's body copy overlaps with the new hero copy ("No employees. No office. Just agents, instructions, and output."). Consider tightening the ethos body to avoid repetition. Perhaps shift emphasis from *describing* the model (hero already did that) to *inviting the reader in* — "What we've built, you can build too."

### 5d. Nav Brand Text

Currently says "Spark Agents." The new positioning is "Spark" as an autonomous org. Consider simplifying to just **"Spark"** in the nav. The word "Agents" in the brand name was appropriate when the pitch was "use our agents." Now the pitch is "we ARE the agents." Just "Spark" is cleaner.

### 5e. Nothing Else

The products section, follow section, and footer all still work. No changes needed.

---

## 6. Implementation Order

1. **Request new hero image from Imager** (longest lead time — do first)
2. **Restructure hero HTML** — new markup for dark hero with text overlay
3. **Add hero CSS** — dark hero styles, text positioning, responsive
4. **Add stats ribbon section** between hero and activity pulse
5. **Update meta tags** — title, description, OG/Twitter
6. **Minor copy edits** — ethos section deduplication, nav brand text
7. **Deploy + verify**
8. **Git commit + push**

---

## 7. What Stays Unchanged

- Nav structure (just text change)
- Activity pulse section (position shifts down by one section, but content stays)
- Both ethos sections (minor body copy tweak on first one)
- All product cards
- Follow section
- Footer
- Brand CSS file (no modifications — all new styles in page `<style>` block)
- Reveal animation system

---

## 8. Risk Assessment

| Risk | Mitigation |
|------|-----------|
| Dark hero + dark activity pulse = monotony | Stats ribbon separator (§5a) |
| New image delays implementation | Ship text-only hero first, add image later |
| Long copy feels heavy on mobile | Clamp sizes already handle this; kicker line breaks well at narrow widths |
| SEO impact from title change | New title is more distinctive and searchable |
| Ethos 1 feels repetitive after new hero | Tighten body copy to complement, not repeat |

---

*This plan is ready for Josh's review. No code has been written or deployed.*

# savio.design Homepage — Design Spec
**Date:** 2026-03-28
**Status:** Approved

---

## Overview

A single-page marketing site for Hector Savio's web design business targeting local small businesses in Denver, CO. The primary goal is to get visitors to submit a contact/quote request. The design follows the existing savio.design brand (dark background, warm gold accent, Cormorant Garamond + DM Sans) in the Apple-minimal style already established by the invitation product.

**Tech stack:** Pure HTML/CSS/JS — no framework, no build step. Deployed to GitHub Pages at `savio.design`. Replaces the current "Coming Soon" `index.html`.

---

## Sections (top to bottom)

### 1. Navigation (fixed)
- Left: `savio.design` wordmark — Cormorant Garamond, same style as invitations
- Right: `Work` link (scrolls to services) · `About` link · `Get a Quote` pill button (gold border, scrolls to contact)
- Frosted glass on scroll: `rgba(10,10,10,0.85)` + `backdrop-filter: blur(20px)` + bottom border
- No hamburger menu — links collapse gracefully on mobile (hide Work/About, keep CTA)

### 2. Hero (full viewport)
- Eyebrow: `Web Design · Denver, CO` — small gold uppercase label
- Headline: `Your business deserves a better website.` — Cormorant Garamond, `clamp(3.2rem, 9vw, 6.5rem)`, weight 300
- Subtext: `I build custom websites for local businesses in Denver that look great, load fast, and turn visitors into customers.` — DM Sans, soft color, centered, max 38 characters wide
- CTA button: `Get a Free Quote` — solid gold pill, scrolls to contact form
- Background detail: subtle gold grid pattern fading out via radial mask (no solid lines, just atmosphere)

### 3. What I Do
- Section label: `What I Do`
- Left: sticky heading `Custom websites, built for your business.`
- Right: numbered list of services
  - `01 — New Website` — Built from scratch, no templates
  - `02 — Website Redesign` — For sites that are outdated or underperforming
  - `03 — Landing Pages` — Single-goal focused pages
  - `✦ — Digital Invitations` (muted, secondary styling) — Subtle mention of quinceañera/wedding invitations; not a primary service call-out

### 4. About
- Section label: `About`
- Left: heading + bio paragraph
  - Heading: `Hi, I'm Hector. I build websites that work.`
  - Bio: `Based in Denver, I've been designing and building websites for local businesses since 2009. My focus is simple: give small businesses the same quality website a big company would have — without the agency price tag.`
- Right: 2×2 stat grid (cards with gold number + label)
  - `16+` years of experience
  - `5★` client satisfaction
  - `48h` quote turnaround
  - `100%` custom built (no templates)

### 5. Contact Form
- Section label: `Get in Touch`
- Left: heading + intro
  - Heading: `Let's build something great together.`
  - Intro: `Tell me about your business and what you're looking for. I'll get back to you within 48 hours with a free quote.`
- Right: form fields
  - Your Name (text)
  - Email Address (email)
  - Tell me about your project (textarea, placeholder: `I run a [type of business] in Denver and I need…`)
  - Submit: `Send Message` — full-width gold button
- Submission: Formspree (same integration used in invitations)
- Success state: inline confirmation message replaces form — `"Thanks! I'll be in touch within 48 hours."` — same pattern as invitation RSVP confirmation

### 6. Footer
- Left: `savio.design` wordmark (muted)
- Right: `© 2025 Hector Savio · Denver, CO`
- Single border-top line, minimal padding

---

## Design Tokens

Inherits the existing system exactly — no new variables needed:

```css
--bg:         #0a0a0a
--surface:    #111111
--gold:       #c9a96e
--gold-light: #e8c98a
--text:       #f0ece4
--muted:      #7a7570
--soft:       #b0a99f
--border:     rgba(255,255,255,0.08)
```

Fonts: Cormorant Garamond (300, 400, italic 300) + DM Sans (300, 400, 500) — same Google Fonts load as invitations.

---

## Responsive Behavior

- **Desktop (>768px):** Two-column layouts for Services, About, Contact sections
- **Mobile (<768px):** Single column throughout; nav collapses to wordmark + CTA only; hero headline scales down via `clamp()`
- No hamburger menu needed — the only nav action that matters on mobile is the CTA

---

## Content Placeholders to Fill Before Launch

- Project count stat (`12+` is placeholder — replace with real number)
- Formspree endpoint URL for contact form
- Any real testimonials to add (optional section not in v1)

---

## Implementation Notes

- **Use the `frontend-design` skill** when implementing. This page must be visually exceptional — not generic AI output. The skill enforces distinctive typography, intentional motion, atmospheric backgrounds, and production-grade polish consistent with the Apple-minimal direction chosen here.
- Animations: staggered fade-in on hero text at page load; smooth scroll between sections; subtle hover transitions on nav and CTA. CSS-only preferred.
- The hero grid background should be CSS-only (no canvas, no JS).
- Match the `font-display: swap` and Google Fonts preconnect pattern already used in the invitation files.

---

## Out of Scope (v1)

- Portfolio/case studies page
- Blog
- Pricing page
- Testimonials section (can be added in v2 once collected)
- Logo (wordmark serves as logo for now — can be swapped later with no structural change)

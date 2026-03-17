# Florida Panthers Venue Audience Intelligence
### Amerant Bank Arena — Hospitality & F&B RFP Research Tool

**Version:** 1.0 (Preliminary — pre-ticketing data)
**Date:** March 2026
**Classification:** Confidential

---

## Overview

This is a single-file, password-protected HTML web application built to support an RFP response for hospitality, concessions, and premium F&B operations at **Amerant Bank Arena** in Sunrise, Florida — home of the Florida Panthers NHL franchise.

The tool presents market intelligence, audience personas, and bidder strategy in an interactive slide-format report. It is designed to be shared internally as a standalone file — no server, no build step, no dependencies beyond a modern browser.

This is a **preliminary analysis** built on publicly available data. It is explicitly designed to be updated and refined once Acxiom-enriched ticketing data is available.

---

## Access

**Password:** `panthers2026`

The password gate uses client-side SHA-256 hashing via the Web Crypto API. The plaintext password is never stored anywhere in the file — only the hash. Session state is maintained via `sessionStorage` so users are not re-prompted on page refresh within the same browser session.

---

## Data Sources

This preliminary version draws on three primary sources:

| Source | What it covers |
|---|---|
| U.S. Census ACS 2024 | Population, income, race, education, and homeownership for Broward, Miami-Dade, and Palm Beach counties |
| NHL Fan Research (S&P Global, SBRnet, Morning Consult, NHL D&I Report) | National fan demographics: age, income, gender, education, ethnicity |
| South Florida Cultural & Culinary Analysis | Cuban/Latin food culture, local restaurant landscape, event programming at Amerant Bank Arena |

**What's missing (pending):** Acxiom-enriched ticketing records. Once received, the buyer median income, gender split, Personicx lifestage segments, homeownership rates, family structure, and education levels should be layered in to sharpen all six persona profiles and confirm or challenge the census-vs.-buyer gap analysis on the Data Analysis slide.

---

## File Structure

The entire application is a single self-contained HTML file:

```
florida-panthers-intelligence.html
```

No external JavaScript libraries, no CSS frameworks, no API calls. The only external dependency referenced is the `fonts/` directory containing the Nicky Sans typeface family (`.otf` files). If those fonts are unavailable, the browser falls back gracefully to Georgia and system-ui.

### Expected folder structure for full font support:
```
florida-panthers-intelligence.html
fonts/
  NickySans-Light.otf
  NickySans-Regular.otf
  NickySans-Medium.otf
  NickySans-SemiBold.otf
  NickySans-Bold.otf
  NickySans-ExtraBold.otf
```

---

## Navigation

The app uses a two-tier fixed navigation bar:

- **Tier 1 (top row):** Chapter tabs — Overview, South Florida, Analysis, Personas, Strategy
- **Tier 2 (bottom row):** Contextual sub-page pills that update based on which chapter is active

Navigation also responds to:
- **Scroll** — active chapter and sub-page update automatically via IntersectionObserver
- **Keyboard** — Arrow keys and Page Up/Down move between slides
- **Touch** — Both nav rows are horizontally scrollable on mobile

---

## Content Chapters

### Overview
- **Cover** — scope, data summary, preliminary data notice
- **Methods** — three data pillars: Census ACS, NHL fan research, South Florida cultural analysis
- **At a Glance** — key market stats snapshot for Amerant Bank Arena

### South Florida
- **South Florida Market** — the NHL fan paradox in a majority-minority metro; Panthers attendance growth trajectory
- **Food Culture** — Cuban/Latin culinary identity as the market baseline, not a specialty offering; the transplant factor; local restaurant competitive landscape
- **Event Mix** — six event types (Panthers hockey, Latin music, major concerts, Disney on Ice/family shows, Monster Jam/PBR, corporate events) with F&B implications for each

### Analysis
- **Census vs. Buyer Data** — anticipated gaps between the likely Panthers buyer sample and the actual tri-county population, with strategic implications for each dimension

### Personas
- **All Personas** — overview grid of all six profiles
- **Individual persona slides** — full detail on who they are, life stage, concession recommendations, and premium dining/club recommendations

### Strategy
- **How to Win the Bid** — do/don't grid focused on Latin cultural fluency as the price of admission
- **Premium F&B Strategy** — suite and club-specific do/don't grid; the 74-suite, 2,623-club-seat economic case
- **Key Takeaways** — four core strategic conclusions

---

## The Six Personas

| Persona | Primary Venue Context | Approx. Share |
|---|---|---|
| The Transplant Season Ticket Holder | Panthers hockey core | ~25% |
| The South Florida Latin Fan | Panthers hockey, growing | ~20% |
| The Corporate Suite Host | Suites & premium | ~12% |
| The South Florida Family | All event types | ~22% |
| The Younger Hispanic Convert | Latin music events | ~18% |
| The Comfortable Empty Nester | Panthers hockey, concerts | ~13% |

Persona shares are estimates based on national NHL fan research and South Florida demographic data. They will be recalibrated once ticketing data is analyzed.

---

## Brand Colors

All colors adhere to the official Florida Panthers palette:

| Color | Hex | Usage |
|---|---|---|
| Navy | `#041E42` | Primary background, nav, dark slides |
| Red | `#C8102E` | Primary accent, South Florida chapter, CTA elements |
| Tan/Gold | `#B9975B` | Secondary accent, Overview/Strategy, overview nav wordmark |

Persona cards also use secondary colors (light blue, teal, purple, coral) chosen for readability against both dark and light backgrounds. A `displayColor` property is used for dark-background contexts (persona overview grid, takeaway cards) and `accentColor` for light-background detail slides, ensuring WCAG-appropriate contrast in both contexts.

---

## Updating for Ticketing Data

When Acxiom-enriched buyer records are available, the following sections should be revised:

1. **At a Glance (Slide 3)** — replace estimated buyer income with actual Acxiom median; add actual gender split, education level, homeownership rate, and family structure from the buyer file
2. **Data Analysis table (Slide 7)** — update the "NHL national data suggests" column with actual buyer data; the "strategic implication" column may also need revision once the real gap size is known
3. **All six persona profiles** — refine age ranges, income brackets, Personicx segment labels, and share estimates
4. **Cover slide metadata** — replace "1.2M+ annual visitors" framing with actual buyer record count once ticketing data is in hand

To update a persona, find the relevant object in the `personas` array in the `<script>` block and edit the fields directly. The UI is generated from that data object — no HTML editing required for persona content changes.

---

## Changing the Password

1. Choose a new password
2. Generate its SHA-256 hash — e.g., in terminal: `echo -n "yournewpassword" | sha256sum`
3. Replace the `HASH` constant near the bottom of the `<script>` block:
```javascript
const HASH = 'paste_new_hash_here';
```
4. Update this README and notify recipients of the new password separately

---

## Technical Notes

- **No build required** — open the `.html` file directly in any modern browser
- **No internet required** — entirely self-contained; works offline
- **Mobile-optimized** — responsive layouts for tablet and iPhone; iOS safe-area insets handled; minimum 44px touch targets on nav
- **Keyboard accessible** — full slide navigation via arrow keys and Page Up/Down
- **Print** — not optimized for print; this is an interactive screen document
- **Browser support** — all modern browsers (Chrome, Safari, Firefox, Edge); requires Web Crypto API for the password gate (available in all modern browsers over HTTPS or localhost)

---

## Iteration History

| Version | Date | Notes |
|---|---|---|
| 1.0 | March 2026 | Initial build — preliminary analysis, no ticketing data. Panthers brand colors applied (`#041E42`, `#C8102E`, `#B9975B`). Contrast fixes applied to dark-background persona cards. |

---

*This document is confidential and intended for internal use only in connection with the Florida Panthers hospitality RFP process.*

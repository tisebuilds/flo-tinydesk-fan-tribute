# PRD: FLO Tiny Desk Micro-Site

**Version:** 0.2 (Updated Prototype)
**Date:** April 2026
**Author:** Tise (tisebuilds.com · @tisebuilds)

---

## Overview

A two-page fan micro-site celebrating FLO's February 20, 2026 NPR Tiny Desk Concert. The site is editorial, bold, and brand-aligned — drawing directly from NPR Tiny Desk's stark black/white/red typographic identity and FLO's vibrant red, cream, and black visual language. It functions as an archival celebration of the set, a curated Vevo live performance archive, and a personal creator page from the builder.

---

## Goals

- Celebrate and archive FLO's Tiny Desk debut in a format worthy of the performance
- Give fans a place to listen to audio from the set (drag-and-drop player)
- Surface FLO's full Vevo live catalogue (7 confirmed videos) to deepen discovery
- Encourage sharing of the NPR set link
- Introduce the creator (Tise) through a personal about page

---

## Non-Goals

- Not a general FLO fansite — scoped to this Tiny Desk performance moment + creator context
- No user accounts, comments, or dynamic backend
- No e-commerce or streaming affiliate links
- No server-side rendering — fully static

---

## Tech Stack

- Two static HTML files — `flo-tiny-desk.html` (main) + `about.html` (creator page)
- Google Fonts: **Playfair Display** (editorial serif) + **Inter** (clean sans)
- Vanilla JS only — drag-and-drop audio, clipboard API, generative disco dots
- YouTube thumbnail CDN (`img.youtube.com/vi/{id}/hqdefault.jpg`) for Vevo card images — zero hosting cost
- Fully static — deployable to GitHub Pages, Vercel, or Netlify with no build step

---

## Site Map

```
flo-tiny-desk.html   ← Main concert page
about.html           ← Creator page
```

Both pages share: the same fixed nav, design tokens, and typography system.

---

## Page 1: The Concert (`flo-tiny-desk.html`)

### Navigation (shared, fixed)
**Purpose:** Persistent wayfinding across both pages.

**Content:**
- Left: `FLO.` logotype (Playfair Display 900, red dot) — links to main page
- Right: `The Concert` | `About` text links
- Active state: white text + 2px red underline

**Design notes:**
- Fixed to top, `z-index: 100`
- `backdrop-filter: blur(12px)` with 92% opacity black background
- 1px white border at 10% opacity on bottom
- Height: 52px

---

### 1. Hero
**Purpose:** Immediate visual impact. Sets the editorial tone.

**Content:**
- Solid red pill label: `NPR Music · Tiny Desk Concert · Feb 20, 2026`
- Large editorial logotype: `FLO` (Playfair Display 900, ~220px)
- Italic subtitle in red: `Access All Areas`
- Member names: Stella Quaresma · Renée Downer · Jorja Douglas
- Ambient disco sparkle dots (generative JS, red + white)
- Scroll CTA → anchors to `#setlist`

**Design notes:**
- Full-viewport height; 4px solid red bar pinned at very top (NPR brand mark)
- Red radial glow from top centre (not gold — pure FLO/NPR red)
- Marquee label is a solid red filled block, not a bordered pill

---

### 2. Scrolling Ticker
**Purpose:** Visual transition / energy between hero and content.

**Content:** Full 7-track setlist looping horizontally. White text, square `■` separators.

**Design notes:**
- Full-width red background band — most NPR-forward visual element on the page
- Font weight 700, all-caps, 0.3em tracking
- CSS `translateX` animation only — no JS

---

### 3. The Set
**Purpose:** Tracklist + audio player. Core functional section.

**Background:** `--off-black` (alternating)

**Content:**
- NPR-style red chip eyebrow: `The Set`
- Title: `Seven songs. No skips.`
- 7 track rows: track number (white at 12% opacity), song name (Playfair 700), source badge
- Badge types: `Single` (white border) · `Album` (white border) · `Unreleased` (red border + red text)
- Unreleased tracks 06–07 at 75% opacity
- Audio player bar: play/pause (red circle), now-playing label, progress bar stub
- Drag-and-drop zone for MP3/WAV/M4A local files

**Setlist:**

| # | Track | Source | Badge |
|---|---|---|---|
| 01 | Cardboard Box | Debut Single · Reimagined | Single |
| 02 | AAA | Access All Areas, 2024 | Album |
| 03 | On & On | Access All Areas, 2024 | Album |
| 04 | Get It Till I'm Gone | Access All Areas, 2024 | Album |
| 05 | Shoulda Woulda Coulda | Access All Areas, 2024 | Album |
| 06 | Therapy at the Club | Unreleased | Unreleased |
| 07 | HaterBooth | Unreleased | Unreleased |

**Behaviour:**
- Click track row → updates "Now Playing" label
- Drag audio file onto drop zone → plays via Web Audio API (`URL.createObjectURL`)
- Play/pause toggle with SVG icon swap
- `audioEl.ended` resets play button state

**v1 todos:**
- Bind track rows directly to individual audio files by filename convention
- Real progress bar via `timeupdate` + `duration`
- Optional: WaveSurfer.js waveform visualiser

---

### 4. Watch The Set
**Purpose:** Drive traffic to the full NPR video.

**Content:**
- 2-col layout: video thumbnail placeholder (left) + copy + CTAs (right)
- Primary CTA: `Watch on NPR` → https://www.npr.org/2026/02/20/g-s1-97283/flo-tiny-desk-concert
- Secondary CTA: `More Tiny Desks` → https://www.npr.org/series/tiny-desk-concerts/
- Metadata: February 20, 2026 · NPR Music · Washington, D.C.
- Video play icon: red-filled circle with white play arrow (updated from gold outline)

**v1 todos:**
- Replace placeholder with YouTube `<iframe>` embed once video ID is confirmed
- Lazy-load iframe (`loading="lazy"`)

---

### 5. Share This Set *(inline strip)*
**Purpose:** Frictionless sharing — deliberately not a full section.

**Content:**
- `Share this set` label
- Tweet button → pre-filled tweet with NPR URL
- Copy Link → clipboard API with "Copied!" fade confirmation

**Notes:** Sits beneath the Watch section at full content width. No social icons, no section header — editorial restraint.

---

### 6. Live on Vevo
**Purpose:** Surface FLO's full Vevo live canon. Discovery layer for new fans.

**Background:** `--off-black` (alternating)

**Layout:** 1 featured hero card (full-width 2-col) + 3×2 grid = 7 total

**Featured card — Check | Live from Vevo Studios:**
- Left: YouTube thumbnail (`img.youtube.com/vi/QJR77KB1wq4/hqdefault.jpg`)
- Right: series label, title, year, "Watch on YouTube ↗" CTA
- Links to: https://www.youtube.com/watch?v=QJR77KB1wq4

**Grid cards (6):**

| Song | Series | Year | YouTube ID | Link |
|---|---|---|---|---|
| Bending My Rules | Live from Vevo Studios | 2024 | `XBnJ3mLQJ5w` | [Link](https://www.youtube.com/watch?v=XBnJ3mLQJ5w) |
| Feature Me | Vevo DSCVR · Artists to Watch 2023 | 2022 | `Laz2udZieRM` | [Link](https://www.youtube.com/watch?v=Laz2udZieRM) |
| Not My Job | Vevo DSCVR · Artists to Watch 2023 | 2022 | `B7xmqFBuK9k` | [Link](https://www.youtube.com/watch?v=B7xmqFBuK9k) |
| Immature | Vevo DSCVR | 2022 | `4yC_2n9VIVY` | [Link](https://www.youtube.com/watch?v=4yC_2n9VIVY) |
| Cardboard Box | Vevo DSCVR | 2022 | `pCOyYgvEfTk` | [Link](https://www.youtube.com/watch?v=pCOyYgvEfTk) |
| Cardboard Box (Acoustic) | Live Acoustic | — | `pfTbj43Dkjc` | [Link](https://www.youtube.com/watch?v=pfTbj43Dkjc) |

**Badge system:**
- `DSCVR` → red background, white text
- `Vevo Studios` → red background, white text
- `Acoustic` → dark background, white text + white border

**Thumbnails:** Pulled live from YouTube CDN — no hosting cost, always current.

**Footer link:** → Full playlist https://www.youtube.com/playlist?list=PLkqz3S84Tw-QNH0mcv-G8lsq6xnEcalw1

---

### 7. The Girls
**Purpose:** Brief artist context. Closes the concert page.

**Content:**
- 2-col: performance description copy (left) + member card stack (right)
- Member cards: Stella Quaresma / Renée Downer / Jorja Douglas — initial avatar (red circle), name, role, red `FLO` tag

---

### 8. Footer
**Content:**
- `FLO.` logotype — red dot
- Disclaimer: fan tribute, not affiliated with NPR or FLO's management
- Link to NPR set page

---

## Page 2: About (`about.html`)

### Navigation
Same fixed nav as main page. `About` link has active state.

---

### 1. Hero
**Layout:** 2-col — creator intro (left) + stats block (right)

**Left:**
- Red chip eyebrow: `About the Creator`
- `Hey, I'm` italic in red + `Tise` in large Playfair 900
- Short tagline
- CTAs: `tisebuilds.com ↗` (red filled) · `@tisebuilds ↗` (white outline)

**Right — Stats block (3 cards):**

| Stat | Label |
|---|---|
| 3 | FLO concerts attended — all NYC |
| 2 | Favourite tracks — Immature & On & On |
| 1 | Tiny Desk to celebrate — Feb 20, 2026 |

---

### 2. Live Experiences — Three NYC Concerts
**Layout:** Stacked card list (3 rows)

| # | Date | Venue | Tag | Status |
|---|---|---|---|---|
| 01 | April 19, 2023 | Webster Hall | Sold Out | Memory placeholder |
| 02 | June 2024 | Gov Ball After Dark | Festival | Memory placeholder |
| 03 | April 21, 2025 | Brooklyn Paramount | Headline Tour | Memory placeholder |

Each card: track-number-style dim count, date in red, venue name in Playfair 700, memory copy (user to fill), concert tag.

**v1 todo:** Replace placeholder memory text with personal recollections. Optional: add a phone photo per concert.

---

### 3. Songs That Live Rent-Free
**Layout:** 2-col song cards

| # | Track | Album | Notes |
|---|---|---|---|
| 1 | Immature | The Lead EP, 2022 | Placeholder — user to fill |
| 2 | On & On | Access All Areas, 2024 | Placeholder — user to fill |

**v1 todo:** Expand to 3–4 songs if desired.

---

### 4. Why I Built This
**Layout:** 2-col — personal copy (left) + suggestions sidebar (right)

**Left:** 3 paragraphs — origin story (prototype copy, user to personalise with their own voice)

**Right — Suggestions sidebar** (5 items, can be removed once content is filled):
- Discovery story — how Tise first found FLO
- Concert photos — one shot from any of the three shows
- What's next — upcoming music, tours, collabs
- A "start here" rec for new fans
- A favourite FLO lyric styled large

---

### 5. Connect
**Layout:** 2-col link cards

| Card | URL | CTA |
|---|---|---|
| Portfolio | https://tisebuilds.com | Visit site ↗ |
| Twitter / X | https://twitter.com/tisebuilds | Follow ↗ |

---

### 6. Footer
- `FLO.` logotype (red dot)
- "Built by Tise" credit with portfolio link
- Disclaimer + `← Back to the concert` link

---

## Design System

### Color Tokens

| Token | Value | Usage |
|---|---|---|
| `--black` | `#080808` | Page background |
| `--off-black` | `#101010` | Alternating section bg |
| `--card-bg` | `#181818` | Card / component bg |
| `--red` | `#e01f26` | Primary accent — FLO/NPR red |
| `--red-dark` | `#b5181e` | Hover state for red elements |
| `--red-dim` | `rgba(224,31,38,0.15)` | Subtle red glow / bg tint |
| `--white` | `#f5f5f5` | Primary text |
| `--cream` | `#f0ebe3` | Reserved — warm text accent |
| `--muted` | `#666666` | Secondary / metadata text |
| `--border` | `rgba(255,255,255,0.10)` | Structural borders |
| `--border-strong` | `rgba(255,255,255,0.18)` | Emphasized borders |

> **No gold.** The previous v0.1 palette used `#c9a84c` gold as the primary accent. This was replaced entirely with the NPR/FLO brand red + white system.

### Brand References

**NPR Tiny Desk:**
- 4px red bar at very top of hero (`::after` pseudo-element)
- Section eyebrows as solid red filled chips (not bordered labels)
- Ticker is a full red background band with white text — most explicit NPR reference
- High-contrast black/white/red — no warm tones

**FLO (Access All Areas era):**
- Primary red `#e01f26` matches FLO's album art and branding
- Disco sparkle dots in red + white (references the actual disco balls from their Tiny Desk setup)
- Red italic `Access All Areas` subtitle in hero
- Red-filled play buttons throughout

### Typography

| Role | Font | Weights |
|---|---|---|
| Headlines / logotypes | Playfair Display | 400 Italic, 700 Bold, 900 Black |
| Body / UI / labels | Inter | 300 Light, 400 Regular, 500 Medium, 600 SemiBold, 700 Bold |

### Layout

- Max content width: **1100px**, centered
- Section padding: **100px vertical**, **32px horizontal**
- Alternating section backgrounds: `--black` / `--off-black`
- All borders use `--border` (white at 10%) or `--border-strong` (white at 18%)
- Gap between bordered grid cells: 1px (background of grid container acts as divider)

---

## Responsive Breakpoints

| Breakpoint | Behaviour |
|---|---|
| `> 900px` | Full 3-col Vevo grid, all 2-col layouts |
| `≤ 900px` | Vevo grid collapses to 2-col |
| `≤ 768px` | All grids go 1-col; track badges hidden; Vevo featured card stacks; about hero stacks; footer centers |

---

## Open Questions / v1 Decisions

| # | Question | Status |
|---|---|---|
| 1 | **Audio file hosting** — Static assets in repo, CDN, or object storage? GitHub Pages has a 1GB soft limit; individual track files may approach 30–50MB each. | ⏳ Open |
| 2 | **NPR Tiny Desk YouTube ID** — Needed to replace the video placeholder with a real `<iframe>` embed. | ⏳ Open |
| 3 | **Concert photos** — One image per show would significantly strengthen the about page concerts section. | ⏳ Open |
| 4 | **About page copy** — Concert memory text, song notes, and "why I built this" are placeholder. Needs Tise's voice. | ⏳ Open |
| 5 | **Domain / hosting** — GitHub Pages (free), Vercel (free tier), or custom domain? | ⏳ Open |
| 6 | **Analytics** — Goatcounter (privacy-first, free) recommended. No cookies, no GDPR banner needed. | ⏳ Open |
| 7 | **OG/meta tags** — `og:title`, `og:description`, `og:image` for social sharing previews. Needed before any public launch. | ⏳ Open |

---

## Resolved Since v0.1

| Item | Resolution |
|---|---|
| Vevo video URLs | ✅ All 7 confirmed with YouTube IDs |
| Vevo thumbnails | ✅ Using YouTube CDN (`img.youtube.com`) — no hosting needed |
| Design system | ✅ Gold removed; full red/black/white rebrand to match NPR + FLO |
| Section order | ✅ Set → Watch → Vevo → Girls (fan tribute removed) |
| About page | ✅ Built with concerts, songs, origin story, connect section |
| Navigation | ✅ Fixed nav across both pages |

---

## File Index

| File | Description |
|---|---|
| `flo-tiny-desk.html` | Main concert page — hero, setlist, video, Vevo, The Girls |
| `about.html` | Creator page — Tise's concerts, faves, origin story, links |

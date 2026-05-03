# PRD: FLO Y2K Fan Shrine

**Version:** 0.2 (Post-FLO Rebrand)
**Date:** April 2026
**Author:** Tise (tisebuilds.com · @tisebuilds)

---

## Overview

A single-page Y2K fan shrine celebrating FLO's February 20, 2026 NPR Tiny Desk Concert. It reads like a GeoCities page a superfan built at 2am after watching the set — Comic Sans, marquees, blinking text, an autoplay popup, a sparkle cursor trail, a hit counter, a broken guestbook. Early-2000s chaos energy, intact.

What separates this from a generic Y2K pastiche: the palette and chrome have been rebranded away from rainbow neon into **FLO's red / cream / black / glossy-pink visual language**. The background is a sticker-collage on deep editorial red instead of stars on black. A new collage hero section under the header layers a polaroid, a spinning CD, sticker text, and a magazine editorial block — scrapbook meets R&B girl-group press kit.

This is the **fan-expression** companion to the editorial micro-site (`flo-tiny-desk.html`). Same Tiny Desk, opposite tone.

---

## Goals

- Evoke authentic late-90s / early-2000s fansite energy (chaotic, personal, clearly homemade)
- Reskin that aesthetic to FLO's visual identity — glossy red editorial + scrapbook collage
- Celebrate and archive the full 8-song Tiny Desk setlist
- Surface FLO's Vevo live catalogue (7 videos) for discovery
- Keep every signature Y2K interaction: sparkle cursor, autoplay popup, hover chord audio, spinning disc, hit counter, guestbook teaser, marquees
- Make someone smile hard enough to share the link

---

## Non-Goals

- Not the editorial archive — that's the job of `flo-tiny-desk.html`
- No real user accounts, backend, or persisted guestbook
- No real music playback of FLO's catalogue — audio is Web Audio chord stabs only
- Not pixel-perfect responsive — embraces "best viewed in 800×600" energy with only minimal mobile fallbacks
- Not accessibility-perfect — the genre is inherently chaotic (but cursor trail is throttled and popup is keyboard-dismissable)
- No build step, bundler, or framework

---

## Tech Stack

- Single static HTML file (`public/index.html`) — inline `<style>` + inline `<script>`
- Google Fonts: **VT323** (terminal), **Permanent Marker** (handwritten), **Press Start 2P** (8-bit)
- System `Comic Sans MS` as body fallback (mandatory for the genre)
- Vanilla JS — Web Audio API (square + sawtooth oscillators), Clipboard API, fake hit counter
- **Zero images** — everything rendered via CSS gradients, emoji, and SVG data URIs
- Sticker-collage body background is an inline-encoded SVG `<text>` pattern
- Fully static — deployable to GitHub Pages, Vercel, or Netlify with no build step

---

## Site Map

```
public/index.html    ← single-page fan shrine
```

One scrolling page. No nav. No routing. Scroll is the only navigation.

---

## Page Structure

Sections, top to bottom:

### 0. Autoplay Popup *(Windows 98 overlay)*
**Purpose:** Nostalgic first-touch gate. Also the user-gesture needed to init `AudioContext`.

**Content:**
- Title bar: `⚠️ FLO Fan Site Alert!` with `✕` close button
- Body copy: *"This page contains AUTOPLAY SOUNDS!! You are about to enter the #1 FLO Tiny Desk Fan Page on the internet!!"*
- Disclaimer: *"(This page is best viewed in 800×600 resolution lol)"*
- Buttons: `OK ✓` (bold) and `Cancel`

**Behaviour:** Any close action (OK / Cancel / ✕) dismisses the overlay **and** calls `initAudio()` → starts room-tone noise + plays opening chord.

---

### 1. Header
**Purpose:** Announce the fan page. Glossy editorial introduction.

**Content:**
- `UNDER CONSTRUCTION · UPDATED FEB 2026` strip (Press Start 2P, with two spinning ⚙ icons)
- Stars divider row: `✦ ★ ✦ ★ ✦ ★ ✦ ★`
- Main title: `💖 FLO 💖` (Permanent Marker, ~5rem, cream on glossy red with layered pink → wine → black drop-shadows)
- Subtitle: `~~*~~ TINY DESK CONCERT ~~*~~` (rainbow class — animates through the FLO palette)
- Tagline: `February 20, 2026 · Washington D.C. · NPR Music` with blinking ★s
- Credit: `Official Unofficial Fan Page by Tise`

**Design notes:**
- Glossy red gradient background (`#1a0608 → #6b0a1c → #b8102e`) with subtle `bgShift` animation
- 4px cream border + 2px wine outline + 8px wine stacked drop-shadow (feels like a printed magazine cover pinned to the page)
- Inset vignette on the bottom half for depth
- Subtle white ink-stripe via `::after` pseudo-element

---

### 2. Collage Hero *(new in v0.2)*
**Purpose:** Scrapbook / magazine-cutout section. Signals FLO's visual identity and the fan-shrine concept in one glance.

**Layout:** 3-col grid on desktop, 1-col stacked on mobile, inside a cream+pink paper panel with dashed red border, triple-layered shadow (cream → wine → black), and scotch-tape strips pinning the corners.

**Content:**
| Slot | Element |
|---|---|
| Left | **Polaroid** — white card, rotated -5°, red gradient photo area with `FLO` in Permanent Marker, caption: `stella · renée · jorja ♥` |
| Centre | **CD Disc** — 168×168 conic-gradient disc (pink → red → wine → cream), animated spin 9s, glossy inner ring highlight |
| Right | **Magazine Block** — cream paper, rotated +2°, red+black stacked shadow. Kicker: `▸ ISSUE 08 · SPRING 2026`. Headline: `R&B'S IT-GIRL TRIO, RELOADED` (Permanent Marker, wine). Serif body copy. |

**Sticker overlays** (absolutely positioned, rotated, drop-shadowed):
- Top-left: red-bright sticker `★ FLO 4 LIFE ★` (rotated -12°)
- Top-right: pink pill `I ♥ FLO` (rotated +8°, dashed wine border)
- Bottom-right: giant 💋 (rotated -18°)
- Bottom-left: pixel tag `♫ CD INSERT ♫` (rotated -4°)

**Design notes:**
- No interaction — purely visual. The polaroid has a hover tilt/scale for charm.
- This section is the brand anchor. Everything else on the page reads as Y2K chaos; this is the beat that says "this is about FLO, specifically."

---

### 3. Top Marquee
**Purpose:** Chaotic energy strip. Classic scrolling ticker.

**Content (looping):**
*"💖 WELCOME TO MY FLO FAN PAGE 💖 ★ TINY DESK WAS EVERYTHING ★ 💖 STELLA RENÉE JORJA I LOVE U ★ CARDBOARD BOX MADE ME CRY ★ 💖 THERAPY AT THE CLUB WORLD PREMIERE!!! ★ FLO SERVED AND LEFT 💖"*

**Design notes:**
- Glossy pink band, cream text with wine text-shadow
- CSS `translateX` keyframe (18s loop)
- Top + bottom 3px cream borders

---

### 4. Now Playing Bar
**Purpose:** Winamp-style indicator tied to setlist clicks.

**Content:**
- Spinning CD disc (conic-gradient: pink → wine → cream → pink, 3s rotate)
- `▶ NOW PLAYING:` blinking label (Press Start 2P, cream)
- Track title (updates on setlist row click)
- Rainbow-animated `♪` on the right

**Behaviour:** Clicking any setlist row updates this bar's title text.

---

### 5. The Set *(8-song setlist table)*
**Purpose:** Tracklist + hover audio. Core interactive section.

**Container:** `box--pink` with `💿 THE SET — ALL 8 SONGS!!! 💿` header.

**Setlist:**

| # | Track | Source | Badge |
|---|---|---|---|
| 01 | Cardboard Box | Debut Single · Reimagined | Single |
| 02 | AAA | Access All Areas, 2024 | Album |
| 03 | On & On | Access All Areas, 2024 | Album |
| 04 | Get It Till I'm Gone | Access All Areas, 2024 | Album |
| 05 | Shoulda Woulda Coulda | Access All Areas, 2024 | Album |
| 06 | Immature | The Lead EP, 2022 | Fav 💛 |
| 07 | Therapy at the Club | UNRELEASED!! World Premiere!! | NEW!!! (blinking) |
| 08 | HaterBooth | UNRELEASED!! Closing Track!! | NEW!!! (blinking) |

**Behaviour:**
- `mouseenter` on row → plays chord[row.dataset.chord] via square+sawtooth oscillators
- `click` on row → updates Now Playing title, plays chord at higher gain, spawns 6 sparkle emoji burst at the row's position
- Rows have `data-chord` (0–7) and `data-title` attributes

---

### 6. Watch The Set *(CRT TV module)*
**Purpose:** Drive traffic to the real NPR video.

**Container:** `box--yellow` reskinned with orange border + orange glow (kept from original spec — reads as vintage TV bezel).

**Layout:** 2-col — fake CRT TV (left) + copy + CTAs (right).

**CRT TV component:**
- Two mini antennae (3px × 22px bars, rotated ±20°)
- 6px dark-grey bezel, 6px→12px rounded border-radius (CRT curve)
- Big ghost `FLO` text inside (VT323, low-opacity orange)
- Red CRT glow + scanline pattern via `::before` + `::after`
- Orange play-pulse button (animation: `playPulse` 1.5s) → links to NPR
- Bottom-centre label: `📡 LIVE ON NPR 📡`

**Copy:** Fan-voice paragraphs about the set (disco balls, martinis, Therapy at the Club, HaterBooth).

**CTAs:**
- Primary: `▶ WATCH ON NPR NOW!! ◀` (blinking, links to NPR set URL)
- Secondary: `✦ More Tiny Desk Concerts ✦` (dashed cream outline, cyan → cream in the remapped palette)

---

### 7. Share Strip
**Purpose:** Frictionless sharing. Deliberately inline, not a full section.

**Content:**
- `📢 TELL UR FRIENDS!!` label (Press Start 2P, cream)
- `🐦 TWEET THIS!!` — pre-filled tweet with NPR URL
- `📋 COPY LINK!!` — Clipboard API → `✅ COPIED!!` flashes (blink animation, 4 pulses)

**Design notes:** Dashed cream border, translucent cream background — reads as a torn magazine strip.

---

### 8. Bottom Marquee
**Purpose:** Pair for the top marquee. Different content, different direction of energy.

**Content:** *"🎤 STELLA QUARESMA 🎤 RENÉE DOWNER 🎤 JORJA DOUGLAS 🎤 THE HOLY TRINITY 🎤 FLO IS EVERYTHING 🎤 ACCESS ALL AREAS 🎤 SOUTH LONDON REPRESENT 🎤 TINY DESK 2026 🎤"*

**Design notes:** Wine background (was electric blue in v0.1), cream text. 28s loop — slower than the top marquee.

---

### 9. The Girls *(member cards)*
**Purpose:** Brief artist context. Matches the Tiny Desk PRD's member block but with hover-to-play sound.

**Container:** `box--yellow` (cream header in the FLO palette) with `👑 THE GIRLS 👑` header.

**Cards (3-col grid):**

| Avatar | Name | Role |
|---|---|---|
| 🌟 | Stella | Quaresma ✦ Vocals |
| 💎 | Renée | Downer ✦ Vocals |
| 🔥 | Jorja | Douglas ✦ Vocals |

**Behaviour:**
- `mouseenter` on card → plays member's chord + a `playBloop()` (sine 880→440Hz sweep)
- Hover transform: scale(1.04) rotate(-1°)
- Floating avatar animation (`floatBob` 2s)

**Caption below:** *"(hover them!! they make sounds!!)"*

---

### 10. Two-Column: Discography + About/Stats/Guestbook

**Left column — Discography** (`box--purple` → remapped to deep wine)
- **The Lead EP** (2022, 5 tracks) — avatar 🎵, track list with `♥` bullets
- **Access All Areas** (2024, 11 tracks) — avatar 🌹 on red gradient tile

**Right column — stacked:**

**About This Page** (`box--cyan` → cream-soft)
- First-person fan origin story: saw Cardboard Box on FYP in 2022, cried, seen FLO 3× NYC (Webster Hall 2023, Gov Ball 2024, Brooklyn Paramount 2025)
- Links out to `tisebuilds.com ↗` and `@tisebuilds ↗`

**Stats / Hit Counter** (`box--lime` → cream)
- Fake 6-digit VT323 visitor count (seeded ~3847, increments every 4–10s)
- Rainbow-animated "You are visitor #N!!" below

**Guestbook Teaser**
- Dashed wine border box
- `💌 Sign my guestbook!! Tell me your fav FLO song!! 💌`
- Button → `alert('Guestbook coming SOON!! Check back!! 🌟')`

---

### 11. FLO on Vevo *(live video grid)*
**Purpose:** Surface FLO's full Vevo live canon.

**Container:** `box--blue` → remapped to wine.

**Grid layout:** 2-col × 3 rows + a full-width acoustic feature card.

| Song | Series | Year | YouTube ID |
|---|---|---|---|
| Check | Live from Vevo Studios | 2024 | `QJR77KB1wq4` |
| Bending My Rules | Live from Vevo Studios | 2024 | `XBnJ3mLQJ5w` |
| Feature Me | Vevo DSCVR | 2022 | `Laz2udZieRM` |
| Not My Job | Vevo DSCVR | 2022 | `B7xmqFBuK9k` |
| Immature | Vevo DSCVR | 2022 | `4yC_2n9VIVY` |
| Cardboard Box | Vevo DSCVR | 2022 | `pCOyYgvEfTk` |
| Cardboard Box (Acoustic) | Live Acoustic — full-width | — | `pfTbj43Dkjc` |

**Behaviour:**
- `mouseenter` on any vevo card → plays that card's chord
- Click opens YouTube in new tab

**Footer link:** Full playlist CTA — `🎬 VIEW THE FULL FLO VEVO PLAYLIST ON YOUTUBE ↗ (all 7 videos!!)` linking to the playlist URL.

---

### 12. Footer
**Content:**
- Blinking ★, credit line, link to tisebuilds.com, link to NPR set page
- Disclaimer: *"Not affiliated with NPR or FLO management · Fan tribute only"*
- 88×31 badge row: `Best Viewed · Chrome` / `💖 FLO FAN` / `Made w/ ❤` / `2026 ©`

---

### Persistent: Audio Status Indicator
**Purpose:** Feedback that `AudioContext` is initialised.

**Content:** Fixed top-right chip, `♪ AUDIO ON ♪` (VT323, cream, wine border). Fades in on popup close, fades out after 3s.

---

## Design System

### Color Tokens *(v0.2 — FLO palette)*

| Token | Value | Usage |
|---|---|---|
| `--flo-red` | `#b8102e` | Glossy lipstick red — primary accent |
| `--flo-red-dark` | `#6b0a1c` | Deep wine / burgundy — shadows, wine backgrounds |
| `--flo-red-bright` | `#e5143a` | High-gloss red — title shadows, stickers |
| `--flo-cream` | `#f0e4c8` | Magazine paper — primary text on dark, light backgrounds |
| `--flo-cream-soft` | `#e8dcb8` | Softer cream accent |
| `--flo-pink` | `#ff9ec7` | Glossy bubblegum — accent stickers, marquee |
| `--flo-pink-soft` | `#ffcce0` | Pink wash tints |
| `--flo-black` | `#0d0608` | Near-black with red undertone — body base |
| `--flo-gold` | `#c9a96a` | Warm gold accent (optional, reserved) |

### Legacy Y2K Aliases *(remapped, not deleted)*

The original v0.1 palette variables (`--hot-pink`, `--electric-blue`, `--lime`, `--yellow`, `--purple`, `--cyan`, `--orange`, `--red`, `--dark`) are **preserved as CSS custom properties** but remapped to FLO tones. This lets every existing selector and inline style cascade into the new look without rewriting every rule.

| Legacy | Now maps to | Effect |
|---|---|---|
| `--hot-pink` | `--flo-pink` | Neon magenta → glossy bubblegum |
| `--electric-blue` | `--flo-red-dark` | Electric blue → wine |
| `--lime` / `--yellow` / `--cyan` | `--flo-cream` / `--flo-cream-soft` | Bright neons → magazine cream |
| `--purple` | `--flo-red-dark` | Neon purple → wine |
| `--orange` | `--flo-red` | Blaze orange → glossy red |
| `--red` | `--flo-red-bright` | Flat red → glossy lipstick |
| `--dark` | `--flo-black` | `#110011` → `#0d0608` |

> **No rainbow.** The previous v0.1 palette ran full hot-pink/cyan/lime rainbow. This version removes all bright greens/cyans except as cream substitutes; the only multi-hue moment is the `.rainbow` keyframe on the subtitle, now looping through the FLO palette.

### Brand References

**FLO (Access All Areas era):**
- Primary red `#b8102e` matches FLO's album art and press kit
- Cream + glossy pink as the scrapbook counterpoint (CD inserts, polaroid)
- Permanent Marker for title evokes fan-made mixtape / magazine cover
- Spinning CD in collage hero references FLO's disc-heavy visual campaign

**Y2K GeoCities / fansite:**
- Comic Sans MS body, Press Start 2P section headers, VT323 terminal moments
- Marquees top and bottom
- `UNDER CONSTRUCTION ⚙` strip
- Hit counter with 6-digit padding
- Guestbook teaser
- 88×31 link badges
- Windows 98 autoplay popup
- Blink animations
- Sparkle cursor trail
- Chorded hover sounds (square + saw waves — period-authentic tone)

### Typography

| Role | Font | Usage |
|---|---|---|
| Headlines & handwritten labels | **Permanent Marker** | Main title, member names, polaroid caption, magazine headline, album names |
| Terminal / digital | **VT323** | Hit counter, now-playing label, audio status |
| 8-bit / pixel | **Press Start 2P** | Box headers, badges, marquee labels, CD-tag sticker |
| Body | `Comic Sans MS`, `Comic Sans`, cursive | All body copy |
| Magazine body | `Georgia`, `Times New Roman`, serif | Only inside the `.mag-block` editorial card |

### Textures & Chrome

- **Body background** — deep `#0d0608 → #3a0612 → #6b0a1c` linear gradient, overlaid with four radial "paper-tear" highlight clouds (red and pink) and an inline-SVG sticker pattern of ♥ ♡ ● ✦ in cream + pink at 8–11% opacity, tiled at 260×260
- **Header** — glossy red gradient with `bgShift` 8s animation, 4px cream border, 2px wine outline, 8px wine stacked shadow, 24px red outer glow, inset dark vignette on the bottom half
- **Boxes** — 3px coloured border, `rgba(13,6,8,0.9)` fill with a 14%-height top highlight strip, 4px wine stacked drop-shadow (collage paper feel)
- **Collage hero panel** — cream + pink paper (`linear-gradient(120deg, #f0e4c8, #f7ecd4, #ffd7e5)`) with pink-wash + red-wash radial highlights, dashed red border, **triple-layered shadow**: cream halo → wine outline → black drop — feels like a 3-deep layered collage
- **Cursor** — SVG data URI `♥` (replaced the original `⭐`)

### Sparkle Cursor System

- On every ~30% of `mousemove` events, spawn a `.sparkle` div at the cursor position with a random emoji from: `['♥','♡','💖','💋','💿','🌹','💄','✦','★','♫','💅']`
- Colour is picked from `SPARKLE_COLORS = ['#b8102e','#e5143a','#ff9ec7','#ffcce0','#f0e4c8','#6b0a1c']` — **not** random HSL rainbow (deliberate change from v0.1)
- Element animates via `sparkFade` 0.8s (opacity 1 → 0, translateY -50% → -120%, scale 1 → 0, rotate 45°) then self-removes

### Audio System

`AudioContext` is created inside `initAudio()`, which fires when the popup is dismissed. On init:
- A 2-second stereo noise buffer at 0.004 amplitude is looped through a 0.06-gain node → room tone
- Opening chord `playChord(5)` plays

**Chord progressions** — 8 × 4-note voicings stored in `CHORDS`, indexed 0–7. Each voicing plays the first 3 notes as a mix of square (lead) + sawtooth (harmony) oscillators with staggered 30ms attacks and a 1.8s exponential decay.

**Triggers:**
- Setlist row hover → `playChord(row.dataset.chord, 0.04)`
- Setlist row click → `playChord(..., 0.06)` + sparkle burst + Now Playing title update
- Member card hover → `playChord(...)` + `playBloop()` (sine 880→440Hz sweep, 200ms)
- Vevo item hover → `playChord(..., 0.04)`

---

## Responsive Breakpoints

| Breakpoint | Behaviour |
|---|---|
| `> 600px` | Full 3-col collage grid, 2-col watch layout, 2-col vevo/about, 3-col member cards |
| `≤ 600px` | Collage grid stacks to 1-col (polaroid → CD → magazine); watch layout stacks; two-col sections collapse to 1-col; vevo grid collapses to 1-col; polaroid max 200px; magazine block rotation softened; site-wrapper padding reduces to 4px; sticker positions shift to avoid overlapping the stacked content |

Below 600px, the page still proudly reads "best viewed in 800×600". This is a feature.

---

## Open Questions / v1 Decisions

| # | Question | Status |
|---|---|---|
| 1 | **Real FLO audio** — Should setlist rows trigger actual FLO snippets instead of synthesised chords? Hosting + licensing implications. | ⏳ Open |
| 2 | **Guestbook** — Hook up Formspree / Netlify Forms / Supabase to make the guestbook actually work? Or keep it as a fake shrine relic? | ⏳ Open |
| 3 | **Real polaroid image** — Swap the Permanent-Marker `FLO` text polaroid for a licensed/press photo? | ⏳ Open |
| 4 | **Link to the editorial companion site** (`flo-tiny-desk.html`) — Add a small `"serious version ↗"` footer link? Or keep the two sites completely siloed in tone? | ⏳ Open |
| 5 | **Sparkle cursor on touch devices** — Currently fires on scroll taps. Disable when `pointer: coarse`? | ⏳ Open |
| 6 | **Autoplay popup on repeat visits** — `localStorage` flag to skip after first dismissal? Contradicts the "every visit is chaos" ethos. | ⏳ Open |
| 7 | **Domain / hosting** — GitHub Pages (free) or a custom domain like `flo4life.tisebuilds.com`? | ⏳ Open |
| 8 | **OG / meta tags** — Need `og:title`, `og:description`, and a bespoke `og:image` (ideally a cropped version of the collage hero) before public launch. | ⏳ Open |
| 9 | **Mobile experience** — Worth investing in beyond current 1-col fallback? Or lean into "not optimised for mobile" as a genre choice? | ⏳ Open |
| 10 | **MIDI export / downloadable ringtone** — The 8 synthesised chords could be downloadable `.mid` or `.wav` ringtones. Y2K-native bonus. | 🔮 Nice-to-have |

---

## Resolved Since v0.1

| Item | Resolution |
|---|---|
| Generic rainbow neon palette | ✅ Rebranded to FLO red / black / cream / glossy pink; legacy tokens remapped |
| Space / starry background | ✅ Replaced with cream/pink SVG sticker collage on editorial wine gradient |
| Star `⭐` cursor | ✅ Swapped to `♥` cursor |
| Rainbow HSL sparkle colours | ✅ Locked to FLO palette via `SPARKLE_COLORS` |
| Sparkle emoji set (`★ ✦ ⭐ 💖`) | ✅ Expanded to FLO-world: `♥ ♡ 💖 💋 💿 🌹 💄 ✦ ★ ♫ 💅` |
| Header treatment | ✅ Glossy red gradient, cream border, wine outline + 8px stacked shadow, 24px red glow, inset vignette |
| Box chrome | ✅ Dark red-tinted fill (was dark-blue-tinted), top highlight strip, 4px wine drop-shadow |
| Collage hero | ✅ New v0.2 section — polaroid + spinning CD + stickers + magazine block + scotch-tape corners |
| Title text-shadow | ✅ Pink → wine → black stack (was hot-pink → purple → yellow glow) |

---

## File Index

| File | Description |
|---|---|
| `public/index.html` | The fan shrine — single-page, inline CSS + JS, zero dependencies |
| `flo-tiny-desk.html` | *(sibling — editorial companion micro-site, see `flo-tiny-desk-PRD.md`)* |

---

## Tone North-Star

> *A superfan made this after watching FLO's Tiny Desk and couldn't get over it.*

If a given styling decision, interaction, or copy line makes that sentence feel more true, it ships. If it makes it feel less true — even if it's "cleaner" or "more accessible" — it doesn't.

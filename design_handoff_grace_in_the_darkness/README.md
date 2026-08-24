# Handoff: Grace in the Darkness — event landing page

## Overview
A single-page landing site for **Grace in the Darkness: A Five-Part Journey from Trauma to Hope** with Cheri Peters — a free community event running in three New Zealand cities in October–November 2026. The page's primary job is to get a visitor to the right city's registration form (Google Forms). Registration is optional; admission is free and no booking is required.

Target deployment: **GitHub Pages** — a static site, no build step required.

## About the design files
The files in this bundle are **design references created in HTML** — a prototype showing intended look and content, not production code to copy verbatim.

`Grace in the Darkness.dc.html` is authored in a proprietary streaming-component format and **will not run standalone**. Do not try to deploy or import it. Read it as the source of truth for markup structure, copy, and inline style values, then recreate it as a plain static site:

```
index.html
styles.css
assets/cheri.jpg
```

No framework, bundler, or JS is needed — the page is static content plus one YouTube iframe and anchor-link scrolling. If the repo already has a static-site toolchain (Astro, Eleventy, Jekyll), use it; otherwise hand-written HTML + CSS is the right choice. Move the inline styles into `styles.css` as classes; keep the computed values identical.

### GitHub Pages notes
- Put `index.html` at the repo root (or in `/docs`) and enable Pages on that branch/folder.
- Asset paths must be relative (`assets/cheri.jpg`), not absolute (`/assets/...`), so it works from a project subpath like `username.github.io/repo/`.
- Add `<title>Grace in the Darkness — Cheri Peters | Free community event</title>`, a meta description, and Open Graph tags (`og:title`, `og:description`, `og:image` using the poster square) — the current prototype has none and this page will be shared on Facebook.
- Add `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- Set `lang="en-NZ"`.

## Fidelity
**High fidelity.** Colors, typography, spacing, and copy are final. Recreate pixel-faithfully. Where a value below and the prototype disagree, the prototype file wins.

## Design tokens

Palette (drawn from the event flyers — deep teal-green and gold on cream):

| Name | Hex | Use |
| --- | --- | --- |
| paper | `#F5EBD8` | Default page background, text on dark |
| ink | `#12333B` | Primary text on paper; dark buttons |
| ink-deep | `#0E2A31` | Dark section backgrounds (programme, video plate, footer) |
| gold | `#E0A020` | Accent: eyebrow text, dates, links, CTA band background |
| gold-soft | `#F0BC55` | Accent text and labels on dark backgrounds |
| gold-deep | `#B87F13` | Link/button hover |

Derived alphas used for secondary text and hairlines:
`rgba(18,51,59,0.86)` body on paper · `0.78` softer · `0.55` muted/labels · `0.25` hairline borders · `0.22` section dividers · `0.06` placeholder fill.
On dark: `rgba(245,235,216,0.82)` body · `0.78` · `0.72` · `0.6` · `0.55` · `0.25` hairlines.

Type — two families only, both Google Fonts:
- **Source Serif 4** (300–700, italic axis used) — display, headings, body, italic captions, pull quote.
- **JetBrains Mono** (400/500) — all uppercase chrome: eyebrows, dates, times, buttons, labels, footer headings. Always `text-transform: uppercase` with `letter-spacing: 0.14em`–`0.16em` at 10–13px.

No third typeface. No sans-serif. Never Title Case headings — sentence case for headings, ALL-CAPS only for the mono chrome.

Type scale (fluid):
- h1: `clamp(46px, 7.2vw, 104px)`, weight 600, line-height 0.94, letter-spacing -0.02em
- hero subtitle: `clamp(20px, 2.2vw, 28px)` italic
- speaker name: `clamp(30px, 3.6vw, 46px)` weight 500
- section h2: `clamp(26px, 3vw, 40px)`–`clamp(28px, 3.4vw, 44px)` weight 500
- card h3 (cities/books): 24–30px weight 500
- body: 15–18px, line-height 1.55–1.65
- mono chrome: 10–13px

Spacing / layout:
- Section padding: `clamp(32px, 5vw, 80px)` vertical, `clamp(20px, 5vw, 72px)` horizontal.
- Long-form copy capped at 58–65ch.
- **Sharp corners everywhere** — `border-radius: 0`. No rounded cards.
- **No shadows.** Surfaces separate by 1px hairline borders and by treatment shift (light-on-cream vs. gold-on-teal).
- Two treatments only: *lit* (ink on paper) and *inverted* (paper/gold on deep teal). Cards alternate deliberately: Mount = lit, Hamilton = inverted, North Harbour = lit.
- Plate framing: dark figure blocks carry an 8px right-edge bar in gold, plus four `+` registration marks in mono 10px at the corners, ~8px/10px inset.

## Page structure

Single scrolling page, sections top to bottom:

### 1. Masthead bar
Full-width, 14px vertical padding, 1px bottom hairline. Three mono uppercase 11px items, `justify-content: space-between`: "Grace in the Darkness" · "Free Community Event" (gold) · "Oct–Nov.2026 · Aotearoa NZ".

### 2. Hero
Two-column grid, `repeat(auto-fit, minmax(300px, 1fr))`, gap `clamp(28px, 4vw, 64px)`. Collapses to one column on phones.

Left column (flex column, 26px gap):
- Eyebrow: "Healing · Hope · Freedom" in gold mono caps, followed by a flexible 1px gold rule.
- `<h1>`: "Grace in the **Darkness**" — the word *Darkness* in italic gold.
- Italic lede: "A five-part journey from trauma to hope", max 22ch.
- Block above a 1px top hairline: mono "with" label, then "Cheri Peters" at display size, then "International Speaker · Author · Host of *Celebrating Life in Recovery*" (series title italic).
- Pull quote with 2px gold left border, 20px left padding, italic: "You are not what happened to you—your story is still being written."
- Two buttons in a wrapping flex row, 12px gap, both mono caps 12px, 15px/30px padding, sharp corners:
  - Primary → `#12333B` fill, paper text, href `#cities`, label "Register your interest". Hover `#0E2A31`.
  - Secondary → 1px `rgba(18,51,59,0.4)` border, ink text, href `#programme`, label "See the five sessions". Hover border and text go gold-deep.
- Muted mono line: "Free admission · No bookings required · Registration optional".

Right column — portrait plate:
`#0E2A31` fill, padding 26px (34px right to clear the bar), min-height 420px, position relative. Contains: 8px full-height gold right-edge bar; four gold `+` ticks at the corners; the portrait `assets/cheri.jpg` filling the remaining height (`object-fit: cover; object-position: 50% 22%; filter: saturate(0.92)`); and a centered gold-soft mono caption "As seen on TV · Hope Channel · Firstlight · 3ABN".

### 3. Cities (`id="cities"`) — the primary CTA section
Heading row: h2 "Three cities, one journey", a flexible hairline, and a muted mono tag "Register · Optional".

Three cards, `repeat(auto-fit, minmax(280px, 1fr))`, 20px gap. Each card is a flex column (18px gap), padding 24px with 34px on the right, and carries an 8px full-height right-edge bar. Contents in order: gold mono date range (13px, 0.1em tracking) → city name h3 30px → venue address block (16px, line-height 1.55) → mono contact block (11px) → register button pinned to the bottom with `margin-top: auto`, full-width, centered mono caps 11px, 14px/22px padding.

| Card | Treatment | Date | Venue | Contact | Button |
| --- | --- | --- | --- | --- | --- |
| Mount Maunganui | lit: `#F5EBD8` fill, 1px `rgba(18,51,59,0.25)` border, ink right-bar | 28–31 OCTOBER 2026 | St Andrews Presbyterian Church / Cnr Macville Road and Dee Street / Mount Maunganui 3116 | 020 4111 5110 / cheri-peters-mtsda@googlegroups.com | ink fill, paper text |
| Hamilton | inverted: `#0E2A31` fill, paper text, gold right-bar | 4–7 NOVEMBER 2026 | Venue to be confirmed / Street address to be confirmed / Hamilton | Phone to be confirmed / Email to be confirmed | gold fill, `#0E2A31` text |
| North Harbour | lit | 11–14 NOVEMBER 2026 | Venue to be confirmed / Street address to be confirmed / North Harbour, Auckland | Phone to be confirmed / Email to be confirmed | ink fill, paper text |

Registration links (open in a new tab, `rel="noopener"`):
- Mount Maunganui — `https://docs.google.com/forms/d/e/1FAIpQLSexdgAQRRcQHb9TrcAooWmN6rJJpuRYI_dZz_Y-_RaXruJ-pQ/viewform`
- Hamilton — `https://docs.google.com/forms/d/e/1FAIpQLSckywdBOEpSE9KdX68pFP5EzN5wghj5KhZDKJYsPw2J0TaTBA/viewform`
- North Harbour — `https://docs.google.com/forms/d/e/1FAIpQLSd7eWW1HkgBjl3I88715-DJ5gXL0411yozE_PZWFvSA_rO0qw/viewform`

Closing note under the cards, muted, max 60ch: "Admission is free and no booking is required. Registering simply helps the host church plan seating, catering and the children's programme."

### 4. Programme (`id="programme"`)
Inverted section: `#0E2A31` background, paper text.

Header row: gold-soft mono "The Programme", flexible hairline, muted mono "Same in all three cities". Then h2 "Five sessions · one transformative journey" (max 26ch).

Five rows, each `display: flex; flex-wrap: wrap; gap: 24px; padding: 26px 0` with a 1px top hairline (last row also has a bottom hairline). Three items per row:
1. `width: 130px` — gold-soft mono caps: "Session N" / weekday.
2. `width: 150px` — muted mono: time / "Doors 6.30 pm".
3. `flex: 1 1 280px` — h3 24px session title + description paragraph 17px, max 58ch.

| # | Day | Time | Title | Description |
| --- | --- | --- | --- | --- |
| 1 | Wednesday | 7.00 – 9.00 pm, doors 6.30 | From the Pit to the Path | A powerful story of trauma and homelessness, revealing how God meets us in our darkest moments and restores home. |
| 2 | Thursday | 7.00 – 9.00 pm, doors 6.30 | Understanding Trauma | A compassionate look at how trauma impacts the mind, body and emotions—and why your responses make sense. |
| 3 | Friday | 7.00 – 9.00 pm, doors 6.30 | Bound by Love or Fear? | Explore people-pleasing and relational patterns, and learn how to build healthy, God-honouring boundaries. |
| 4 | Saturday | 10.45 am – 12.30 pm | Rebuilding | Discover how healing unfolds over time and how to reclaim your identity through God's truth and grace. |
| 5 | Saturday | 7.00 – 9.00 pm, doors 6.30 | The Healing Conversation | A guided, safe space for reflection, sharing, and prayer—helping participants process and take their next step toward freedom. |

The programme is identical in all three cities, which is why sessions are labelled by weekday rather than date.

Below it, a five-cell fact strip: `repeat(auto-fit, minmax(200px, 1fr))` with `gap: 1px` over a `rgba(245,235,216,0.25)` background so the gaps read as hairlines; each cell `#0E2A31`, 20px/18px padding, mono caps 11px — gold-soft label on line one, paper value on line two:
Doors open / 6:30 pm · Free admission / No bookings required · All are welcome / Come as you are · Children's programme / Provided each session · Please note / For mature audiences.

### 5. About the speaker
Two columns, `repeat(auto-fit, minmax(320px, 1fr))`, gap `clamp(28px, 4vw, 56px)`, items top-aligned.

Left: gold mono eyebrow "About the Speaker" → h2 "Cheri Peters" → bio paragraph 18px, max 60ch, `text-wrap: pretty` (series title italic): "Cheri Peters is an international speaker, author and trauma recovery advocate. Through her television ministry *Celebrating Life in Recovery*, featured on Hope Channel, Firstlight and 3ABN, she has helped thousands discover hope after trauma, abuse and loss. Her compassionate, faith-filled presentations combine biblical truth with practical insight into emotional healing." → three outlined mono chips: Hope Channel · Firstlight · 3ABN (1px hairline border, 7px/12px padding).

Right: video plate — `#0E2A31` fill, 24px padding (32px right), 8px gold right-edge bar, a 16:9 responsive iframe (`padding-top: 56.25%` wrapper, black behind), and an italic paper caption. Video: `https://www.youtube-nocookie.com/embed/sTytfNNXaGk`, caption "Cheri tells her own story — from the street to a life spent helping others recover."

### 6. Books
Gold mono eyebrow "Books" + hairline, then two cards, `repeat(auto-fit, minmax(300px, 1fr))`, 20px gap. Each card: 1px hairline border, 22px padding, `grid-template-columns: 120px 1fr`, 22px gap.
- Left cell: cover placeholder — `aspect-ratio: 2/3`, `rgba(18,51,59,0.06)` fill, 1px hairline, centered mono 9px caps "Cover image to come". **The client will supply cover images later; keep the slot the same size.**
- Right cell: h3 24px title, description 16px, and a gold mono caps link pinned bottom (`margin-top: auto`) reading "Adventist Book Center →" pointing at `https://adventistbookcenter.com/authors/cheri-peters`.

| Title | Description |
| --- | --- |
| Miracle From the Street | Cheri's own account of childhood trauma, homelessness and the long road out. |
| God Is Crazy About You | A plain-spoken book about being loved before you have anything sorted out. |

### 7. CTA band
Full-width gold `#E0A020` background with `#0E2A31` text, padding `clamp(40px, 5vw, 80px)` / `clamp(20px, 5vw, 72px)`, flex wrap, `space-between`, 28px gap.
Left (max 34ch): mono caps "Healing · Hope · Freedom" then h2 "Come as you are. Bring someone with you."
Right: button, `#0E2A31` fill, paper text, mono caps 12px, 17px/34px padding, href `#cities`, label "Choose your city". Hover `#12333B`.

### 8. Footer
`#0E2A31` background, `rgba(245,235,216,0.78)` text, `repeat(auto-fit, minmax(200px, 1fr))`, 28px gap, 15px/1.7 body. Five blocks, each a gold-soft mono 10px caps heading over plain lines:
1. Presented by — Mount Maunganui Seventh-day Adventist Church
2. Contact · Mount Maunganui — 020 4111 5110 / cheri-peters-mtsda@googlegroups.com (mailto link, gold-soft)
3. Contact · Hamilton — Phone to be confirmed / Email to be confirmed
4. Contact · North Harbour — Phone to be confirmed / Email to be confirmed
5. Grace in the Darkness — Oct–Nov 2026 · Free community event

## Interactions & behavior
- **Anchor scrolling only.** "Register your interest" and "Choose your city" → `#cities`; "See the five sessions" → `#programme`. Add `html { scroll-behavior: smooth; }` and `scroll-margin-top` on the anchored sections.
- **Registration** is three outbound links to Google Forms, `target="_blank" rel="noopener"`. No form handling, no backend, no analytics in the prototype.
- **Hover** = color shift only. No transforms, no scaling, no shadow. Buttons darken (`#12333B` → `#0E2A31`, gold → `#F0BC55`), text links go gold → gold-deep.
- **Focus**: give every link and button a visible focus ring — 2px solid gold-deep at 2px offset. The prototype relies on browser defaults; do better in production.
- **Responsive**: every grid uses `auto-fit`/`minmax` or `flex-wrap`, so the page collapses to a single column on phones with no media queries. Verify at 390px that the programme rows stack and nothing overflows horizontally.
- **No animation** anywhere. Keep it that way.

## State management
None. Fully static.

## Assets
- `assets/cheri.jpg` (1040×1680 JPEG) — portrait of Cheri Peters, cropped from the client's Instagram-square flyer. **Low-ish source quality; ask the client for the original photograph before launch.** Needs `alt="Cheri Peters"`.
- Book covers — not yet supplied; placeholders in the markup.
- Poster/flyer PDFs live in the project `uploads/` folder; useful for an `og:image` and for checking color against print.

## Content caveats to carry into the build
- Hamilton and North Harbour venues and contacts are genuinely unconfirmed. Keep the "to be confirmed" strings until the client sends details — do not invent addresses.
- Three typos from the print flyer were corrected in this copy: "boundries" → boundaries, "identiy" → identity, "darkness moments" → darkest moments.
- Event is billed for mature audiences with a separate children's programme; keep both notes visible.

## Files in this bundle
- `README.md` — this document.
- `Grace in the Darkness.dc.html` — the design prototype. Reference only; not deployable.
- `assets/cheri.jpg` — portrait used in the hero.
- `screenshots/` — visual reference captures of the prototype: `01` hero, `02` city cards, `03` programme, `04` CTA band and footer. Captured at a narrow viewport, so headings wrap earlier than they will on desktop; the video iframe appears blank because embeds aren't captured.

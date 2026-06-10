# Sign Painter's Companion — Project Handoff

A single-file web app for traditional sign painters: layout math plus a working
reference, drawn from real sources. Built to be used on a job (phone or desktop),
offline-capable, installable to a home screen.

**Live:** https://drtsuby.github.io/sign-layout
**Repo:** github.com/drtsuby/sign-layout (file served as `index.html`)
**Deliverable:** one self-contained `index.html` (~160 KB) — no build, no server,
no external dependencies except Google Fonts. Icon, manifest, and offline service
worker are embedded in the file.

_Last updated: added two Reference cards — "Letter Spacing — Optical" (John King)
and "Layout & Lettering" (Bond 1937) — plus a "Negative space" Sketcher check
(John King's message-block hierarchy). Source library found on the **W: drive**
(`W:/Sign_Painting/Sign painting books`, `/PDF`, `/Charts`). Kynaston
lowercase/italic is RESOLVED — the booklet has no numeric lowercase/italic table
(lowercase is derived by eye from the caps), so nothing to add. Additional books
still open._

---

## What it is

A practical companion, not a tutorial. It assumes the user knows the craft. Every
number and rule traces to a source (below); where the app uses a sensible default
rather than a sourced figure, it says so. Guiding principle: **trust the eye over
the math** — the tools give starting points, the painter decides. Measurements
display in **decimal** (a `frac()` function exists, unused; one-line flip to enable
fractions). **Value contrast is the most important factor; never trade legibility
for harmony.**

---

## Navigation (8 top tabs)

The nav uses a two-level sub-tab pattern. Two tabs are wrappers:

- **Margins**
- **Letters** <- wrapper, sub-tabs: **Widths / A-Z / Slope**
- **Sketch**
- **Ideas**
- **Shadow**
- **Contrast**
- **Colors**
- **Tools** <- wrapper, sub-tabs: **Rows / Scale / Reference / Kit**

### Sub-tab machinery (how it works)
- Each sub-section is `<section class="view subview grp-X ...">` with `data-sub="1"`,
  where `grp-X` is `grp-tools` or `grp-letters`.
- CSS: `.subview{display:none!important}`, then
  `body.tools-active .subview.grp-tools.on{display:block!important}` and the
  matching `letters-active`/`grp-letters` rule.
- JS: the top `nav` handler toggles `tools-active` / `letters-active` on `<body>`.
  `wireSubnav(navId, grpClass)` wires each sub-nav (`#subnav` -> grp-tools,
  `#subnavL` -> grp-letters) and only toggles `.on` within its own group.
- To add another grouped tab later: new body class + CSS rule + `wireSubnav` call,
  tag sub-sections with a new `grp-` class.

---

## Tab contents

**Margins** — sign WxH -> exterior margin (15% / 20% / eyeball), bottom bumped for
optical center, interior-margin ceiling, border-first reminder. Live sign preview.

**Letters > Widths** — width solver for six alphabets (Gothic, Phoenix, Roman,
Thick&Thin, Western, Casual). Enter stem -> normal/narrow/wide widths, M/W, bar
rule, and ICS 1902 spacing gaps scaled to the stem.

**Letters > A-Z** — per-letter spec sheet. **Six alphabets:** Class Gothic (course
chart, default), Full Block & Roman (Lester 1903 stroke tables), Egyptian & Half
Block (Matthews 1920), and **DK Roman (Kynaston 2024, 10-point system)**. Tap a
letter for width (strokes/points + inches at cap height) and construction notes.
**Style preview:** glyph rendered in a font resembling the style — Playfair Display
for Roman & DK Roman, Bitter (slab) for Egyptian, Oswald for sans styles. Labeled
"approximation." A **"Preview font" dropdown** lets you switch to any custom font
loaded from the `fonts/` folder (see Font workflow below).

**Letters > Slope** — slant/italic helper (Gage 1924). Enter slope-deg + cap height
-> top lean, lean-per-inch, rise:run, slant-line diagram.

**Sketch** — copy-block layout sketcher with rule checks (emphasis, size variation,
movement, phrase count, margin, **negative space** — perimeter margin must beat the
gaps between copy blocks, per John King's message-block hierarchy).

**Ideas** — practice-prompt generator. Storefront/Grocery toggle, Simple/Detailed.

**Shadow** — type characters, pick shade type (drop/cast/relief/block/beveled) +
direction -> offset/angle/depth numbers + diagram.

**Contrast** — value + harmony from a One Shot-style palette; grayscale value test;
pass/weak/fail rating; ranked best letter colors.

**Colors** — 32 Matthews paint recipes, searchable.

**Tools > Rows** — even menu lines via the yardstick-teeter method.

**Tools > Scale** — scale-up & grid calculator; multiplier, grid square/count,
measurement converter.

**Tools > Reference** — emphasis hierarchy, six alphabets, optical rules, ICS 1902
spacing card, ICS 1902 shading card, Casual & Slope card (Gage 1924), Roman
Construction card (Kynaston/DK 2024), Pen-Written Roman card (Gage 1924) —
nib pen thick/thin rules, proportions, per-letter notes — **Letter Spacing —
Optical card (John King)** — eye-first spacing, A/V/W gauge, double spacing —
**Layout & Lettering card (Bond 1937)** — 4 principles, high-light rule, balance
(pyramid/lever, obvious vs occult), proportion (Golden Measure), caps vs lower
case, character lettering.

**Tools > Kit** — brush series numbers, paint/thinner, brush care, transfer methods,
gilding checklist (Matthews), safety.

---

## Sources mined

- **Course transcripts** (a working sign painter's class; teacher Alex Jurakart,
  mentor "Doc") — the backbone.
- **Lester, Key to Practical Sign Writing (1903)** — exact Block & Roman stroke tables.
- **Matthews, How to Paint Signs & Sho' Cards (1920)** — colors, gilding,
  Egyptian/Half-Block proportions.
- **ICS, A Textbook on Lettering and Sign Painting (1902)** — spacing (by stroke,
  per family) + shading (45-deg light, five treatments). ~380pp, still largely unmined.
- **Gage, Vel-Vet Show Cards (1924)** — casual/single-stroke method, slope rules,
  pen-written Roman (thick/thin pen rules + per-letter notes). Available on
  archive.org inside the "117 Vintage Lettering Books" collection
  (identifier: wagner-blue-print-text-book-1946). More to mine: visual alphabet plates
  (image-only, need photos/scans).
- **Kynaston, Little Booklet of Roman Lettering (2024)** — DK Roman 10-point
  construction chart (in the app). Fully mined: the booklet has NO numeric
  lowercase/italic table — lowercase is derived by eye from the caps. Done.
- **John King, Quick Letter Spacing & Quick Layout lessons (LetterArt Academy)** —
  optical spacing (A/V/W gauge, double spacing) + negative-space "message-block"
  layout hierarchy. → Spacing card + Layout card + Sketcher negative-space check.
- **Bond, Showcard Lay-out and Design (1937)** — Ch. II Lettering + Ch. III Design
  & Lay-out: 4 principles, high-light rule, balance, proportion, subordination,
  repose, caps-vs-lower-case, character lettering. Still to mine: Ch. VI panel
  lay-outs, Ch. XII trade phrase lists (→ Ideas tab).
- **Source library on the W: drive** — `W:/Sign_Painting/` (`Sign painting books/`,
  `PDF/`, `Charts/`). Dozens of vintage titles (Speedball, French, Idarius, etc.).
  PDFs are image scans: render with PyMuPDF (`fitz`) → read PNGs.
- **Class Gothic chart photo** (Jurakart/Olson) — exact per-letter stems, in the app.

---

## Deploy workflow (automated)

Repo is cloned locally at `C:/Users/User/Documents/GitHub/sign-layout/`.
Edit `index.html` → Claude commits + pushes → GitHub Pages auto-deploys in ~1 min.
Git credentials work via Windows Credential Manager on that machine.

**From another machine:** clone `drtsuby/sign-layout`, open in VS Code, edit,
Source Control → Commit → Sync (or `git push`). Pages auto-deploys.

**Starting a new Claude session on a different machine:** paste this HANDOFF.md —
it has everything needed to pick up where we left off.

---

## Font workflow (A–Z preview)

A `fonts/` folder lives in the repo root and is served by GitHub Pages.

To add a font to the preview dropdown:
1. Drop the font file (`.ttf`, `.otf`, `.woff2`) into `fonts/`
   — either via GitHub web UI or into the local clone folder
2. Tell Claude the filename
3. Claude adds a `@font-face` declaration (in the `/* CUSTOM FONTS */` CSS section)
   and an `<option>` to `#specFontSel` using the filename as the label, then pushes

The font then appears in the "Preview font" selector on the A–Z tab.
**Only the filename/label is used as-is — no renaming.**

---

## Validation pattern (use on every build)

Extract `<script>` blocks and `node --check` each; confirm
`html.count('<div') - html.count('</div>') == 0` and section balance; confirm nav
buttons match sections. For any visual/SVG change, render the **actual app code** in
a real browser (playwright/chromium is installed) to a PNG and look — NOT a separate
copy. Rendering a separate copy caused repeated failures; `getBBox` only returns real
ink metrics in a live browser DOM.

---

## Parked / open

- **Hand-drawn letterforms.** Dropped — SVG-from-primitives couldn't match real
  letters and system fonts don't sit on the stroke-count grid. Replaced with
  font-based style preview. Realistic path: trace real outlines in Glyphs/FontForge
  into clean SVG paths.
- **Pricing/quote calculator** — highest-value unbuilt feature. Logic: per-sq-ft,
  gold leaf per linear ft, outline ~= doubles the job, dark-ground base-coat penalty.
- **Paint quantity estimator.**
- **Job save/recall for the Sketcher** (localStorage; works on hosted site, not in
  sandboxed previews).
- **More from ICS (1902)** — ~380pp, much unmined.
- **More from Gage** — visual alphabet plates (image-only in the PDF; need photos).
- ~~Kynaston lowercase/italic Roman~~ — RESOLVED: booklet has no numeric
  lowercase/italic table; lowercase is derived by eye from the caps. Nothing to add.
- **W: drive source library** — large collection at `W:/Sign_Painting/`
  (`Sign painting books/`, `PDF/`, `Charts/`). Mineable next: Speedball Textbooks
  (pen-width proportions, incl. lowercase + numerals), French *Essentials of
  Lettering* 1912, Bond Ch. XII trade phrase lists (→ Ideas tab) and Ch. VI panel
  lay-outs. PDFs are image scans (no text layer) — render with PyMuPDF (`fitz`),
  then read the PNGs; `pdftoppm`/Playwright are NOT installed on this machine,
  but Chrome headless works for app screenshots.
- **Additional books** — drop PDFs in chat or copy to a local path (or point at
  the W: drive).

---

## Conventions

Single self-contained `index.html`; no external deps except Google Fonts; assets
inline. Decimal measurements. Value contrast first; never trade legibility for
harmony. App is for someone who knows the craft. Trust the eye over the math.

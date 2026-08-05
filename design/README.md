# Handoff: AIMMI website (design phase → build)

## Overview
Design-phase deliverables for the aimmi.vn rebuild: a Vietnamese-primary marketing site with six client-side self-assessments. Structure and visual theme are signed off (Gate 0).

## About the design files
Everything in `wireframes/` and `themes/` is a **design reference created in HTML** — prototypes showing intended structure, look and behaviour, not production code. The task is to **recreate these in the target stack** (Astro 5 + Tailwind + Preact islands, per `docs/03-Build-Brief.md`) using `tokens.css` and the component inventory. Open any `.dc.html` file directly in a browser (each folder is self-contained with its `support.js`).

## Fidelity
- `wireframes/` — **low-fidelity.** Greyscale structure at 375px and 1280px for every page of the sitemap, plus five flow diagrams (`flows.dc.html`). Use for layout, content order, and interaction flow — not styling. Assessment wireframes are clickable with canned results. Copy is English placeholder; production copy is Vietnamese-first (+15–20% length).
- `themes/ho-so-mo.dc.html` — **high-fidelity, the chosen theme** ("Hồ sơ mở" — the open dossier). Recreate its four screens faithfully: home (375 + 1280), destination comparison, assessment question, assessment result (ready). Exact values live in `tokens.css`.
- `themes/ban-ve.dc.html`, `ho-so.dc.html`, `con-so.dc.html` — rejected alternatives, kept as the record of the comparison. (`ban-ve` references a design-system stylesheet not included here; it will render unstyled — that is fine.)

## Key screens (chosen theme)
1. **Home** — nav (logo, 5 items, VI/EN), dot-marked kicker, serif hero thesis, live question-1 card (dot progress, 4 option rows), destinations list, artefact photo cards, scope statements, footer.
2. **Destination comparison** — tint-banded table on desktop with criteria column; on mobile becomes destination tabs with persistent criteria labels (decision D3). INGWE disclosure on-page.
3. **Assessment question** — one question per screen, dot progress, back link, white card, 44px+ option rows.
4. **Assessment result (ready)** — the signature element: memo card with navy-tint header, serif verdict, rotated circular seal (navy ring, orange dot, "Sẵn sàng"), dot checklist of dimensions, memo paragraph; below it the navy service panel with fee range; then lastVerified + disclaimer + handoff line. Not-ready state: same memo grammar, no seal, no gate — see doc 05 §9 and the wireframes.

## Interactions & behaviour
Flows 1–5 in `wireframes/flows.dc.html`: assessment flow with gate-question early exit; the disqualification path; language switching (URL swaps slug, question index preserved); lead capture and consent (granular, unticked, allowlisted payload — never answers); destination routing (route *types*, never recommendations). Motion is limited to the result value revealing; respect `prefers-reduced-motion`.

## Design tokens
`tokens.css` is the single source: brand navy #224185 (700: #162C5B, tint: #E8EDF7), orange #EB8123 (deep #B25F12, small-text), paper #FBFAF6, page #FFFFFF, ink #2A2C33, lines #E3DFD2/#EFECE3; Literata 600 display over Public Sans; radius 6/8/12/pill; the dot motif at 8px. Tabular numerals for number sequences. No gradients.

## Assets
`../brand/` — the full AIMMI logo set (source PNGs carry large transparent canvases; `logo-cropped*.png` are trimmed web-ready variants: colour on light, white on navy, colour lockup with tagline). `themes/photo.jpg` is a placeholder photograph only — replace with real, consented photography.

## Files
- `tokens.css` · `decisions.md` (12 signed-off structural decisions) · `components.md` (component inventory) · `type-test.html` (diacritic test)
- `wireframes/index.dc.html` — entry point to all page wireframes + flows
- `themes/index.dc.html` — the four-theme comparison; `ho-so-mo.dc.html` is chosen

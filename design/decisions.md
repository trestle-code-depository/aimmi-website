# Design decisions — Phase C handover

Signed off by Tony (structure + Theme 4). The build (doc 03) does not relitigate these.

## Theme

**D0. Theme 4 — "Hồ sơ mở", the open dossier.** The paper file as organising principle: pages, document numbers, ruled rows, a verification seal — warmed with sentence-case Literata display, 8px corners, warm photography, and the logo's orange dots as progress/list/gap marks. Tokens in `tokens.css`. Chosen over the drawing (read engineering, not advisory), the pure dossier (too legalistic), and the number (too austere for sales material). **Guardrail:** the stamp, index numbers and ruled rows are load-bearing credibility — do not soften them away.

**D0a. Brand:** navy #224185 carries the accent role; orange #EB8123 is reserved for the dot motif and gap flags (deep step #B25F12 at small sizes); the logotype replaces set text in headers — colour lockup on paper, white variant on navy fields. Fonts self-hosted (Vietnamese subsets); a CDN font call is a cross-border transfer (doc 04 §3).

## Structure (Phase A, as wireframed)

1. **Primary nav is five items** — Assessments, Destinations, Services, Knowledge, About — Assessments second (doc 01 §8). Fees, Concerns, Contact, Partners and B2B live in the footer. Eight top-level items don't fit 375px.
2. **The homepage hero contains a live first question**, not a CTA. Answering it deep-links into question 2 of *ho-so-san-sang*.
3. **The comparison table on mobile becomes destination tabs**: criteria as persistent row labels, one destination column at a time. Desktop keeps the full table with a sticky criteria column. No horizontal scroll.
4. **Assessments are one question per screen at both widths**; desktop centres the question card. One flow to test and maintain.
5. **The not-ready result has no email gate anywhere.** Order: binding constraint → fixability → one honest alternative → optional emailed explanation, last.
6. **The ready result shows the paid service and fee range on the same screen**, above the fold on mobile. The itemised remediation plan is held back as the paid tier.
7. **Representatives render as verification rows** — name, licence number, register link — never logo cards.
8. **US and Panama pages are built as gated shells**: full structure, every claim inside a DRAFT — NOT CLEARED frame (doc 03 §3), so legal review is a walkthrough.
9. **Language toggle in the header at both widths**; mid-assessment it preserves the current question index (flow 3).
10. **Closed programmes page is a dated table**, newest first, each row carrying what replaced it — the credibility asset of doc 01 §3.
11. **Gate questions may end an assessment after one answer**, with a generous early-exit screen (the most-travelled path, flow 1).
12. **Result copy discipline:** banned-language lint (qualify / eligible / guaranteed / success rate / percentage likelihood); every result carries lastVerified, the disclaimer, and the readiness-vs-eligibility handoff line.

## Reference

- Annotated wireframes: `design/wireframes/` (index.dc.html — all pages at 375 + 1280, five flows).
- Copy is English placeholder; the Vietnamese pass (terminology glossary first, doc 01 §10) happens in build Phase 1. Layouts must absorb +15–20% text length.
- All bracketed placeholders ([FEE RANGE], [LICENCE NUMBER], …) are deliberate and must fail the clearance check if they survive to production (doc 03 §3.2).

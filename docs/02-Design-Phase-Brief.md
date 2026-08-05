# 02 — Design phase brief (Claude Code)

**This phase produces no production code.** It produces three artefacts for review and sign-off: a clickable wireframe, a set of flow diagrams, and three visual theme mockups. Nothing here carries forward directly except the token file of the chosen theme and the annotated wireframes.

**Why this phase exists:** structure disagreements found after the build are expensive; found in greyscale they cost an afternoon. And the visual direction needs a real choice between real alternatives, not the first thing that gets built.

---

## Phase A — Wireframes and flows

### A1. What to build

A static, clickable, **greyscale** wireframe site covering every page in doc 01 §8. Plain Astro with a single stylesheet. No visual design, no imagery, no brand, no colour beyond greys and one flat accent for interactive elements.

Every page. Not a representative sample — the argument this phase settles is about structure, and structure problems hide in the pages nobody wireframes.

### A2. Hard rules for wireframes

**Use real Vietnamese content, not lorem ipsum.** This is the single most important instruction in Phase A. Vietnamese runs roughly 15–20% longer than English for equivalent meaning, and diacritics increase line height. A layout that works in placeholder Latin text breaks in production. Write plausible Vietnamese for every heading, label, button and paragraph. Where exact copy is unknown, write realistic Vietnamese of realistic length.

**Build mobile first, at 375px, and show it first.** Zalo and Facebook in-app browsers are the primary first touch. Every page needs a 375px wireframe and a 1280px wireframe. If they conflict, mobile wins.

**Use placeholders for anything unverified.** `[PARTNER NAME]`, `[LICENCE NUMBER]`, `[FEE RANGE]`, `[STATISTIC — SOURCE NEEDED]`. Never invent a plausible-looking name, number or credential — that is the exact failure this rebuild exists to correct.

**Annotate.** Each wireframe carries margin notes explaining what a block is for and what decision it serves. The reviewer is Tony, not a designer.

### A3. Flow diagrams

Produce these as simple rendered diagrams (Mermaid is fine) on a `/flows` page:

1. **Assessment flow** — entry, gate questions, early-exit path, profile questions, result, PDF gate, lead capture. Show the early exit prominently; it is the most-travelled path.
2. **The disqualification path** — what a visitor sees, in what order, when their file is not ready. This is the most commercially important flow in the product and the one most likely to be designed carelessly.
3. **Language switching** — how state, progress and URL behave when a visitor switches mid-assessment.
4. **Lead capture and consent** — what is collected, what is not, which consent applies to which action, where each piece of data goes.
5. **Destination routing** — how a visitor moves from the global readiness assessment to a destination page without the tool ever recommending one.

### A4. Pages requiring particular care

| Page | Why |
|---|---|
| Home | Six blocks doing different jobs, on mobile, in a longer language |
| Destination comparison | A wide table on a 375px screen. Solve this properly; do not defer it |
| Assessment question | One question per screen on mobile, progress visible, back always available |
| Assessment result — not ready | The hardest screen to get right. It must be generous, specific, and not feel like a rejection |
| Assessment result — ready | Shows the result, holds back the paid detail, without feeling withheld |
| Representatives | Name, licence number, register link, in a way that reads as verification rather than endorsement |
| Fees | Ranges, three fee categories separated, no ambiguity about who is paid for what |

### A5. Deliverable

`/wireframes` — a browsable index linking every page at both widths, plus `/flows`. A written list of the structural decisions the wireframes assume, so Tony can disagree with them explicitly.

---

## Phase B — Theme mockups

### B1. What to build

**Three genuinely different visual directions**, each applied to the same four screens:

1. Home (mobile and desktop)
2. Destination comparison
3. Assessment question
4. Assessment result — the "ready" state

Each theme is a complete token set plus those four screens. Not three shades of one idea — three answers to the same brief that a client could reasonably choose between.

### B2. The brief each theme answers

Serious financial and legal decisions, made by Vietnamese business owners who read financial statements and are marketed to badly. The competitive set is maple leaves, stock families with passports, gold gradients and countdown urgency. **Looking like none of that is the design objective**, and restraint reads as competence to this audience.

### B3. Directions to avoid

Current AI-generated design clusters around three looks. All three are defaults rather than choices, and this brief leaves the visual axis open, so do not spend that freedom on them:

- Warm cream background (near `#F4F1EA`) with high-contrast serif display and a terracotta accent near `#D97757`
- Near-black background with a single acid-green or vermilion accent
- Broadsheet layout with hairline rules, zero border-radius, dense newspaper columns

If a proposed theme resembles one of these, revise it and say what changed.

### B4. What makes the three genuinely different

Vary the *organising principle*, not just the palette. Each theme should be describable in one sentence naming what it treats as the primary material — for example: the document, the number, the process, the archive, the ledger, the map. Derive palette, type and layout from that principle rather than choosing them independently.

For each theme produce, before building:

- **Palette:** 4–6 named hex values with roles
- **Type:** two families, with a stated reason for the pairing, and a type scale
- **Layout:** one-sentence concept plus an ASCII wireframe
- **Signature:** the one element this theme would be remembered by

Then review that plan against §B2 and §B3 before writing code. Revise anything that reads as a generic default and note what changed.

### B5. Non-negotiable per theme

- **Vietnamese diacritics render correctly at every weight used.** Test `ế ữ ỗ ằ ợ ặ ậ ườ ễ` in every face and weight. If a family fails, it is disqualified regardless of how it looks in English. Show the test string in the theme documentation.
- The **assessment result is the signature element** in all three. It is the one moment worth spending boldness on; everything around it stays quiet.
- Tabular numerals wherever numbers appear in sequence.
- Contrast ≥ 4.5:1 on body text, ≥ 3:1 on large text and interactive boundaries.
- No gradients. No red-and-white flag palette.
- Motion limited to the result value revealing. `prefers-reduced-motion` respected.

### B6. Deliverable

`/themes` — a comparison page showing all three side by side at both widths, plus `/themes/[name]` for each full walkthrough. A short written rationale per theme: the organising principle, why the type pairing, what the signature element is, and one risk each carries.

---

## Phase C — Handover package

On sign-off of structure and one theme:

1. `design/tokens.css` — the chosen theme's tokens, complete and final
2. `design/decisions.md` — every structural decision made in Phase A, with its rationale, so the build does not relitigate them
3. `design/components.md` — component inventory derived from the wireframes: name, purpose, variants, where used
4. `design/wireframes/` — the annotated wireframes, retained as reference
5. `design/type-test.html` — the diacritic test page for the chosen faces, kept for future font changes

Nothing else carries into the build. The wireframe site itself is discarded.

---

## Constraints for this phase

- **No real partner names, logos, licence numbers, fees or statistics.** Placeholders only.
- **No analytics, no third-party embeds, no external font CDN.** Fonts local from the start; a CDN font call is a cross-border data transfer with legal consequences (doc 04 §3).
- **Do not build assessment logic.** Wireframes and mockups show static states. Scoring belongs to the build phase.
- **Do not build the CMS, the clearance system, or the lead endpoint.** They belong to doc 03.
- Everything in this phase is throwaway except the Phase C package. Optimise for speed of iteration and clarity of comparison, not for code quality.

---

## Definition of done

Tony can, in one sitting: walk every page at mobile and desktop width, read the five flows, compare three themes side by side, and say "this structure, that theme." If any page requires explanation to interpret, the annotation failed.

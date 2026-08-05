# CLAUDE.md — build rules for this repository

Full authority: `docs/03-Build-Brief.md` (build) and `docs/04-Compliance-Register.md` (compliance). If this file and those conflict, the docs win. Design decisions in `design/decisions.md` are signed off — do not relitigate.

## Stack (doc 03 §2)

Astro 5 + TypeScript strict + content collections with Zod schemas · Preact islands for assessments only · Tailwind consuming `design/tokens.css` (no arbitrary values) · Decap CMS (git-backed) · Cloudflare Pages + one Worker for the lead endpoint · Vitest, Playwright, axe-core.

**Do not add dependencies without asking.** No analytics, chat widgets, remote font loaders, or A/B tools — each is a cross-border data transfer with legal consequences. Fonts are self-hosted (Literata + Public Sans, Vietnamese subsets).

## Non-negotiable rules

1. **Build the clearance gate first** (doc 03 §3). Every third-party claim, credential, fee or statistic carries a `clearance` object; production builds FAIL on any entry not `cleared`, any partner without logo consent + signed MOU, any US content without an I-956K receipt number, any remaining TODO. Dev/staging render uncleared content inside a `DRAFT — NOT CLEARED` badge.
2. **Never invent content.** Missing partner name, licence number, fee, statistic or threshold → a `TODO` marker that fails the clearance check. A plausible-looking invention is the exact failure this rebuild exists to correct (doc 04 §1).
3. **Assessment answers never leave the browser.** Scoring is pure and client-side; `sessionStorage` only, cleared on completion; the lead payload allowlist is name, email, optional phone, language, assessment id, result band, consent flags, timestamp, UTM — never answers. The Worker rejects any payload with keys outside the allowlist.
4. **Readiness, never eligibility.** Banned in result copy, both languages, enforced by lint: *qualify, eligible, guaranteed, success rate*, any percentage likelihood. AIMMI never represents clients (VI verbs to avoid: *đại diện*, *thay mặt*; use *chuẩn bị*, *hỗ trợ*, *biên soạn hồ sơ*).
5. **Vietnamese primary, English mirror.** VI at root, EN under `/en/`; no machine translation; a missing string fails the build; `hreflang` pairs with `x-default` → VI; diacritic check (`ế ữ ỗ ằ ợ ặ ậ ườ ễ`) at every weight in CI.
6. **No online ordering or payment, ever** (Bộ Công Thương notification perimeter). Booking is an outbound calendar link. No study-abroad or labour-export service pages — knowledge-base articles only, each naming the licensed provider. No employment content. No informal-capital-channel content.
7. **Staging is noindexed (header-level) and access-controlled from the first commit.** No partner name or logo anywhere — including staging — before the doc 04 §5 checklist is complete.
8. **Result screens follow doc 05 §9.** Not-ready: binding constraint → fixability → one honest alternative → optional email, never gated. Ready: service + fee range on the same screen; the itemised plan is the paid tier. Every result renders `lastVerified` + disclaimer + the readiness/eligibility handoff line.

## Tests that define done (doc 03 §13)

T1 ownership (30% registered last year + 8 claimed years → credited 0), T2 wealth (20bn claimed / 6bn documentable → 30%, gap is the headline), banned-phrase lint, payload guard, clearance gate failure, US gate failure, diacritics, i18n parity, axe-core clean, LCP < 2.0s on 4G, JS < 100kb on static pages.

## Design implementation

`design/tokens.css` is complete and final — if a value is missing, ask; do not invent. `design/components.md` names the component set. The wireframes in `design/wireframes/` are lofi structure references; `design/themes/ho-so-mo.dc.html` is the hifi look reference. Recreate in Astro/Tailwind — the HTML design files are references, not production code.

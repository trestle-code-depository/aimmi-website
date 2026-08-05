# AIMMI website

Rebuild of aimmi.vn. Vietnamese-primary marketing site with six in-browser self-assessments, built to be complete before it is publishable: every claim is gated on verification, consent and legal clearance.

## Read first, in order

1. `docs/00-README.md` — the document pack and the four governing principles
2. `docs/01-Strategy-Brief.md` — what AIMMI is, audience, messaging rule, sitemap
3. `docs/03-Build-Brief.md` — stack, clearance gating, everything this build must and must not do
4. `docs/04-Compliance-Register.md` · `docs/05-Assessments-Specification.md` · `docs/06-Technical-Manager-Instruction.md`

`CLAUDE.md` distils the build rules for AI-assisted work in this repo.

## Design (Phase A + B, signed off)

- `design/tokens.css` — final tokens: Theme 4 "Hồ sơ mở" (the open dossier)
- `design/decisions.md` — the theme choice and 12 structural decisions; do not relitigate
- `design/components.md` — component inventory
- `design/type-test.html` — Vietnamese diacritic test for the chosen faces
- `design/wireframes/` — annotated wireframes, every page at 375/1280 + the five flows (open `index.dc.html` in a browser)
- `design/themes/` — the four theme mockups (`ho-so-mo.dc.html` is the chosen one; the other three are the record of the comparison)
- `brand/` — the AIMMI logo set (navy #224185 / orange #EB8123) + cropped web-ready variants

## Sequence

```
PHASE 0  Clearance system, schemas, CI, environments, tokens   ← start here
PHASE 1  Structure + all static pages, VI + EN, all `draft`
PHASE 2  ownership + wealth assessments
PHASE 3  Remaining assessments, knowledge base, partners, B2B
PHASE 4  Redirects, performance, accessibility, legal-review build
```

Gates (docs/06): Gate 1 build complete (technical manager signs) → Gate 2 legal cleared (four counsel) → Gate 3 publish (Tony signs). **A production deploy path that can skip the clearance check is a bug.**

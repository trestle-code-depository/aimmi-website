# 03 — Build brief (Claude Code)

**Prerequisite:** doc 02 complete, structure and theme signed off, Phase C handover package in the repository.

**Critical context:** this site is built to completion with all partner names, logos and claims in place, but **must not be publishable** until MOUs are signed and four legal reviews are complete. The clearance system in §3 is the primary safety mechanism of this build. Implement it before any content is written.

---

## 1. Scope

| In | Out |
|---|---|
| Marketing site, VI primary + EN mirror | Client portal, file management |
| Six self-assessments (doc 05) | Payment processing |
| Knowledge base with editorial workflow | Online ordering on-domain (§9) |
| Partner and licensee listings | Document upload |
| Lead capture to a single endpoint | Any US programme content until doc 04 §4 clears |

---

## 2. Stack

- **Astro 5**, TypeScript strict, content collections with Zod schemas
- **Preact islands** for assessments — no framework on static pages
- **Tailwind** consuming `design/tokens.css` from the design handover; no arbitrary values in components
- **Decap CMS**, git-backed — content in the repo is what makes §3 enforceable
- **Cloudflare Pages**, plus one Worker for the lead endpoint
- **Vitest**, **Playwright**, **axe-core**

Do not add dependencies without asking. Specifically no analytics library, chat widget, remote font loader, or A/B tool — each creates a cross-border data transfer with legal consequences (doc 04 §3).

---

## 3. Clearance gating — build this first

Every assertion is either **safe** (AIMMI describing its own services) or a **claim** (anything about a third party, a credential, a foreign programme requirement, a fee, or a statistic).

### 3.1 Schema

```ts
const clearance = z.object({
  status: z.enum(['draft','legal_review','cleared']).default('draft'),
  clearedBy: z.string().optional(),
  clearedDate: z.string().optional(),
  jurisdiction: z.array(z.enum(['CA','VN','US','PA'])).default([]),
  evidenceRef: z.string().optional(),
  notes: z.string().optional(),
});

const partner = z.object({
  legalName: z.string(),
  displayName: z.string(),
  programmes: z.array(z.enum(['CA_PNP','US_EB5','PA_RESIDENCE','VN_STUDY','VN_LABOUR'])).default([]),
  logoConsent: z.boolean().default(false),
  logoConsentRef: z.string().optional(),
  mouSigned: z.boolean().default(false),
  mouDate: z.string().optional(),
  licenceNumber: z.string().optional(),
  licenceAuthority: z.string().optional(),
  licenceVerifiedDate: z.string().optional(),
  registerUrl: z.string().url().optional(),
  i956kFiledDate: z.string().optional(),
  i956kReceiptNumber: z.string().optional(),
  securitiesOpinionRef: z.string().optional(),
  feeModel: z.enum(['client_flat_fee','partner_commission','other']),
  clearance,
});
```

### 3.2 The gate — `scripts/check-clearance.ts`, pre-build

Fail the build in production if **any** of these hold:

- Any entry has `clearance.status !== 'cleared'`
- A cleared partner has `logoConsent === false` or `mouSigned === false`
- A partner has a `logoUrl` but no `logoConsentRef`
- An entry includes jurisdiction `VN` but has no `clearedBy`
- Content with `destination: 'US'` exists and no partner with `US_EB5` has a non-empty `i956kReceiptNumber`
- Content with `destination: 'US'` exists and `securitiesOpinionRef` is empty
- Any `TODO` or placeholder marker remains

Emit a build **warning in every environment** if a partner has `feeModel: 'partner_commission'` and `programmes` includes `US_EB5`, naming the securities question. It should be uncomfortable to ship.

In development and staging: warn, continue, and render uncleared content inside a `<ClearanceBadge>` — a bordered container labelled `DRAFT — NOT CLEARED` listing pending jurisdictions. This makes the legal review a walkthrough rather than a spreadsheet exercise.

Run in CI as well as locally. A production deploy path that can skip this check is a bug.

### 3.3 Evidence register

`content/evidence/*.md`, one entry per claim: claim text, source URL or document reference, date verified, verifier, jurisdiction. `evidenceRef` points here. Render at `/_internal/evidence`, 404 in production.

---

## 4. Repository structure

```
src/
├─ content/
│  ├─ pages/{vi,en}/          destinations/{vi,en}/     services/{vi,en}/
│  ├─ knowledge/{vi,en}/      partners/    representatives/    evidence/
│  └─ config.ts               Zod schemas incl. clearance
├─ assessments/
│  ├─ engine/  scoring.ts · Runner.tsx · types.ts
│  └─ configs/ readiness · ownership · wealth · oirc · personal · sector
├─ components/  layouts/  pages/  styles/tokens.css
scripts/  check-clearance.ts · check-redirects.ts · check-diacritics.ts · check-i18n-parity.ts
tests/  public/  workers/lead-endpoint/  design/
```

---

## 5. Internationalisation

- Vietnamese at root (`/dich-vu/...`), English under `/en/`. Vietnamese slugs are Vietnamese words, not transliterations.
- Every page must exist in both languages before reaching `cleared`. Enforce with a schema refinement and `check-i18n-parity.ts`.
- Correct `hreflang` pairs plus `x-default` → Vietnamese.
- Language toggle preserves the current page and, mid-assessment, the current progress.
- **No machine translation anywhere**, including UI strings. A missing string fails the build rather than falling back — a half-English Vietnamese page is worse than a build error.
- `check-diacritics.ts` renders `ế ữ ỗ ằ ợ ặ ậ ườ ễ` in every configured weight and fails on any substitute-font fallback.

---

## 6. Assessment engine

One engine, six configs. Full specification in doc 05.

**Hard rules:**

- **Scoring runs entirely in the browser.** No answer is ever sent to a server.
- **Answers are never persisted.** `sessionStorage` only, cleared on completion. No `localStorage`, no cookies, no server logging.
- Lead payload contains **only**: name, email, optional phone, language, assessment id, result band, consent flags, timestamp, UTM. Never the answers.
- **Readiness language only.** A lint rule scans result copy in both languages for a banned list: qualify / eligible / guaranteed / success rate / any percentage likelihood.
- Every result renders `lastVerified` and the standard disclaimer.
- Result displays free on screen. **PDF download requires an email address**; newsletter opt-in is separate and unticked. Never gate the on-screen result.

Build order: `ownership` and `wealth` first — they carry the commercial weight.

---

## 7. Lead endpoint

Single Cloudflare Worker. Validates, forwards to ClickUp.

- No API keys in the client bundle
- Rate limit by IP
- **Reject any payload containing keys outside the allowlist** — a standing guard against a future change reintroducing answers
- Log the fact of submission, not its contents
- `PUBLIC_DATA_REGION` flag so lead storage can be repointed to Vietnamese infrastructure without a rewrite, pending the legal opinion

---

## 8. Design implementation

Consume `design/tokens.css` and `design/components.md` from the handover. Do not introduce new tokens; if something is missing, ask rather than inventing a value.

Quality floor: responsive to 320px, visible keyboard focus, 4.5:1 contrast, labels tied to inputs, errors announced to screen readers, full keyboard operation, axe-core clean in CI.

---

## 9. What must not be built

- **No online ordering or payment.** Vietnamese e-commerce rules require notification to Bộ Công Thương for sites with an online ordering function; penalties include suspension and .vn domain revocation. Bookings are an outbound link to a third-party calendar; payment is offline.
- **No study-abroad or labour-export service pages.** Those sit with the licensed partner. Knowledge base coverage only, and every such article names the licensed provider.
- **No employment or job-offer content**, in any language.
- **No content describing ways to move capital outside registered channels.**
- **No invented content.** Missing partner name, licence number, fee, statistic or threshold → a `TODO` that fails the clearance check. Never generate a plausible placeholder.

---

## 10. Data protection

Vietnam's PDPL 91/2025/QH15 and Decree 356/2025/ND-CP took effect 1 January 2026. Financial information is sensitive personal data. Processing Vietnamese residents' data outside Vietnam is a cross-border transfer requiring an impact assessment filed with A05 within 60 days of the first transfer. Cross-border breach penalties reach 5% of prior-year revenue.

**The architecture minimises rather than manages:**

- Assessment answers never leave the browser, so the most sensitive data in the product is never transferred, stored or processed anywhere
- Only contact details and a result band cross a border
- Consent is granular, purpose-specific, unticked, in Vietnamese, captured separately for contact, newsletter, and cross-border transfer
- Consent records store timestamp and privacy policy version
- Versioned privacy policy in both languages; documented data subject request route with a named contact

---

## 11. Environments

| | Dev | Staging | Production |
|---|---|---|---|
| Clearance gate | Warn | Warn | **Fail** |
| Draft badges | Visible | Visible | N/A |
| robots.txt | `Disallow: /` | `Disallow: /` | Allow |
| `X-Robots-Tag` | noindex, nofollow | noindex, nofollow | none |
| Access | Cloudflare Access | Cloudflare Access | Public |
| `/_internal/*` | Available | Available | 404 |

**Staging is access-controlled and noindexed from the first commit.** A staging site carrying unconsented partner logos and indexed by Google is a published site.

---

## 12. SEO migration

`redirects.csv` maps every existing aimmi.vn URL to its destination, including retired pages. `check-redirects.ts` fails on any unmapped legacy URL or a chain longer than one hop. All EB-3 and US programme URLs → 301 to `/dich-vu`. `/co-hoi-canada` → `/diem-den/canada`.

---

## 13. Testing

| Test | Expectation |
|---|---|
| Scoring purity | Same input → same output; no I/O, no clock dependency |
| Ownership T1 | 30% ownership registered last year, 8 claimed owner-years → credited 0, fails on ownership evidence |
| Wealth T2 | 20bn claimed, 6bn documentable → 30%, gap is the headline result |
| Banned phrases | No qualify / eligible / guaranteed / success rate / percentage likelihood, either language |
| Payload guard | Endpoint rejects any payload containing an `answers` key |
| Clearance gate | Production build fails on any uncleared entry |
| US gate | Production build fails when US content exists without an I-956K receipt number |
| Diacritics | All test glyphs render at every weight |
| i18n parity | Every VI page has an EN counterpart and vice versa |
| Accessibility | axe-core clean; full keyboard traversal of each assessment |
| Performance | LCP < 2.0s simulated 4G; JS < 100kb on static pages |

---

## 14. Phases

| Phase | Deliverable | Done when |
|---|---|---|
| **0** | Clearance system, schemas, CI, environments, tokens | Production build fails on an uncleared entry; staging noindexed and access-controlled |
| **1** | Structure, home, destinations, five service pages, about, representatives, fees, concerns, contact — VI + EN | Both languages render; all entries `draft` |
| **2** | `ownership` and `wealth` assessments | Tests pass; no answer leaves the browser; PDF gate works |
| **3** | Remaining four assessments, knowledge base, partners, B2B page | Full i18n parity |
| **4** | Redirects, performance budget, accessibility pass, legal review build | Reviewer can walk staging and see every draft badge |

Publication is a separate event gated on §3 and doc 06 §7. Do not build a deploy-to-production path that can be triggered without the clearance check passing.

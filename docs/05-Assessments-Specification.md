# 05 — Assessments specification

Six assessments, one engine, six configs. Do not write six tools.

**What they are for:** triage, not lead generation. Every one must be willing to say a visitor is not ready and that AIMMI cannot help them yet. A visitor told that honestly returns in eighteen months and talks about you meanwhile.

The two carrying the commercial weight — **ownership** and **wealth** — mention no country's immigration requirements at all. They tell a Vietnamese business owner something about their own documents they did not know. That is a service they will pay for immediately, in Vietnam, in dong, whether or not they ever leave.

---

## 1. Engine

```ts
type AssessmentConfig = {
  id: string;
  questions: Question[];        // number | select | boolean | currency
  gates?: GateRule[];           // optional early-exit rules
  scoring: ScoringRule[];       // pure, declarative
  results: ResultBand[];        // thresholds → copy keys
  lastVerified: string;         // ISO date, rendered in the footer
};
```

**Hard rules** (repeated from doc 03 §6 because they are easy to erode):

- Scoring runs entirely in the browser. No answer is ever sent to a server.
- Answers are never persisted. `sessionStorage` only, cleared on completion.
- Lead payload: name, email, optional phone, language, assessment id, result band, consent flags, timestamp, UTM. **Never the answers.**
- Result displays free on screen. PDF download requires an email address; newsletter opt-in separate and unticked. **Never gate the on-screen result.**
- Every result renders `lastVerified` and the standard disclaimer.

**Flow:** gate questions first, and they may end the flow. Nobody should answer sixteen questions before being told the one thing that stops them. Progress visible, back always available, one question per screen on mobile.

---

## 2. Copy rules

| Don't say | Say |
|---|---|
| "You qualify" | "Your file has the documentation these programmes call for" |
| "You are not eligible" | "Your file is missing evidence every programme of this type requires" |
| "Your score is 112 of 175" | "Your documentation covers 9 of the 12 factors assessed" |
| "We recommend Nova Scotia" | "A licensed representative determines what applies to you" |

Banned in result copy, both languages, enforced by lint: *qualify, eligible, guaranteed, success rate,* and any percentage likelihood of an outcome.

Every result closes with the same handoff: **readiness is what AIMMI assesses; eligibility is determined by a licensed representative.**

---

## 3. `readiness` — Is your file ready?

The global entry point. Replaces destination selection with file assessment, which is both the honest framing and the better sales logic: it tells the visitor something about themselves before asking them to choose anything.

**8 questions:** deployable capital band · source of that capital (business income / property / inheritance / other) · years of documented business ownership · language level · willingness to relocate and manage actively versus invest passively · family composition · timeline · whether they have applied anywhere before and been refused.

**Output:** readiness across four dimensions — capital documentation, business evidence, personal documentation, outbound investment compliance — plus a plain statement of which *kinds* of route the file could currently support.

**Output constraint.** Names route *types*, never destinations, never eligibility:

> Files with your profile are most often prepared for **active business routes** (you operate a business, typically CAD 400–800k, requires relocation) rather than **passive investment routes** (larger capital, no operating role). A licensed representative for your chosen destination determines what you are eligible for.

Never "you should do EB-5." Never "Canada is right for you."

---

## 4. `ownership` — Is your ownership provable?

**Build first.** Catches the most common false positive in this market: family equity parked recently and presented as long-held.

**8 questions:**

| # | Field | Note |
|---|---|---|
| 1 | Registered ownership percentage | From the certificate, not what they consider their share of the family business |
| 2 | Year that percentage was registered | **Not the company founding year.** Check the amendment number on the certificate |
| 3 | Amendment number on the current certificate | |
| 4 | Do they appear on the company payroll | Ask for six months of payroll sheets |
| 5 | Are they the legal representative (*người đại diện theo pháp luật*) | |
| 6 | Years of filed financial statements available | |
| 7 | Company equity position — positive / negative / unknown | |
| 8 | Can related-party balances be explained | |

**Derived:** `ownershipTenure = currentYear − yearRegistered`, and credited owner-years capped at `min(claimedYears, ownershipTenure)`.

**Output:** readiness across six evidence categories, weakest named.

**Reference case (test T1):** 30% ownership registered last year, eight claimed owner-years, not on payroll, not the legal representative → credited owner-years 0, ownership evidence fails. If the tool ever passes this profile, the logic is wrong.

---

## 5. `wealth` — Will your wealth survive verification?

**Build second.** The sharpest output in the set.

**10 questions:** asset composition · registered owner of each asset · mortgages and charges outstanding · gold and cash holdings · property valuation basis · whether income tax was filed on the income behind each asset · gifts and family transfers · undocumented cash income · business equity book value · years of bank statements available.

**Output: documentable net worth versus claimed net worth, as a percentage.** That gap is the product. A client who declares 20 tỷ and can document 6 tỷ needs AIMMI and does not know it.

**Test T2:** 20bn claimed, 6bn documentable → 30%, with the gap as the headline result, not a footnote.

**Framing note.** This result will be uncomfortable for most visitors. Write it as a diagnosis, not a verdict: the gap is normal, it is fixable, and it is fixable faster before an application than during one.

---

## 6. `oirc` — Do you need an OIRC?

**6 questions:** planned investment amount · personal or corporate funds · source of funds · whether a Vietnamese company will hold the foreign entity · timeline · prior outbound transfers.

**Output:** OIRC required yes/no, estimated timeline, sequencing risk.

Include a **live CAD/VND and USD/VND threshold conversion**. The exchange rate decides which side of the line a client falls on, and nobody else in this market publishes it. Rate source and date must be shown.

Note for the result copy: at competitive investment levels for most destinations, the certificate is unavoidable rather than optional. That is the useful finding — clients routinely discover it after committing.

---

## 7. `personal` — Where are your gaps?

**7 questions:** language level and whether tested · education · whether an ECA exists · age band · spouse's language and education · relatives abroad · months lived, worked or studied abroad.

**Output:** a preparation plan ranked by effort and timeline. **Not a points score.**

Language is almost always the cheapest improvement and the one most reliably ignored. Offer a "not tested yet" option that produces a specific result state rather than a failure — untested is not the same as low.

---

## 8. `sector` — Which sector fits you?

Canada-specific. Lives under `/diem-den/canada`.

**6 questions:** sector of their own business · years operating it · deployable capital · willingness to relocate rural · buy versus build · timeline.

**Output:** three sector directions with plain reasoning drawn from the founder-background analysis. **No province names, no scores.** This is the free tier of the internal opportunity matrix; the matrix itself stays internal.

---

## 9. Result screen design

### When the file is not ready — the expected majority

Show this fully and generously. There is nothing to sell and a bad experience costs referrals.

- The binding constraint, named plainly: *"Your registered ownership is 30%, and it was registered last year. Programmes that count ownership experience generally require a third or more, held for at least three years."*
- Whether it is fixable and roughly how. Language is trainable in 6–12 months; ownership tenure is not retroactively fixable.
- **One honest alternative direction.** Many disqualified entrepreneur enquiries are viable skilled-worker or employer-driven files. Offer it as information, not a pitch.
- No email gate. Let them leave. Offer the emailed explanation.

### When the file is ready

Show: the readiness picture, the strongest and weakest evidence categories, and the paid service that closes the gap, with a fee range — **on the same screen, not one click away.**

Hold back: the itemised remediation plan with costs and timelines. That is the paid assessment. Tease its existence without giving it away.

---

## 10. Test matrix

| # | Input | Expected |
|---|---|---|
| T1 | Ownership 30%, registered last year, 8 claimed years, not on payroll | Credited years 0; ownership evidence fails; binding constraint is ownership, not money |
| T2 | 20bn claimed net worth, 6bn documentable | 30% documentable; gap is the headline |
| T3 | Strong file — 100% ownership since 2010, documented wealth, CLB 6 | All categories ready; paid service shown with fee range |
| T4 | Language "not tested" | No hard failure; result flags language as unassessed and as the cheapest available improvement |
| T5 | Ownership registered current year, 10 claimed years | Credited years 0 |
| T6 | Any | Result copy contains no banned phrase, either language |
| T7 | Any | Lead payload contains no `answers` key; endpoint rejects it if present |
| T8 | Vietnamese selected | Every string translated; no English fallback visible; diacritics render at all weights |

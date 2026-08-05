# 06 — Technical manager instruction

**Your role:** you own delivery, and you own the gate. The build can be produced quickly with AI assistance. What cannot be automated is verifying that every claim on the site is true, consented and cleared. That verification is the job.

**The one thing to internalise:** this rebuild exists because the current site published affiliations and credentials that were never secured. Speed is not the risk. Publishing something unverified is the risk, and it recurs quietly — a placeholder that looks plausible, a logo added "temporarily," a staging link shared with a client. Your controls exist to catch exactly those.

Read doc 04 §1 before anything else. The pattern described there has already recurred three times in this project.

---

## 1. Authority

**You decide:** technical architecture within the briefs, sequencing, tooling, hosting configuration, repository access, when a phase is complete.

**You escalate to Tony:** any content claim you cannot evidence · any request to publish before clearance · any partner asking for placement without signed consent · any change to what the site says AIMMI does · any new third-party service that would send data outside Vietnam.

**You have a veto on publication.** If the clearance check fails, the site does not go live, regardless of commercial pressure. **Get this acknowledged in writing before you start.** A veto that has not been agreed in advance is not a veto, and the moment it gets tested will be the moment there is pressure to launch.

---

## 2. The four gates

Nothing moves without the prior gate closed.

```
Gate 0 — DESIGN APPROVED     Tony signs structure + one theme
Gate 1 — BUILD COMPLETE      you sign
Gate 2 — LEGAL CLEARED       four counsel sign
Gate 3 — PUBLISH             Tony signs, you execute
```

### Gate 0 — design approved

Doc 02 delivered. Tony can walk every page at 375px and 1280px, read the five flows, compare three themes, and say "this structure, that theme." Confirm before signing:

- Every page in doc 01 §8 is wireframed at both widths — not a representative sample
- Wireframes use **real Vietnamese**, not lorem ipsum. Vietnamese runs 15–20% longer; a layout proven in Latin placeholder text is not proven
- No real partner names, logos, licence numbers, fees or statistics appear anywhere
- All three themes pass the diacritic test at every weight used
- The Phase C handover package is complete: tokens, decisions, component inventory, annotated wireframes, type test

### Gate 1 — build complete

- All phases delivered, CI green
- Every page exists in Vietnamese and English
- **Verify staging headers yourself** with a direct fetch — do not trust the config
- Evidence register has an entry for every claim marked `legal_review`
- No `TODO` markers remain
- Redirect map verified against a fresh crawl of the live site

### Gate 2 — legal cleared

Four counsel, four question sets (doc 04 §6). Every entry moves to `cleared` only with a named reviewer and date. **You enter clearance status; counsel does not touch the repository.** Their opinion arrives as a document; you transcribe it and file the document in the evidence register.

### Gate 3 — publish

Tony's written go, then §6.

---

## 3. Partner onboarding

Doc 04 §5 is the checklist. Three things to hold firm on:

**Verify licences at the issuing authority, not from the partner.** "They sent us their licence number" is not verification. Check the public register, screenshot it, date it. If a regulator ever asks why AIMMI relied on a partner's licence, the file answers for you.

**Nothing appears on staging either.** Staging with unconsented logos, if a link escapes, is publication.

**Diary the annual re-verification**, and re-verify immediately on any partner name or ownership change.

---

## 4. Environment security

Treat staging as public, because one shared link makes it public.

- Cloudflare Access with named users. No shared passwords. Review the list weekly and remove anyone who no longer needs access
- `noindex` enforced at header level, not only `robots.txt`. Verify by fetching headers
- **Never send a staging link to a client, partner or prospect.** If a partner needs to review their own entry, send a screenshot
- Secrets in the platform secret store. Audit repo history for committed keys before adding any external contributor
- Branch protection on `main`: no direct pushes, CI must pass, one review required

---

## 5. Working with AI-generated code

Three failure modes, in priority order:

**Plausible fabrication.** The most dangerous output is a confident, well-formatted claim nobody supplied — a licence number, a fee, a statistic, a threshold. It reads as authoritative precisely because it is fluent. **If you cannot trace a factual assertion to the evidence register, it does not ship, however reasonable it looks.** The clearance check catches marked TODOs; it cannot catch a confident invention.

**Silent scope creep.** An added dependency, a CDN font, an embedded widget — each can create a cross-border data transfer with legal consequences. **Review the dependency diff on every pull request**, not just the source diff.

**Copy drift.** Regenerated content quietly reintroduces banned language. The lint rule catches the known list; read result copy yourself when it changes.

---

## 6. Publication runbook

Any no-go stops the sequence.

1. Gate 2 signed by all four counsel, documents filed
2. Tony's written go
3. Run the production build locally — **clearance check passes with zero warnings**
4. Verify every partner entry against doc 04 §5
5. Verify the redirect map against a fresh crawl of the live site
6. Verify the privacy policy is live, versioned, and referenced by consent records
7. Full backup of the current site and database
8. Deploy
9. Remove `noindex`, submit the sitemap
10. Verify: headers, `hreflang`, 20 sample redirects, all assessments end to end in both languages, one lead arriving with no answers in the payload
11. Verify the old site's problematic claims are gone from **every** URL, including cached and duplicate pages
12. Monitor 404s daily for two weeks

**If step 3 fails, stop.** Do not override. It failing is the system working.

---

## 7. After launch

| Cadence | Task |
|---|---|
| Weekly | 404 report · lead delivery check · staging access review |
| Monthly | Dependency and security updates · review content edited since last check |
| Quarterly | **Re-verify every programme threshold at source**, update `lastVerified`. The single most likely way this site becomes wrong |
| Six-monthly | Update the data protection impact assessment · re-verify partner details if changed |
| Annually | Full licence re-verification · accessibility audit |

The `lastVerified` date renders publicly. That is deliberate — it makes neglect visible. Do not let it go stale.

---

## 8. When something changes

**A programme closes or a threshold moves.** Update the config, refresh `lastVerified`, check whether any knowledge base article is now untrue. Five programmes have closed or gone dormant in eighteen months; assume this happens again.

**A partner withdraws consent.** Remove the same day. Set `clearance.status` to `draft`; the gate handles the rest.

**Someone asks to add a logo before consent is in.** No. The answer is a one-paragraph email requesting written permission; publication follows the reply. This is the exact failure the rebuild exists to correct, and it will be asked for under time pressure.

**Legal opinion changes something structural.** Escalate rather than patch. A finding that, say, the vendor arrangement does not hold changes the sitemap, not a paragraph.

---

## 9. Weekly report to Tony

Five lines:

1. Phase status and anything blocked
2. Content entries by clearance status: draft / in review / cleared
3. Partners by checklist completion
4. Open items needing a decision from Tony
5. **Anything found that was published previously and is not true**

Line 5 matters most in the early weeks. Assume there is more of it on the current site than the review has already found, and report it as you encounter it rather than saving it up.

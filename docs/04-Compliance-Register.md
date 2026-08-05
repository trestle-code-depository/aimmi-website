# 04 — Compliance register

**Purpose:** one source of truth for every rule that constrains the site, across four jurisdictions. The technical manager maintains it. Counsel reviews against it.

**Evidence grades:** **[A]** read from a primary government source · **[B]** consistent across multiple professional sources, unconfirmed at source · **[C]** judgement.

---

## 1. What went wrong before — the pattern to prevent

The current site states that each client's profile is "legally and transparently represented by AIMMI, SK Immigration & Law," and describes the licensee as "a member of the Canadian Immigration Consultants Association IRCC." **No such association exists.** It also describes a "collaborative – cooperative – as one relationship" between the two firms.

Three failures in one paragraph: an invented credential, a claim that an unlicensed Vietnamese company represents immigration files, and language merging a licensee with an unlicensed entity.

**The pattern is publishing an affiliation or credential that was never secured.** It has recurred in this project three times in different forms — the original credential, the proposal to use partner logos before consent, and the assumption that a partner's licence covers AIMMI. Every control in doc 03 §3 exists to catch this specific pattern.

### Immediate actions on the live site — do not wait for the rebuild

| Action | Status |
|---|---|
| Remove the fabricated association reference, VI and EN | ☐ |
| Remove all "represents your file" language | ☐ |
| Retire EB-3 and US programme pages | ☐ |

---

## 2. Canada — CICC

| Rule | Grade |
|---|---|
| AIMMI never represents a file before an immigration authority. Vietnamese verbs to avoid: *đại diện*, *thay mặt*. Use *chuẩn bị*, *hỗ trợ*, *biên soạn hồ sơ* | [A] |
| Licensed representatives named individually with licence number and public register link | [A] |
| No outcome guarantees, success rates, or *cam kết đậu* — anywhere, including social embeds and testimonials | [A] |
| Published fee ranges separating AIMMI's fees, third-party professional fees, and government fees at cost | [A] |
| A "How to raise a concern" page naming the CICC with address and telephone | [A] |
| **No referral fees, received or paid**, in either direction. Stated publicly | [A] |
| Individuals choose their own representative; AIMMI receives nothing for the choice | [A] |

**Structure:** AIMMI is an arm's-length preparation firm. It is not an agent of any licensee. Where firms are AIMMI's clients, published rules of engagement state that AIMMI does not represent clients, that firm-originated clients are never solicited, and that file contents are never used for AIMMI's marketing.

---

## 3. Vietnam

### 3.1 Data protection — the highest-consequence item

| Item | Detail | Grade |
|---|---|---|
| Governing law | PDPL 91/2025/QH15 and Decree 356/2025/ND-CP, both effective 1 January 2026, replacing Decree 13/2023 | [B] |
| Sensitive data | Financial information is expressly sensitive personal data | [B] |
| Cross-border definition | Processing Vietnamese residents' data on systems located outside Vietnam counts as a transfer — captures cloud services and global platforms | [B] |
| Transfer impact assessment | Filed with A05 within 60 days of first transfer; updated every six months on regulated changes; retained at head office | [B] |
| Penalty | Up to 5% of prior-year revenue for cross-border breaches | [B] |
| Possible relief | Five-year grace period from 1 Jan 2026 for small enterprises and startups on DPO and operational standards, conditions apply; micro-enterprises exempt from impact assessments | [B] |

**Architectural response:** assessment answers never leave the browser. Only contact details and a result band cross a border. This removes the sensitive data from scope entirely rather than managing its transfer.

### 3.2 Licensing perimeter

| Activity | Position | Grade |
|---|---|---|
| Study-abroad consulting | Conditional business line; licence from provincial Sở Giáo dục và Đào tạo; 80–100m VND fine under Decree 88/2022 for operating without it | [B] |
| Labour export | Licensed under Law 69/2020. Any content reading as arranging overseas employment sits near this regime | [B] |
| Settlement consulting | Boundary genuinely unsettled in commercial sources. **Requires a written local opinion** | [C] |

**Structure with the licensed partner:** the partner holds the client, contracts, is paid, and is the named provider. AIMMI is the partner's vendor for defined non-licensed preparation work. **A partner's licence does not cover AIMMI** — licensing attaches to the entity conducting the activity. If AIMMI advertises the service, quotes, signs the client and then hands the file over, AIMMI is conducting an unlicensed conditional business.

Website consequence: study abroad and labour mobility are **information in the knowledge base**, never service pages, and every such article names the licensed provider.

### 3.3 Advertising

Advertising rules require documentary proof of claims. The amended Advertising Law 75/2025/QH15 imposes joint liability across advertiser, agency, publisher and any KOL or influencer who carries a message without checking it; penalties under Decree 38/2021. **[B]**

This reaches the Zalo and Facebook strategy, not only the site. An influencer repeating an unverifiable claim exposes both parties.

### 3.4 E-commerce notification

Since 1 January 2022, Decree 85/2021 narrowed the obligation: **only sites with an online ordering function must notify** Bộ Công Thương. A site that introduces and displays services without on-site ordering does not. Penalties under Decree 98/2020 include 6–12 month suspension of e-commerce activity and .vn domain revocation. **[B]**

**Build consequence:** no online ordering or payment. Bookings are an outbound calendar link; payment is offline.

### 3.5 Capital movement

The OIRC service is on the right side of this line — it helps people comply. The site must never read as advice on moving capital outside registered channels: no workaround content, no comparison of informal routes, no worked examples implying one. **[C]**

---

## 4. United States — EB-5 via INGWE Global

**All items below block US content. None blocks the Canada launch.**

| Item | Detail | Grade |
|---|---|---|
| Promoter registration | Form I-956K required under the EB-5 Reform and Integrity Act 2022 for any person or entity promoting a regional centre, NCE, JCE or securities issuer to immigrant investors — migration agents explicitly included | [B] |
| Who files | **AIMMI files its own.** INGWE's registration does not cover AIMMI | [B] |
| Timing | Must precede promotion. Marketing may begin on issuance of the I-797 receipt notice; no approval step | [B] |
| Disclosure | The form requires disclosure of the written agreement with each entity including compensation terms — **the INGWE agreement must be final before filing** | [B] |
| Pending change | A proposed rule published July 2026 would broaden the promoter definition and require individual filings from each employee meeting it. Monitor | [B] |
| Securities law | EB-5 investments are securities. Transaction-based compensation for soliciting investors implicates US broker-dealer registration independently of I-956K | [B] |

**The fee model decides the securities question.** A flat, disclosed fee paid by the client for defined preparation work, unrelated to whether any investment is made, sits very differently from a commission per investor placed. **Obtain a written US securities opinion before the MOU is executed** — this is the most consequential structural decision in the partnership and expensive to unwind.

**Panama:** if the route involves a fund, a real estate offering or any pooled investment, the securities questions apply again. If it is a residence application with direct property purchase, they largely do not. Establish which before writing the page.

---

## 5. Partner onboarding checklist

No partner name or logo appears anywhere, **including staging**, until all rows are complete and filed.

| # | Item | Evidence held |
|---|---|---|
| 1 | Written consent to be named | Email or MOU clause, PDF |
| 2 | Written consent to use the logo | Same |
| 3 | Licence verified **at source** | Dated screenshot of the register entry showing licence number and exact legal name |
| 4 | MOU signed | Executed PDF |
| 5 | *(EB-5 only)* AIMMI's I-956K receipt | I-797 notice |
| 6 | *(EB-5 only)* Securities opinion on the fee model | Written opinion |

**The consent request, sent this week:**

> May we name [Firm] as a practice we provide Vietnam-side preparation services to, and use your logo on our website? Cross-marketing arrangements can follow separately if useful.

**Verify licences at the issuing authority, not from the partner.** CICC public register, provincial law society, provincial Sở Giáo dục và Đào tạo, the public register of licensed labour-export enterprises. Confirm three things: current, exact legal name, covers the specific activity. Keep the dated screenshot. Re-verify annually and immediately on any name or ownership change.

**What replaces a logo wall:** for this audience, logos of unfamiliar foreign firms carry almost no weight. Name, licence number, and a register link are checkable in ten seconds and demonstrate the exact transparency the old site failed.

---

## 6. Legal review — four counsel, four question sets

Do not combine. A combined packet produces a combined answer that satisfies no one.

### Canadian counsel
1. Does anything on this site constitute Canadian immigration advice or representation by AIMMI?
2. Do the assessments stay on the readiness side of the line?
3. Is the description of each licensed representative relationship accurate and complete?
4. Does the fee presentation meet transparency expectations?
5. Any residual exposure from the prior site's claims the rebuild does not resolve?

### Vietnamese counsel
1. Does AIMMI's activity touch the conditional-business perimeter for study-abroad consulting, or Law 69/2020? **Does the vendor-to-licensed-partner structure keep AIMMI outside it? Get this in writing.**
2. Under PDPL and Decree 356: does AIMMI qualify for the small-enterprise grace period? Does the lead architecture require a transfer impact assessment, and on what timeline?
3. Are the consent mechanisms compliant in form and language?
4. Does the site require Bộ Công Thương notification given no online ordering function?
5. Do any claims breach advertising rules? Note joint liability reaching influencers — this affects the social strategy.
6. Does promoting a foreign securities offering to Vietnamese residents engage Vietnamese securities or public-offering rules?

### US immigration counsel
1. Does anything on the site constitute US immigration advice?
2. Is the I-956K filing complete and accurate?
3. Does the EB-5 content meet RIA marketing standards?

### US securities counsel — **obtain first**
1. Does the fee model with INGWE require broker-dealer registration?
2. Does any site content constitute an offer or solicitation of securities?
3. What disclosure is required?

Obtain the securities opinion before the others, because it may change the commercial agreement — and everything else is written on top of that agreement.

---

## 7. Ongoing verification

| Cadence | Task |
|---|---|
| Quarterly | **Re-verify every provincial and programme threshold at source**; update `lastVerified`. The single most likely way this site becomes wrong |
| Six-monthly | Update the data protection impact assessment; re-verify partner details if changed |
| Annually | Full licence re-verification for every partner; accessibility audit |
| On change | Programme closes or threshold moves → update config, refresh `lastVerified`, check the knowledge base for newly untrue statements |
| On withdrawal | Partner withdraws consent → set `clearance.status` to `draft` the same day; the gate handles removal |

The `lastVerified` date renders publicly on every assessment. That is deliberate: it is a credibility signal and it makes neglect visible.

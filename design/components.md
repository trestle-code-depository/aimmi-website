# Component inventory — Phase C handover

Derived from the Phase A wireframes and the Theme 4 mockups. Names are suggestions for `src/components/`; all styling from `tokens.css`, no arbitrary values (doc 03 §2).

## Shell

| Component | Purpose | Variants | Used on |
|---|---|---|---|
| `Nav` | Header: logo, 5 items, language toggle. The one 2px ink rule sits under it | mobile (hamburger) / desktop | every page |
| `LangToggle` | VI/EN switch; preserves page and mid-assessment progress | header / inline | every page |
| `Footer` | Four columns: About/Partners/Fees · Help · For firms · Scope statement | mobile 2-col / desktop 4-col | every page |
| `SectionMark` | Orange dot + serif heading + optional document number ("Hồ sơ 02") | with/without number | all content pages |

## Content

| Component | Purpose | Variants | Used on |
|---|---|---|---|
| `Button` | Actions | primary (navy fill) / secondary (navy outline) / block | everywhere |
| `Tag` | Pill label ("Phiếu 01 · Tự đánh giá") | navy fill / tint | assessment cards, badges |
| `Card` | White sheet, line border, radius-lg, shadow-card | plain / linked (arrow) | destinations, services, KB |
| `ArtefactCard` | Photo + one-line caption (deliverables, team) | photo / placeholder | home, about, services |
| `ComparisonTable` | The destination comparison | desktop table (tint header band, sticky criteria col) / mobile tabs + criteria rows | /diem-den |
| `DataTable` | Fees, provinces, closed programmes | with lastVerified column | fees, canada subpages |
| `VerificationRow` | Name · licence number · authority · verified date · register-link button | person / firm | home, /doi-tac |
| `DisclosurePanel` | INGWE relationship, on-page | — | /diem-den, hoa-ky, panama |
| `ScopeList` | "What AIMMI does not do" dash list | — | home, about, B2B |
| `ArticleCard` | KB entry: topic · dates · title · summary; names licensed provider where required | — | /kien-thuc |
| `ClearanceBadge` | DRAFT — NOT CLEARED frame listing pending jurisdictions (doc 03 §3.2) | — | dev/staging only, any uncleared entry |

## Assessment engine (one engine, six configs — doc 05)

| Component | Purpose | Variants | Notes |
|---|---|---|---|
| `AssessmentIntro` | Title, scope, privacy line, lastVerified, Start | — | privacy line verbatim: answers stay in the browser |
| `ProgressDots` | Orange/line dots, one per question | — | replaces bars; the dot motif |
| `QuestionCard` | Serif question + helper note + options; Back always available | — | one per screen, both widths; desktop centres it |
| `OptionButton` | Full-width answer row, radius-md | default / hover (navy tint) | 44px+ hit target |
| `EarlyExit` | Generous gate-exit screen: answer, why, honest alternative | — | flow 1's most-travelled path |
| `ResultMemo` | The signature: tint header + serif verdict + `Seal` + dot checklist + memo paragraph | ready / not-ready | not-ready: constraint → fixability → alternative, no gate |
| `Seal` | Circular navy seal, rotate(8deg), orange dot + "Sẵn sàng" | ready only | never on not-ready |
| `DotChecklist` | Dimension rows: dot (navy=đủ, orange=thiếu, line=chưa) + state word | — | no scores, no percentages |
| `ServicePanel` | Navy panel: the paid service + fee range + CTA, same screen as result | — | ready result only |
| `PdfGate` | Email for PDF only; newsletter checkbox separate, unticked | — | never gates the on-screen result |
| `ResultFooter` | lastVerified · disclaimer · readiness/eligibility handoff line | — | every result, both languages |

## Forms & consent

| Component | Purpose | Notes |
|---|---|---|
| `Field` | Label-tied input, radius-md, navy focus ring | errors announced to screen readers |
| `ConsentCheckbox` | Granular, purpose-specific, unticked, Vietnamese | separate boxes: contact / newsletter / cross-border (doc 03 §10) |
| `BookingLink` | Outbound calendar link, marked external | no on-site ordering, ever (doc 04 §3.4) |

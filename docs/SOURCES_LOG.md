# Sources & Decisions Log — J26-IT-363

Every finding, decision, or scope pivot made by a human or an agent on this project must be
logged here with a source and justification (project rule #3). This is a running ledger, append
only — do not delete old entries even if superseded; mark them `SUPERSEDED` instead.

**Format per entry:**

```
### YYYY-MM-DD — <short title>
- **Type:** finding | decision | pivot
- **Claim:** what is being asserted
- **Source:** URL / DOI / file / conversation, resolved and checked (not just plausible)
- **Justification:** why this source supports the claim, in one or two sentences
- **Recency check (if a research paper):** publication year; if older than 5 years
  (pre-2021-08), state why it qualifies as a foundational/classical exception (see CLAUDE.md rule 4)
- **Status:** active | superseded by <link to entry>
```

Pre-existing verified sources for each module already live in `docs/REFERENCES_BY_COMPONENT.md`
(one row per paper, with venue/year/link/what it's used for). Do not duplicate that table here —
this log is for *new* findings, decisions, and pivots made from this point forward (2026-08-28
onward), including anything that revises or overturns what's in that file.

**Note on `docs/FACTS_COMPILED.md` (removed 2026-08-28):** that file was the raw fact-check audit
this project's verified references were distilled from. It has been deleted as redundant now that
its durable findings are captured here and in `docs/REFERENCES_BY_COMPONENT.md`. If you need the
full original fabrication write-up (exact wrong-DOI resolutions, etc.) beyond the list preserved
below, it is not recoverable from this repo — re-verify from scratch instead of assuming a prior
finding.

---

## Baseline entries (retroactive, from project setup on 2026-08-28)

### 2026-08-28 — TAF v5 is the panel-accepted canonical scope
- **Type:** decision
- **Claim:** The project's official scope is TAF v5 ("A Decentralized, Edge-Native AI Framework
  for Sustainable Hiking Tourism in Sri Lanka" — four loosely-coupled modules: IMU terrain/effort,
  litter+degradation vision, offline RAG assistant, ST-GNN carrying-capacity forecasting).
- **Source:** `taf/TAF-J26-IT-363-v5-ACCEPTED.pdf`, page 7 — Topic Screening Panel section, marked
  "Topic Assessment Accepted", comment "All components are acceptable", signed by panel members
  Junias Anjana and Thisara Shyamalee, dated 2026-07-07.
- **Justification:** This is the only version of the TAF in the project files bearing panel
  signatures and an "Accepted" mark. No other version has been reviewed.
- **Status:** active

### 2026-08-28 — TAF v6 is an unreviewed, unaccepted draft pivot
- **Type:** finding
- **Claim:** A newer draft (v6) exists that reframes the same four modules around PINN, UDA,
  MILP, a custom "Dynamic Inference Power Manager", and "EdgeRAG" — a much heavier mathematical
  framing than the accepted v5.
- **Source:** `taf/TAF-J26-IT-363-v6-DRAFT.pdf`, all 6 pages (no supervisor/panel section filled
  in, no signatures, no acceptance mark).
- **Justification:** Compared directly against v5's signed panel page — v6 has no equivalent
  page 6/7 approval content, so it has not gone through the screening process.
- **Status:** active — flagged as an open risk in `CLAUDE.md`. Needs explicit team confirmation
  before any agent treats v6 as current scope.

### 2026-08-28 — Sajana batch of the literature-tracking sheet is ~90% fabricated
- **Type:** finding
- **Claim:** 9 of 10 entries attributed to "Sajana" in `research/Research Topics.xlsx` are
  fabricated or mismatched citations (invented DOIs, DOIs resolving to unrelated papers, or
  titles with no web presence at all). The specific entries, so nobody re-cites them:
  - "Edge Computing … Avalanche Risk" — no link, no paper with this title exists.
  - "AR Navigation for Off-Trail Hikers" (DOI 10.3390/mti7060058) — real DOI, but the real paper
    is *on-trail* AR guidance (MTI 2023); title was embellished. Weak, not usable as-is.
  - "Wearable Biosensors … Altitude Sickness" (DOI 10.1371/journal.pbio.2001402) — real DOI,
    resolves to PLOS Biology 2017 general wearable health tracking, not altitude sickness.
  - "Gamification of Sustainable Hiking" (DOI 10.3390/su71014128) — DOI does not exist (404 on
    doi.org and CrossRef).
  - "Predicting Trail Congestion … Geotags" — no link, no such paper (only urban-traffic geotag
    work exists).
  - "Solar-Powered Drone Relays" (DOI 10.1109/ACCESS.2019.2931456) — real DOI, resolves to IEEE
    Access 2019 wildfire-spread prediction via smartphones; unrelated.
  - "ML for Automated Flora Identification" (DOI 10.1007/s10514-017-9654-z) — DOI does not exist
    (that prefix belongs to *Autonomous Robots*, not botany).
  - "Acoustic Monitoring of Wildlife" (DOI 10.1093/biosci/biz009) — real DOI, resolves to
    BioScience 2019 on gene-editing governance; unrelated.
  - "Blockchain for Ecotourism Funding" — no link, no such paper.
  - "Haptic Feedback Trekking Poles" — no link, no such paper.
- **Source:** checked directly against the doi.org resolver and the CrossRef metadata API for
  each DOI above (verification performed 2026-06-29 per the original audit; re-confirmed present
  in `research/Research Topics.xlsx` on 2026-08-28).
- **Justification:** Direct resolver/API verification, not just plausibility — this is the
  standard this project holds all citations to (rule #3).
- **Status:** active. Do not cite any Sajana-batch entry without independently re-verifying it
  from scratch first.

### 2026-08-28 — Headline "1.2 million hikers by 2035" figure is a vendor estimate, not fact
- **Type:** finding
- **Claim:** The oft-repeated "1.2 million international hikers by 2035" traces only to a paid
  commercial vendor forecast (Future Market Insights: 610k in 2025 → 1.2M in 2035, ~8.6% CAGR),
  not a government or peer-reviewed source, and should never be presented as an established
  projection or as "exponential" growth.
- **Source:** Future Market Insights commercial trekking-market forecast (as traced in the
  project's original 2026-06-29 fact-check audit); cross-checked against the Gemini Deep Research
  chat exports that first introduced the figure (now removed — see entry below).
- **Justification:** Traced the figure to its origin; the verified, citable growth figure instead
  is the IESC/USAID Pekoe Trail Demand Study's "~35,000 dedicated hikers by 2033", confirmed
  verbatim in the source PDF.
- **Status:** active. `docs/PROJECT_PROPOSAL.md` §1 already applies this correction — keep new
  writing consistent with it.

### 2026-08-28 — Two Module 4 citations re-verified with real years; one could not be re-verified
- **Type:** finding
- **Claim:** Two Module 4 references were missing a publication year in
  `docs/REFERENCES_BY_COMPONENT.md` and have now been confirmed: "GCN–LSTM Analysis of
  Spatiotemporal Evolution of Node Centrality in Tourism Flow Networks" (Jia & Chen, Informatica
  49(14), published 2025-11-23, DOI 10.31449/inf.v49i14.10973) and "Forestry Tourism Resource
  Carrying Capacity Prediction Model Based on Multi-Source Data Algorithm" (Ma & Geng, MDPI
  Forests 17(5):534, 2026). Both pass the 5-year recency rule. A third, "Hybrid tourist-arrivals
  forecasting, Sri Lanka" (claimed as ResearchGate publication 392533688), **could not be
  re-verified** — the URL returns 403/inaccessible and no web search matches that specific
  publication ID or a "hybrid" Sri Lanka tourist-arrivals title; several similarly-named but
  differently-ID'd papers exist, none matching.
- **Source:** direct WebFetch/WebSearch re-verification, 2026-08-28 (see also
  `docs/REFERENCES_BY_COMPONENT.md` Module 4 table, rows now updated with full titles/years/⚠️).
- **Justification:** Rule #3 requires every citation to be independently resolved, not assumed —
  these three had no confirmed year on record, which also made the 5-year rule unverifiable for
  them.
- **Status:** active. The Jia & Chen and Ma & Geng citations are now fully verified and safe to
  use. **The "RG 392533688" hybrid-arrivals citation must not be used in any deliverable
  (proposal, thesis, presentation) until re-verified from scratch** — either find the correct
  ResearchGate ID for the paper actually being described, or drop the claim it supports (it was
  being used as a national-arrivals covariate reference for Module 4) and replace it with a
  verified alternative.

### 2026-08-28 — Project Charter already submitted; binding AI-usage policy discovered
- **Type:** finding
- **Claim:** The Project Charter checkpoint (previously assumed upcoming/undated) was actually
  already submitted on **2026-08-01**, alongside a signed "Use of AI Policy: Student Declaration
  and Agreement." All four members (Kankanige S.S as group leader, Weerasekara J.V, Ahamed M.N.I,
  Ahamed M.M) and the supervisor (Dr. Prasanna Sumathipala) signed it. The policy requires: AI as
  a support tool only, transparent disclosure of AI use, full student accountability for
  AI-assisted output, and that the student must be able to explain/justify/defend that work in
  evaluations.
- **Source:** `governance/Project Charter.pdf`, all 3 pages — dates and signatures verified
  directly from the document (all four member signatures dated 01/08/2026; supervisor signature
  dated 2026/08/1, read as 01/08/2026 given the surrounding declarations).
- **Justification:** Primary-source document, directly read and transcribed, not inferred.
- **Status:** active. Updated `docs/GOVERNANCE_SUMMARY.md` (new §6, and the Charter row in the
  IT-specialization checklist table) and `CLAUDE.md` (new rule #5) to reflect both the Charter's
  completed status and the binding AI-usage terms. This supersedes the assumption made earlier in
  this session that the Charter was an upcoming, undated deliverable to prep for — it is done.

### 2026-08-28 — Added Module 4 extended methodology & plan of work to the Proposal
- **Type:** decision
- **Claim:** Added `docs/PROJECT_PROPOSAL.md` §5.5, expanding Module 4's methodology
  justification (why ST-GNN vs. baselines is a testable hypothesis, not an assumed win; why the
  synthetic foot-traffic target is partially but not fully circular; ECC framed as a derived
  output, not a validated prediction) and a 7-phase plan of work, ahead of preparing the full
  Proposal + Ethics Form submission (the next deliverable after the already-accepted TAF v5).
- **Source:** synthesized directly from already-verified project material — no new external
  claims were introduced. Architecture/risk reasoning drawn from `docs/TECHNICAL_AUDIT.md`
  "C4 — ST-GNN dynamic carrying capacity" section; citations reused from
  `docs/REFERENCES_BY_COMPONENT.md` Module 4 table (AAAI 2024, PMC11723455, Jia & Chen 2025 —
  all previously verified); evaluation protocol (paired t-test, p<0.05, spatial block CV) reused
  from `docs/PROJECT_PROPOSAL.md` §9, which was already in the document.
- **Justification:** No new factual/citation claims were added, only methodological argument
  built from already-sourced material — satisfies rule #3 without needing new verification.
- **Status:** active. Plan-of-work phase dates are explicitly left unscheduled pending the
  Charter, which the team has not yet defined — do not backfill dates without the team's input.

### 2026-08-28 — Raw Gemini Deep Research chat transcripts and FACTS_COMPILED.md removed
- **Type:** decision
- **Claim:** The three raw Gemini chat exports (`research/Gemini Chats/*.txt`, the origin
  material for this project's topic) and `docs/FACTS_COMPILED.md` (the raw fact-check audit) were
  deleted as redundant once their durable content was distilled into
  `docs/REFERENCES_BY_COMPONENT.md`, `docs/PROJECT_PROPOSAL.md`, and this log.
- **Source:** human instruction, this session, 2026-08-28 ("feel free to clean up the docs, fact
  check, combine, delete as needed / same goes for current content of research folder").
- **Justification:** Both were AI-generated intermediate material (Gemini Deep Research chats;
  a fact-check working document), not primary sources in their own right — the primary sources
  are the papers/datasets/DWC-SLTDA figures those chats pointed to, which are already captured in
  `docs/REFERENCES_BY_COMPONENT.md`.
- **Status:** active. One notable item from the raw chats did NOT make it into any surviving doc
  and needs follow-up: the chats describe a **"Limits of Acceptable Change" (LAC)** management
  framework as the theoretical justification for why a dynamic ECC (Module 4's output) is
  preferable to a static permit quota — e.g. "50 hikers in a monsoon downpour can degrade a trail
  more than 300 hikers on a dry day; a fixed quota can't see that, but tracking against LAC
  thresholds can." This is a genuinely useful framing for Module 4's literature review, but as
  captured in the chats it has **no cited source** (it's Gemini's own prose, not a paper
  reference) — do not use it in any deliverable until the research-agent finds and verifies an
  actual citable LAC source (the concept originates from Stankey et al., US Forest Service
  recreation-management literature; confirm a real, ideally <5-year, application to trail/
  ecotourism carrying capacity before citing).

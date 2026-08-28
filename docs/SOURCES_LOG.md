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

### 2026-08-28 — Proposal skeleton built; structure validated against external precedent
- **Type:** decision
- **Claim:** Built `docs/PROPOSAL_SKELETON.md`, a section-by-section gap analysis for the Research
  Proposal deliverable (the checkpoint after the accepted TAF v5 and submitted Charter). The
  skeleton confirms the existing `docs/PROJECT_PROPOSAL.md` structure (shared front matter +
  problem/objectives, one literature-review chapter with per-module subsections, one methodology
  chapter with per-module subsections, shared plan-of-work/ethics/conclusion) already matches real
  precedent for multi-component proposals, rather than needing a restructure — the work
  remaining is mostly gap-filling (front matter, word-count expansion, weaving in new citations),
  not new architecture.
- **Source:** structural precedent researched this session — (1) Horizon Europe work-package
  proposal convention (enspire.science grant-writing guide, grey literature, cited for structural
  convention only, not a technical/scientific claim); (2) University of Iowa Human Subjects
  Office "Umbrella Project Educational Tool" (existence and structural shape confirmed via search
  snippet; full-text extraction failed — PDF returned unreadable binary to the fetch tool — so
  treat the structural claim as adequately but not exhaustively verified); (3) a deliberate
  negative/contrast example, Silvestri et al. 2024 (Sensors 24(7):2376, DOI 10.3390/s24072376),
  which fuses multiple subsystems into one shared-architecture narrative with no per-subsystem
  methodology — used to illustrate the failure mode this project must avoid (flattening Module
  4's own methodology into a shared "system" description), not as a source to emulate.
- **Justification:** Two independent institutional contexts (grant-writing, human-subjects
  research governance) converging on the same "shared front + full per-component deep-dive"
  shape is reasonable evidence the pattern is generic rather than an artifact of one body's house
  style — sufficient grounding for a structural (not factual/scientific) claim.
- **Status:** active. Four new Module 4 literature sources were also found and logged in this same
  research pass (Gupta et al. 2025 BuildSys, Zhu et al. 2021 Expert Systems with Applications, Du
  et al. 2025 Applied Intelligence, Dong et al. 2025 JABES) — see `docs/REFERENCES_BY_COMPONENT.md`
  Module 4 table for full entries; two directly strengthen the §5.5 "why the GNN isn't circular
  and must beat baselines" argument and are flagged in `docs/PROPOSAL_SKELETON.md` §3.5 as not yet
  woven into that section's prose.

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

### 2026-08-28 — Proposal-skeleton research: multi-module umbrella structure precedent + 3 new Module 4 sources
- **Type:** finding
- **Claim:** Researched precedent for how a single proposal document should structure 4
  loosely-coupled sub-modules (for the upcoming skeleton), and found three genuinely new, verified,
  recent Module 4 sources relevant to justifying the "small-graph GNN vs. baseline" and
  "synthetic-target validation" methodology presentation. Full detail below; skeleton reasoning
  reported separately to the requesting agent, not duplicated here.
- **Source(s), each independently resolved:**
  1. Horizon Europe work-package guidance (enspire.science, "Work Packages in Horizon Europe: How
     to do it right", accessed 2026-08-28, https://enspire.science/work-packages-in-horizon-europe-how-to-do-it-right/)
     — grey-lit grant-writing guide, not an academic paper; used only as structural precedent, not
     a factual/technical claim.
  2. University of Iowa HSO "Umbrella Project Educational Tool" (PDF,
     https://hso.research.uiowa.edu/sites/hso.research.uiowa.edu/files/2024-04/Umbrella%20Project%20Educational%20Tool.v4.10.27.2022.pdf)
     — official university research-governance document; confirmed to exist via search snippet
     (full PDF text extraction failed — binary/compressed stream, not re-attempted since the
     search snippet already gave the needed structural fact and this is grey-lit precedent, not a
     load-bearing technical citation).
  3. Silvestri et al., "An Urban Intelligence Architecture for Heterogeneous Data and Application
     Integration, Deployment and Orchestration", Sensors (Basel) 24(7):2376, 2024. DOI
     10.3390/s24072376, resolved directly via https://pmc.ncbi.nlm.nih.gov/articles/PMC11014012/
     (title/authors/venue/year confirmed on the page itself). Used as a *contrast* precedent — a
     real multi-subsystem systems paper that uses a single layered shared-architecture narrative
     WITHOUT per-subsystem deep-dive methodology sections (i.e., the pattern this proposal should
     NOT copy, since Module 4 needs its own full methodology).
  4. Gupta, Raina, Chen, Chen, Danilov, Eckhardt, Bernard, Nahrstedt, "No One-Model-Fits-All:
     Uncovering Spatio-Temporal Forecasting Trade-offs with Graph Neural Networks and Foundation
     Models" (arXiv preprint title: "Evaluating Spatio-Temporal Forecasting Trade-offs Between
     Graph Neural Networks and Foundation Models"), arXiv:2511.05179 (submitted 2025-11-07,
     v2 2025-11-30), peer-reviewed and published at the 12th ACM International Conference on
     Systems for Energy-Efficient Buildings, Cities, and Transportation (BuildSys '25), Golden CO,
     Nov 2025. DOI 10.1145/3736425.3771958, resolved via doi.org redirect to
     https://dl.acm.org/doi/10.1145/3736425.3771958 and cross-checked via search snippet of the
     ACM proceedings TOC. Compares STGNNs against classical (VAR), neural (GRU, Transformer), and
     time-series foundation models on sparse/small IoT sensor-network graphs (not large urban
     traffic networks) — directly precedent for Module 4's "GNN must earn its keep vs. baselines
     on a small graph" methodology framing.
  5. Zhu, Zhang, Li, Zhou, Dai, Hu, "Spatiotemporal multi-graph convolutional networks with
     synthetic data for traffic volume forecasting", Expert Systems with Applications 187:115992,
     2022 (online-first/indexed October 2021). DOI 10.1016/j.eswa.2021.115992, resolved via
     CrossRef API (https://api.crossref.org/works/10.1016/j.eswa.2021.115992) confirming exact
     title, authors, journal, and October 2021 online date. Precedent for a peer-reviewed GNN
     forecasting paper that explicitly uses synthetic training data as part of its methodology
     (analogous to Module 4's synthetic foot-traffic target), i.e. shows synthetic-data-assisted
     GNN training/validation is an accepted, published pattern, not a novel weakness unique to
     this project.
  6. Du, Liu, Li, "Pedestrian flow prediction using a spatiotemporal multi-head attention graph
     convolutional network integrated with knowledge graph", Applied Intelligence 55(13):896, 2025
     (online 2025-07-29, print Aug 2025). DOI 10.1007/s10489-025-06793-8, resolved via CrossRef API.
     Domain-relevant (pedestrian/foot-traffic flow, not vehicle traffic) recent GNN precedent for
     Module 4's literature review.
  7. Dong, Chu, Zhang, Ghaderi, Yang, "Pedestrian Volume Prediction Using a Diffusion Convolutional
     Gated Recurrent Unit Model with Dynamic Time Warping", Journal of Agricultural, Biological and
     Environmental Statistics 17(3), 2025 (online 2025-06-09). DOI 10.1007/s13253-025-00696-4,
     resolved via CrossRef API. Also domain-relevant (pedestrian volume, not vehicle traffic),
     recent, GNN/graph-adjacent precedent for Module 4.
- **Justification:** Items 4–7 are new, independently resolved (DOI/CrossRef/ACM-proceedings
  cross-checks, not assumed from titles), on-topic for Module 4, and pass the 5-year recency rule
  (all published/online-dated after 2021-08-28). Items 1–3 are structural/precedent sources for the
  proposal-skeleton pattern question, not technical claims, logged for traceability per rule #3
  even though they carry a lower evidentiary bar than a scientific citation.
- **Recency check:** arXiv:2511.05179 / ACM BuildSys'25 — Nov 2025, well within 5 years. Zhu et al.
  2021/2022 — online-dated Oct 2021, which is *after* the 2021-08-28 cutoff, so it qualifies as
  current (not a foundational exception) — flagged explicitly here because the print year (2022 in
  vol. 187) could otherwise look ambiguous. Du et al. 2025 and Dong et al. 2025 — both well within
  5 years. Silvestri et al. 2024 — within 5 years (used as structural/contrast precedent, not a
  technical claim, so recency is not load-bearing here anyway).
- **Status:** active. A candidate MDPI paper ("Pedestrian Flow Prediction in Open Public Places
  Using Graph Convolutional Network", ISPRS Int. J. Geo-Inf. 10(7):455) was found but **excluded**
  — confirmed published 2021, vol 10 issue 7 (July), which is before the 2021-08-28 cutoff with no
  later online-first date found; do not cite it without re-confirming an online-first date on or
  after 2021-08-28.

### 2026-08-29 — §4.5 literature-review deepening pass: LAC sourced, dead citation replaced, 9 new Module 4 sources
- **Type:** finding + decision
- **Claim:** Ran a dedicated research pass to close the specific gaps flagged in
  `docs/PROPOSAL_SKELETON.md` for Module 4's literature review (§4.5): (1) find a real citable
  source for the "Limits of Acceptable Change" framing that had been used only as unsourced prose
  from an old Gemini chat export; (2) replace the dead RG 392533688 citation; (3) deepen each of
  the five thematic strands (ST-GNN architecture, tourism-flow precedent, small/sparse-graph
  precedent, synthetic-target precedent, local carrying-capacity grounding); (4) find precedent for
  DEM-derived TWI as an ML covariate. All nine results below were independently verified (CrossRef
  API, doi.org redirect, or the publisher's own landing page — not title-plausibility alone) and
  have now been woven into `docs/PROJECT_PROPOSAL.md` §4.5 (rewritten as five thematic prose
  paragraphs, each ending in an explicit critique sentence per the skeleton's "critique, not just
  gap" note) and §5.5 (baseline-justification and synthetic-target paragraphs), and added to
  `docs/REFERENCES_BY_COMPONENT.md`'s Module 4 table.
- **Source(s), each independently resolved:**
  1. **LAC foundational citation** — Stankey, Cole, Lucas, Petersen, Frissell, "The Limits of
     Acceptable Change (LAC) System for Wilderness Planning", USDA Forest Service Gen. Tech. Rep.
     INT-GTR-176, 1985. Verified via the official USDA Forest Service Treesearch record
     (https://research.fs.usda.gov/treesearch/66741), cross-checked against Internet Archive and
     Biodiversity Heritage Library listings showing identical bibliographic data.
     **Foundational/classical exception (rule #4)** — 1985, cited for the named LAC method itself,
     on the same basis as the already-accepted Cifuentes 1992 exception; every recent paper on LAC
     (including #2 below) still cites this as the origin.
  2. **LAC modern application** — Dragovich & Bajpai, "Managing Tourism and Environment—Trail
     Erosion, Thresholds of Potential Concern and Limits of Acceptable Change", Sustainability
     14(7):4291, 2022-04-04. DOI 10.3390/su14074291, resolved via doi.org redirect and
     independently cross-confirmed via the CrossRef API. Applies LAC/TPC empirically to hiking-trail
     erosion (trail width as the impact indicator) in a high-visitation national park. Passes the
     recency rule (2022-04-04, after the 2021-08-28 cutoff).
  3. **Replacement for dead RG 392533688** — Hewapathirana, "Advancing tourism demand forecasting
     in Sri Lanka: evaluating the performance of machine learning models and the impact of social
     media data integration", Journal of Tourism Futures 11(2):261 (online 2023-12-15, print 2025).
     DOI 10.1108/JTF-06-2023-0149, confirmed via the Emerald publisher landing page and
     independently via the CrossRef API (which additionally confirms both the online and print
     dates). Sri Lanka-specific, hybrid SVR/Random Forest/ANN vs. SARIMA baseline, covers the same
     methodological ground (hybrid statistical/ML national tourist-arrivals forecasting) the dead
     citation was meant to cover.
  4. Uremović, Mongus, Pur, Lukač, "Contextualized spatio-temporal graph-based method for
     forecasting sparse geospatial sensor networks", Expert Systems with Applications 294:128779,
     2025-12. DOI 10.1016/j.eswa.2025.128779, confirmed via CrossRef API bibliographic match
     (direct ScienceDirect fetch was blocked with HTTP 403 — CrossRef is the authoritative
     registry, treated as sufficient verification, but flagged for a human with institutional
     ScienceDirect access to do a final visual confirmation before final submission, same caveat
     for findings #5 and #6 below).
  5. Acciai, Bilotta, Fanfani, Nesi, "Graph neural network for continuous traffic density
     estimation on unmonitored roads from very few scattered measurements", Expert Systems with
     Applications 327:132713, 2026-09 (per CrossRef). DOI 10.1016/j.eswa.2026.132713, confirmed via
     CrossRef API. Structural analogy to Module 4's sparse manual-calibration-count situation.
  6. Gayathri, Harshitha, Kriyasri, Balasundaram, "Enhancing crowd management through
     behaviourally informed synthetic datasets and predictive deep learning models", Results in
     Engineering 28:108210, 2025-12. DOI 10.1016/j.rineng.2025.108210, confirmed via CrossRef API
     and independently corroborated by a ResearchGate listing and a VIT-Chennai research-centre
     newsletter PDF describing identical content.
  7. Ryu, Jung, Kim, Lee, "Visitor Number Prediction for Daegwallyeong Forest Trail Using Machine
     Learning", Sustainability 17(13):6061, 2025-07. DOI 10.3390/su17136061, confirmed via CrossRef
     API and independently corroborated via a ResearchGate listing describing the same methodology
     (RF/GBM/LightGBM + Bayesian optimization, weather/social-media/calendar covariates, SHAP,
     six trail sections).
  8. Guo, Chen, Bai, Zhang, "Landscape Drivers of Trail Formation in Peri-Urban Mountains: Insights
     from an Explainable Machine Learning Approach", Land 15(5):715, 2026-04. DOI
     10.3390/land15050715, confirmed via CrossRef API metadata fetch (which returned the abstract
     directly) and independently corroborated by a search snippet explicitly confirming slope,
     elevation, and **TWI** are used as covariates.
  9. Zhang, Wang, Yu, Yang, Zhou, Wang, "Do We Really Need GCNs in Traffic Forecasting? A
     Graph-Less Pure-MLP Architecture", Companion Proceedings of the ACM Web Conference 2025 (WWW
     '25 Companion), 2025-05. DOI 10.1145/3701716.3715464, confirmed via CrossRef API (direct ACM
     landing-page fetch blocked with HTTP 403, same CrossRef-as-authoritative caveat as #4–#6).
     Stronger, more directly on-point than the already-logged Gupta et al. 2025 for the "graph
     structure isn't automatically worth it" argument, since this one is an empirical graph-free-
     vs-GCN ablation rather than a GNN-vs-foundation-model comparison.
- **Justification:** All nine are independently verified (not title-plausibility), on-topic for
  Module 4, and pass the 5-year recency rule except the deliberately-flagged Stankey 1985
  foundational exception. Satisfies rule #3 (source + one-line justification for every claim) and
  rule #4 (recency, with the foundational exception explicitly labelled rather than presented as
  recent literature).
- **Recency check:** All of #2–#9 are dated 2021-08-28 or later (earliest is Zhu et al., already
  logged 2026-08-28, online-dated Oct 2021). #1 (Stankey et al. 1985) is explicitly flagged as the
  foundational/classical exception per rule #4, not presented as recent.
- **Searched but excluded (do not re-search these angles expecting a different result without new
  cause):**
  - No Sri Lanka/Horton Plains-specific carrying-capacity paper newer than the already-logged
    Senevirathna & Perera (2015) was found — the 2015 citation remains the best available; do not
    treat this as unresearched.
  - Páskova, Wall, Zejda, Zelenka, "Tourism carrying capacity reconceptualization" (J. Destination
    Marketing & Management 21, DOI 10.1016/j.jdmm.2021.100638) — CrossRef lists the volume as
    September 2021 but the precise online-first date relative to the 2021-08-28 cutoff could not be
    confirmed (ScienceDirect fetch blocked, no precise date in available search snippets). **Not
    used** — genuinely ambiguous, not guessed in either direction. If a human with ScienceDirect
    access confirms an online-first date ≥2021-08-28, it would support the dynamic-vs-static
    carrying-capacity narrative and could be added later.
  - Liu et al., "Do We Really Need Graph Neural Networks for Traffic Forecasting?" (arXiv:2301.12603,
    Jan 2023, the "SimST" paper) — content verified to exist and match its claimed conclusion, but
    no confirmed peer-reviewed venue found. **Not used as primary** — Zhang et al. 2025 (ACM WWW
    Companion, finding #9) makes the same argument with confirmed peer review and is cited instead;
    Liu et al. could be added as secondary/supporting only if a preprint citation is later judged
    acceptable.
  - No wilderness/trail/rural-recreation-domain GNN paper with an explicitly small node count
    (comparable to Horton Plains' 25–40 nodes) was found — all small/sparse-graph precedent
    (findings #4, #5, plus the already-logged Gupta et al.) remains transportation/geospatial-
    sensor domain, applied by structural analogy only. `docs/PROJECT_PROPOSAL.md` §4.5 states this
    explicitly as a critique rather than overstating the match.
  - SiGuNiang Mountain Scenic Area tourist-flow paper (Wang, Jiang, Su, ACM ICCNIOT 2024, DOI
    10.1145/3670105.3670137) — verified to exist, but uses LSTM + Baidu search-behaviour data, not
    a graph neural network, and is a small regional conference proceedings paper. Not used.
  - VisitHGNN (Pang & Yang, arXiv:2510.02702, Oct 2025) — verified to exist (heterogeneous GNN for
    POI visit-pattern modelling, Fulton County GA) but urban/socio-demographic, unconfirmed peer
    review, no small-graph framing. Not used — doesn't add anything beyond what's already cited.
  - ForecastPFN/TimePFN-style synthetically-trained zero-shot time-series foundation models — real,
    but general time-series, not spatio-temporal-graph or occupancy/crowd-specific. Not used.
  - Freycinet National Park GNSS visitor-tracking study (Journal of Sustainable Tourism 28(2),
    2019) — real, but pre-2021-08-28 and not a named foundational method, so does not qualify for
    the recency exception. Not used.
- **Status:** active. Follow-ups for a human to action before final submission: (a) confirm the
  Páskova et al. 2021 online-first date via direct ScienceDirect access if the dynamic-vs-static
  carrying-capacity narrative would benefit from one more citation; (b) do a final visual
  confirmation of findings #4, #5, #6 (Uremović, Acciai, Gayathri) and #9 (Zhang et al.) on their
  publisher pages if institutional/VPN access to ScienceDirect/ACM DL is available, since the fetch
  tool was blocked (HTTP 403) on all four and CrossRef API was used as the authoritative fallback.

### 2026-08-29 — §4.5.1 synthesis table added (no new sources; pure synthesis of already-verified findings)
- **Type:** decision
- **Claim:** Added `docs/PROJECT_PROPOSAL.md` §4.5.1, a 17-row comparison table placing every
  ST-GNN/flow-forecasting precedent from §4.5 (domain, graph size, real-vs-synthetic ground truth,
  whether the paper tests a non-graph baseline) plus a final row placing Module 4 itself on the
  same axes, per `docs/PROPOSAL_SKELETON.md` §2.7's synthesis/taxonomy recommendation.
- **Source:** no new external sources — every row reuses a citation already verified and logged in
  the 2026-08-29 entry above or in the pre-existing Module 4 table in
  `docs/REFERENCES_BY_COMPONENT.md`. This is a synthesis/organizational pass over already-verified
  material, not a new factual claim.
- **Justification:** Rule #3 is already satisfied by the underlying per-source verifications; this
  entry exists for traceability of the *editorial* decision (which axes to compare on, and the
  "only 2 of 17 test a non-graph baseline" observation drawn from the table) rather than to
  introduce a new claim requiring independent verification.
- **Status:** active.

### 2026-08-29 — Front matter added (title page, TOC placeholder, list of figures/tables, acronym list)
- **Type:** decision
- **Claim:** Added a Front Matter block to `docs/PROJECT_PROPOSAL.md`: a title page (project ID,
  title, programme, supervisor/co-supervisor, the four-member ownership table), a placeholder note
  for the Table of Contents (deferred to auto-generation once structure is locked, per the
  skeleton's own instruction not to hand-number), a List of Figures/Tables enumerating the tables
  already in the document, and a full alphabetical List of Acronyms cross-checked against every
  acronym actually appearing in the current document text (not a generic list).
- **Source:** team/supervisor names and reg. numbers reused from `CLAUDE.md`'s ownership table
  (itself sourced from the panel-accepted TAF v5, per the existing 2026-08-28 log entry); no new
  external claims were introduced.
- **Justification:** Purely organizational/mechanical content synthesized from already-verified
  project facts — no new factual/citation claim requiring independent verification under rule #3.
- **Status:** active. Submission date left explicitly blank (no team-confirmed deadline exists yet
  in any project doc) rather than guessed. Flagged in the title page itself: re-confirm the
  member/module table hasn't changed before final submission.

### 2026-08-29 — Whole-project Plan of Work added; dates deliberately left blank
- **Type:** decision
- **Claim:** Added `docs/PROJECT_PROPOSAL.md` §10 "Plan of Work (whole-project)": a shared-
  milestones table (TAF and Charter marked Done with their real dates; Proposal marked In Progress;
  PP1, PP2, Final Evaluation, and Thesis Submission all marked "Not started — date TBD") and a
  coarse three-window per-module phase-mapping table (Proposal→PP1 / PP1→PP2 / PP2→Final) that
  reuses Module 4's existing §5.5 7-phase breakdown rather than restating it, plus a short
  individual-member-contribution note pointing back to the Title Page's ownership table rather than
  redrafting it. Renumbered the former §10 ("Corrections carried over from the source-material
  audit") to §11 to make room.
- **Source:** milestone names and statuses reused directly from `docs/GOVERNANCE_SUMMARY.md` §4,
  which was itself checked in this same pass and confirmed to list milestone *names* only, with "—"
  in every date column except the Charter (already submitted, 2026-08-01) and implicitly the TAF
  (already accepted, 2026-07-07, per the existing 2026-08-28 log entry). No new external claims.
- **Justification:** Rule #3 is satisfied by the reused, already-verified facts; no new citation
  was needed since this is a scheduling/organizational document, not a factual claim. The decision
  to leave PP1 onward undated rather than estimate a schedule is itself the notable choice here —
  worth logging so a future session doesn't mistake the blank dates for an oversight.
- **Status:** active. Explicit follow-up: once the team/supervisor confirms PP1/PP2/Final/Thesis
  dates, replace the three coarse windows in the per-module table with real date ranges and
  consider upgrading to a Gantt-style view (per the Horizon Europe work-package precedent already
  used to validate this document's overall structure, see the 2026-08-28 skeleton-research entry
  above) — do not backfill dates without that confirmation.

### 2026-08-29 — Abstract and Conclusion added; proposal skeleton's Module-4 gap list now closed except M1–M3 lit review and real dates
- **Type:** decision
- **Claim:** Added an Abstract (~200 words, placed before §0, covering motivation/problem/
  four-module framework/Module-4 methodology/expected outcomes, no fabricated "key findings" since
  this is proposal- not results-stage) and a Conclusion (placed after §10 Plan of Work, before the
  renumbered §11 Corrections/erratum section) to `docs/PROJECT_PROPOSAL.md`, following the 4-step
  process in `docs/LEC_NOTES_DIGEST.md` (answer the RQ at a proposed-approach level; reflect on the
  research process; give narrow recommendations; state contribution) and introducing no new data,
  citation, or argument beyond what §0–§11 already establish.
- **Source:** synthesized entirely from already-verified/already-logged material in this document
  and this log — no new external claims. The Conclusion explicitly cites the Stankey et al. 1985
  LAC framing and the §4.5.1/§5.5 baseline-testing discipline, both already verified and logged
  earlier in this same 2026-08-29 session.
- **Justification:** Purely a synthesis/writing pass over already-verified material — no new
  factual or citation claim requiring independent verification under rule #3.
- **Status:** active. This closes every Module-4-scoped item on `docs/PROPOSAL_SKELETON.md`'s
  priority list from the 2026-08-28 skeleton pass except two items explicitly left open by design:
  (a) real PP1/PP2/Final/Thesis dates, blocked on team/supervisor input; (b) M1–M3 literature-review
  depth, out of Module-4 scope per the user's explicit instruction this session to skip it.

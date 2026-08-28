# Principles and Rules for This Project

A single practical rulebook combining (a) what IT4010 ("Research Methods and Professional
Practice", module code CMM708) actually teaches and requires, (b) SLIIT Faculty of Computing
compliance rules, and (c) this project's own working rules for Module 4 (Weerasekara J.V. —
Crowd & Carrying-Capacity Forecasting). Written so a team member can open one file before making
a scope, methodology, ethics, writing, or citation decision, instead of searching three source
documents.

**Sources digested:** `docs/LEC_NOTES_DIGEST.md` (8 lecture handouts + tutorials, `lec notes/`),
`docs/GOVERNANCE_SUMMARY.md` (the two official SLIIT PDFs in `governance/`), and the top-level
`CLAUDE.md`. Where this document states a rule, the detailed source section is linked so you can
verify it rather than trust this summary blindly (per Rule 3 below, applied to itself).

---

## 1. Assessment structure — what is actually graded (CMM708 / Handout 1)

- **Individual (75%):** Research Proposal (60%) + 3 quizzes (5% each = 15%).
- **Group (25%):** Poster Presentation on a research paper.
- **4 Module Learning Outcomes:** (1) undertake a literature search; (2) participate within a
  professional, legal, ethical framework; (3) plan independent research using appropriate
  software tools; (4) critically appraise research evaluation methodologies.
- **Workload:** 36 contact hours + 114 non-contact hours = 150 total (part-time).
- This is distinct from the **Faculty-level IT specialization checklist** (TAF, PP1, PP2, Final
  Evaluation, Thesis, Logbook) in §7 below — the module grades the proposal-writing skill itself;
  the faculty checklist grades the actual FYP deliverables.

## 2. Research fundamentals — definitions that get tested and that anchor scope decisions

- **Research** is systematic, creative investigation to establish facts/principles or create/apply
  knowledge — not pure logic; requires imagination and tolerance for uncertainty.
- **Methodology ≠ Method.** Method = the specific technique (e.g. ST-GNN training, an experiment).
  Methodology = the overall, justified strategy for how you know your conclusions are valid. Every
  Module 4 methods choice (why ST-GNN, why this baseline, why this validation split) must be
  traceable to a stated methodology, not just asserted.
- **Research Question vs Hypothesis:** a question is open-ended and comes first; a hypothesis is a
  closed, testable prediction. Good research questions are Feasible, Clear, Significant, Ethical.
- **Aim vs Objective:** aim = broad intent; objectives = specific, measurable actions achieving it.
  Use **SMART** objectives (Specific, Measurable, Achievable, Relevant, Time-based). Use strong
  verbs (construct, develop, evaluate) — avoid weak verbs (understand, appreciate, know).
- **Scope discipline:** define an explicit "effort budget" before starting work — don't begin
  implementation without a clear idea of what's being accomplished and why. This is the same
  discipline `CLAUDE.md` applies when it says Module 4 must not be re-architected around
  Modules 1–3's unreliable outputs — scope creep through "nice to have" integration is exactly the
  failure mode this principle guards against.

## 3. Research gap — the exact taxonomy to use, and how to justify one

Use this course's specific 5-type taxonomy when writing or defending Module 4's gap — do not
invent other gap-type language:

1. **Theoretical Gap** — no theory explains a phenomenon, or theory conflicts with evidence.
2. **Empirical Gap** — insufficient/inconclusive data on the topic.
3. **Methodological Gap** — no adequate method/technique exists yet to answer the question.
4. **Practical Gap** — findings exist but aren't practically implemented (cost/political/social).
5. **Knowledge Gap** — an emerging area or a different context/population not yet studied.

**Process (7 steps, iterative, not linear):** review literature → identify a specific
problem/question → analyze existing research for unstudied areas/inconsistencies → brainstorm →
consult experts to validate → refine the question/hypothesis → write the proposal.

**Rule:** the gap must be *derived from and justified by* the literature review — never asserted
independently of it. This is also a formal supervisor checkpoint (§7, item 1).

## 4. Literature review rules

- **Purpose is critique, not description.** A lit review analyzes strengths/weaknesses, links
  gaps to your research questions, and evaluates — it is not a chronological list of summaries.
- **Source hierarchy — search "working backwards":** Tertiary (definitions/background) →
  Secondary (reviews, methodologies used) → Primary (original peer-reviewed evidence, used as the
  actual evidentiary basis for claims).
- **Credibility checklist for every source:** Currency (recent enough?), Coverage/Relevance,
  Authority (author credentials, h-index), Accuracy (are claims independently verifiable?),
  Objectivity (author motive/bias). This is the operational meaning behind `CLAUDE.md` Rule 4
  (papers ≤5 years old unless foundational).
- **Predatory/blacklisted source check — mandatory before citing anything unfamiliar:**
  - Beall's List (beallslist.net)
  - Web of Science / Clarivate Master Journal List (mjl.clarivate.com)
  - Scopus indexing via Scimago
  - Retraction Watch (retractionwatch.com)
  - This is the mechanical check behind `CLAUDE.md` Rule 3's warning about the "Sajana batch" of
    fabricated/mismatched citations in `docs/SOURCES_LOG.md` — run this checklist on every new
    citation before it's logged, not just on citations that look suspicious.
- **Search techniques:** Pearl growing/snowballing (follow a good paper's references, and its
  references' references), forward search (Google Scholar "cited by"), backward search (follow a
  paper's own reference list).
- **Word-count benchmark taught in the course:** a full literature review is typically
  6,000–12,000 words (annotated bibliography entries ~150 words each) — check the actual TAF/RP
  guideline word count for this cohort's mandated figure rather than assuming this number applies
  verbatim.
- **Never cite wikis or blogs in the reference list** of an academic thesis.
- **Individual peer review before group review** (Tutorial 3 rule): when reviewing a draft
  literature review or proposal section, each member reviews individually first — do not go
  straight to a group review session, since that collapses independent critical perspectives into
  one groupthink pass before anyone has actually caught the issues alone.

## 5. Academic writing style — the standard every deliverable is held to

Four features, all required simultaneously:

1. **Objectivity** — no personal pronouns (I/you/we); passive voice or the topic itself as
   subject.
2. **Formality** — no contractions/colloquialisms, no rhetorical questions, no vague categories
   ("things," "stuff").
3. **Precision** — specific numbers/dates; no vague quantifiers ("a lot," "very"); no
   imprecise/phrasal verbs (do, get, find out) — use precise single verbs instead.
4. **Hedging** — qualify claims with quantifiers/modal verbs (some, may, could) — avoid both
   overconfidence and over-caution. This directly operationalizes the project's standing rule to
   never paper over a real limitation with false confidence.

Same rigor is expected in every audience-facing document — examiner-facing and peer-facing writing
differ in tone, not in rigor.

## 6. Ethics — frameworks to apply, and when they gate Module 4 work

- **Belmont Report's 3 principles** (also the base of the AI-ethics extension used for anything
  ML-related in Module 4): **Respect for Persons** (informed consent, privacy), **Beneficence**
  (maximize benefit/minimize harm — for Module 4, includes guarding against biased/misleading
  crowd-forecast outputs that could misdirect visitors or park management), **Justice** (fair
  distribution of who benefits/bears burden of the system's recommendations).
- **Nuremberg Code** — foundational reference for human-subject research if Module 4 or any
  cross-module work ever collects data from real hikers (surveys, interviews): informed consent is
  essential, no unnecessary risk, right to withdraw at any time.
- **Additional named ethics-framework references** (from Tutorial 5, not detailed in the main
  digest but citable as further reading): APA's "Five principles for research ethics" (apa.org)
  and the Australian Code for the Responsible Conduct of Research (NHMRC 2018) — both sit
  alongside Belmont/Nuremberg as recognized ethics frameworks, not replacements for them.
- **Research misconduct (FFP):** Fabrication, Falsification, Plagiarism — explicitly does NOT
  include honest error or differences of opinion, but does bind every dataset/statistic claim
  this project makes (ties directly to `CLAUDE.md` Rule 3).
- **When Module 4 needs formal ethical clearance:** any human-subject data collection (visitor
  surveys, park-operator interviews used to validate carrying-capacity assumptions) requires
  Ethics Review Committee sign-off before data collection starts — informed consent,
  confidentiality, and right-to-withdraw must be built into the study design, not added after.
- **DECIDE framework**, if any usability/user study work touches Module 4's dashboard: Determine
  goals → Explore questions → Choose evaluation paradigm → Identify practical issues → Decide on
  ethical handling → Evaluate/interpret/present.

## 7. SLIIT Faculty of Computing gates — apply before any scope pivot

**Topic-approval checklist** (supervisor must confirm all ten before any scope, including a v6-style
pivot, is treated as approved — full detail in `docs/GOVERNANCE_SUMMARY.md` §1):
research gap, subject-area fit, impact/policy relevance (SDG alignment), data availability
verified in advance, theoretical grounding, methodology distinguished from system-development
method, personal motivation, appropriately scoped title, identified real-world stakeholders,
stated expected outputs.

**Project-level facts to keep consistent:**
- Research group: **AIMS** cluster.
- SDG claims: **15** (Life on Land), **12** (Responsible Consumption/Production), **3** (Good
  Health and Well-being) — any new claim must trace to one of these three or the SDG list needs a
  formal supervisor revision.
- All **5 RP Learning Outcomes** are mandatory, including LO5 (commercial viability assessment) —
  easy to under-weight since it's not a technical requirement, but it is graded.
- **The git repository itself is a graded deliverable** (PP1 status doc: README with overview,
  architecture diagram, dependencies, real commit/branch/merge history) — this is why `CLAUDE.md`
  Rule 2 (never commit, only stage) exists: the human team must be the one producing that commit
  history, not Claude on their behalf.

## 8. Referencing mechanics

- **Harvard style** is taught in the greatest depth (author-year in-text, alphabetical reference
  list) — but **IEEE** is also explicitly named as acceptable ("IEEE/Harvard Ref Style," Tutorial
  2). Confirm which one the department mandates for the actual thesis submission before assuming
  Harvard by default; don't mix styles within one deliverable once chosen.
- **Zotero** is the primary reference-management tool taught (Word/Google Docs/Overleaf
  integration, PDF annotation, switchable citation styles). Mendeley/EndNote are named alternatives.
- No mandated Turnitin similarity-percentage threshold appears anywhere in the module content —
  that number, if it exists for this cohort, lives only in the SLIIT-specific guideline PDFs.

## 9. Evaluation/validation — how Module 4's ST-GNN work must be validated when it gets there

- Evaluation criteria must be **chosen up front** (accuracy, efficiency, coverage, etc.) and any
  comparison baseline must **already have been discussed in the literature review** — introducing
  a new baseline for the first time in the results chapter is not allowed.
- **ML-specific validation menu:** cross-validation, standard metrics (accuracy, precision,
  recall/sensitivity, specificity, AUC-ROC for classification; MAE/RMSE for regression forecasts —
  directly relevant to ST-GNN crowd-forecasting output), robustness/adversarial testing, bias
  testing across visitor/seasonal subgroups.
- **Good research/experiment principle, repeated emphasis in the course:** work must be
  replicable, reproducible, transparent, and comparisons must be fair.
- Results-writing rule: be concise, include only what answers the actual research questions
  (move extras to appendix), move broad → granular.

## 10. Quick decision guide

| If you're about to... | Apply |
|---|---|
| Add a new integration between Module 4 and Module 1/2/3 | Keep it explicitly optional/future-work per `CLAUDE.md`; check it doesn't violate the "loosely coupled peers" architecture that passed topic approval (§7) |
| Cite a new paper/dataset | Run the predatory-source checklist (§4) + log in `docs/SOURCES_LOG.md` with justification (`CLAUDE.md` Rule 3) |
| Write a claim about a gap, limitation, or result | Use the 5-gap taxonomy (§3) if it's a gap claim; hedge per §5; never smooth over a real limitation with false confidence |
| Plan a validation/evaluation experiment for Module 4 | §9 — baseline must already be in the lit review, choose metrics up front |
| Touch anything involving real hiker/park-operator data | §6 — check whether Ethics Review clearance is needed before collecting it |
| Draft or revise the proposal/thesis structure | §7 for the mandatory checklist items; `docs/LEC_NOTES_DIGEST.md` §7 for the generic chapter template, cross-checked against the SLIIT guideline PDFs for the exact mandated version |

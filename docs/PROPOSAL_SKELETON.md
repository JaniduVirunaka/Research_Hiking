# Proposal Skeleton — J26-IT-363

Section-by-section outline for the full Research Proposal deliverable (the checkpoint after the
already-accepted TAF v5 and the already-submitted Charter). This is a **skeleton**, not content —
it maps what each section must contain, where the content already exists, what's missing, and
what pattern each section follows, so the actual writing pass has a clear target.

**Structure rationale (researched and logged 2026-08-28, see `docs/SOURCES_LOG.md`):** confirmed
against SLIIT's own generic proposal template (`docs/LEC_NOTES_DIGEST.md` §7) and against two
independent external precedents for multi-component proposals — the Horizon Europe work-package
convention and the "umbrella protocol" convention from research governance — both of which
converge on the same shape: **one shared front (problem/objectives/lit-review), one Methodology
chapter with a full, self-contained subsection per module, one shared plan-of-work/ethics/
conclusion.** This validates the structure `docs/PROJECT_PROPOSAL.md` already mostly uses — the
skeleton below formalizes it and fills the gaps, it does not propose a rewrite. Explicitly
avoided: (a) four disconnected mini-proposals stapled together, (b) one fused narrative that
hides Module 4's own methodology inside a single shared "system" description (a real risk per
`CLAUDE.md`'s warning against flattening the four loosely-coupled modules into one system).

Owner note: Module 4 sections are marked **[M4 — your section]**; the other three are context —
per `CLAUDE.md` "Whose seat this is," don't build against their internals, just keep them
coherent enough for the shared narrative.

---

## Front Matter

| Section | Status | Notes |
|---|---|---|
| Title Page | **Missing** | Project ID J26-IT-363, title (v5 wording), team names/IDs, supervisor/co-supervisor, date |
| Abstract (~150–200 words) | **Missing — write LAST** | Per `docs/LEC_NOTES_DIGEST.md`: covers Introduction, Problem, Background, Research Questions, Methodology, Key Findings (N/A at proposal stage — use "expected outcomes" instead), Conclusions |
| Table of Contents | **Missing** | Auto-generated once structure is final — don't hand-number |
| List of Figures / Tables | **Missing** | Populate once diagrams (architecture diagram, Module 4's trail-graph diagram, etc.) are placed |
| List of Acronyms | **Missing** | IMU, RAG, ST-GNN, ECC, PCC, RCC, GCN, LSTM, DEM, TWI, OSM, DWC, SLTDA, etc. — pull from existing docs as written |

---

## 1. Introduction

Maps to existing `docs/PROJECT_PROPOSAL.md` §0–§1 (already drafted, verified, word-count checked
in `docs/TAF_CONTENT.md`).

- **1.1 Motivation / Rationale** — existing §1 "Background and Motivation." Ready, reuse as-is.
- **1.2 Problem Statement** — existing §2 "Research Problem, Gap, and Question." Ready.
- **1.3 Significance / Potential Contribution** — partially covered in §0 "In Plain Terms" and §3
  "Objectives." **Gap:** not yet framed explicitly against the "Significance of the Study"
  assessment factors from `docs/LEC_NOTES_DIGEST.md` §4 (originality, practical relevance,
  theoretical contribution, methodological rigor, social/cultural impact) — worth an explicit
  pass mapping each factor to a concrete claim, one sentence each.
- **1.4 Aims and Objectives** — existing §3 "Research Objectives and the Gaps They Close." **Gap:**
  not yet explicitly labelled with the SMART framework or the Aim-vs-Objective distinction taught
  in `docs/LEC_NOTES_DIGEST.md` §3. Each module's sub-objective (§3 table) should be checked
  against the "strong verbs" list (collect, construct, classify, develop, devise, measure,
  produce, revise, select, synthesize) — a quick scan shows most already qualify (e.g. Module 4:
  "Build," "Model," "Train," "Validate"); worth a final verb-choice pass rather than a rewrite.
- **1.5 Research Questions** — existing §2.2–§2.3 (main question + one sub-question per member).
  Ready. **[M4 — your section]** Module 4's sub-question (§2.3) is already framed as
  independently answerable, consistent with the loose-coupling requirement.
- **1.6 Scope** — partially covered per-module in existing §5 (each module has an explicit
  MVP/Stretch/Out-of-scope split). **Gap:** no single consolidated "Scope of the Research"
  statement at the whole-project level (the "effort budget" framing from
  `docs/LEC_NOTES_DIGEST.md` §7 — what's deliberately NOT being attempted, stated once, up front).
- **1.7 Report Structure** — **Missing.** One paragraph, written last, once the final structure is
  locked.

---

## 2. Background / Literature Review

Maps to existing `docs/PROJECT_PROPOSAL.md` §4, organized as one shared chapter with a
domain-level subsection (§4.1) plus one subsection per module (§4.2–§4.5) — this already matches
the "thematic clustering" convention taught in `docs/LEC_NOTES_DIGEST.md` §5 and the
work-package-style precedent found in this session's research.

- **2.1 Domain background** (Sri Lankan trail tourism, carrying-capacity theory) — existing §4.1.
  Ready.
- **2.2–2.5 Per-module literature** — existing §4.2–§4.5, each ending in an explicit "Gap:"
  statement. This already satisfies the taught 3-part structure (Introduction → thematic Body →
  gap-focused Conclusion) at the *subsection* level. **Gap:** the taught structure also wants an
  explicit **critique**, not just a gap statement — "are there better approaches, has the author
  covered relevant literature, what are strengths/limitations" (`docs/LEC_NOTES_DIGEST.md` §5,
  "Critiquing Literature"). Current §4 sections state gaps well but read as summary-then-gap
  rather than summary-then-critique-then-gap; a light pass adding one critique sentence per
  subsection would strengthen this without a rewrite.
- **2.6 Word count check** — `docs/LEC_NOTES_DIGEST.md` benchmarks a full literature review at
  **6,000–12,000 words**. Current §4 (all five subsections) is well under that — this is the
  single biggest structural gap in the whole document. **[M4 — your section]** §4.5 (Module 4 lit
  review) is the thinnest of the four at present relative to how much verified literature already
  exists for it (11 rows in `docs/REFERENCES_BY_COMPONENT.md` Module 4 table, four more just
  added). Expanding §4.5 into full prose paragraphs per theme (ST-GNN architecture precedent →
  tourism-flow-specific precedent → small/sparse-graph precedent → synthetic-target precedent →
  local carrying-capacity grounding) would both raise the word count and directly support §5.5's
  methodology argument.
- **2.7 Synthesis / taxonomy** — **Missing.** `docs/LEC_NOTES_DIGEST.md` recommends a tabulated
  comparison as a synthesis tool. **[M4 — your section, optional but strong]** A comparison table
  of ST-GNN/GNN-forecasting precedents (architecture, graph size, data type real-vs-synthetic,
  what gap remains) would visually reinforce the §5.5 argument and is a natural way to work in
  the newly-added Gupta et al. 2025 and Zhu et al. 2021 sources.

---

## 3. Methodology

**One chapter, four self-contained module subsections** — the pattern this session's research
explicitly validated (not four separate chapters, not one fused description). Maps to existing
`docs/PROJECT_PROPOSAL.md` §5 (Module 1–4) plus §5.5 (Module 4 extended methodology).

- **3.1 Shared methodology framing** — **Missing, small gap.** One short paragraph explaining
  *why* one Methodology chapter with parallel subsections (rather than one fused system
  description) — i.e. make the "loosely-coupled peers" architectural claim explicit as a
  methodological choice, not just a system-design one. Existing §6 "How the Modules Relate" covers
  the architecture claim but sits *after* Methodology in the current doc order — consider whether
  it reads better moved earlier, right before §5, as the connecting rationale the research
  flagged as the thing that stops multi-module proposals reading as "stapled together."
- **3.2 Module 1 Methodology** — existing §5 Module 1. Ready (context only, not your section).
- **3.3 Module 2 Methodology** — existing §5 Module 2. Ready (context only).
- **3.4 Module 3 Methodology** — existing §5 Module 3. Ready (context only).
- **3.5 Module 4 Methodology** — **[M4 — your section]** existing §5 Module 4 + §5.5 (Extended
  Methodology & Plan of Work, added this session). This is already the most fully developed
  methodology subsection in the document: data/shape/size, architecture, MVP/stretch/out-of-scope,
  the "why GNN, why not circular" argument, and a 7-phase plan of work. **Remaining gap:** the
  newly-found Gupta et al. 2025 ("No One-Model-Fits-All") and Zhu et al. 2021 (synthetic-data GNN
  precedent) sources are logged in `docs/REFERENCES_BY_COMPONENT.md` but not yet woven into §5.5's
  prose — doing so would upgrade the "why this isn't circular" argument from reasoned-from-first-
  principles to literature-grounded, which is a meaningfully stronger proposal claim.
- **3.6 Data collection & ethics summary** — existing §7 "Consolidated Dataset Plan" (table form,
  ready) and §8 "Ethics, Privacy and Risk" (ready, though the Ethics *Form* itself is a separate
  submission per `docs/GOVERNANCE_SUMMARY.md` §5, held pending your template).

---

## 4. Plan of Work

- **4.1 Whole-project timeline** — **Missing.** No document currently has a consolidated,
  cross-module timeline. Per the Horizon Europe work-package precedent found this session, the
  convention is a single table/Gantt with per-module phases mapped to shared milestones (TAF ✓ →
  Charter ✓ → Proposal → PP1/50% → PP2/90% → Final Evaluation → Thesis, per
  `docs/GOVERNANCE_SUMMARY.md` §4). **[M4 — your section]** already has a 7-phase plan
  (§5.5) that could anchor/inform the shared timeline's Module 4 row once real dates exist — the
  phases don't yet have dates, deliberately (see `docs/SOURCES_LOG.md`, dates were left
  unscheduled pending team/Charter input).
- **4.2 Individual member contribution note** — **Missing**, but the ownership table already
  exists in `CLAUDE.md` and the TAF's Objectives table (`taf/TAF-J26-IT-363-v5-ACCEPTED.pdf` §9) —
  reuse, don't redraft.

---

## 5. Conclusion (proposal-level, not final-thesis-level)

- **Missing.** Per `docs/LEC_NOTES_DIGEST.md`'s 4-step process (answer the RQ directly at a
  proposed-approach level, reflect on the planned process, state expected contribution, do NOT
  introduce new data/arguments) — this is a short synthesis pass once §1–§4 are locked, not new
  research. Existing §10 "Corrections carried over from the source-material audit" is useful
  supporting material but is not itself a conclusion — it's closer to an erratum and could move to
  an appendix or stay as an internal note (it's about the *document's* history, not the project's
  contribution).

---

## End Matter

- **References** — existing "Key references" list at the end of `docs/PROJECT_PROPOSAL.md`, plus
  the full per-module tables in `docs/REFERENCES_BY_COMPONENT.md`. **Gap:** citation style not yet
  confirmed — `docs/LEC_NOTES_DIGEST.md` teaches Harvard in depth but says IEEE is also
  acceptable; per `docs/GOVERNANCE_SUMMARY.md` this needs to be settled with the supervisor before
  final formatting, default to Harvard if unconfirmed.
- **Appendices** — not yet needed at proposal stage (source code excluded per taught convention;
  appendices are more a thesis-stage concern).

---

## What's genuinely new work vs. reassembly

Most of this proposal is **already written and verified** — the skeleton above is mostly a gap
list, not a from-scratch outline. The real new-writing items, in rough priority order for a
Module-4-first pass:

1. Front matter (title page, TOC, acronym list — mechanical, low-risk, do anytime)
2. §4.5 literature review expansion to full prose (raises word count, directly strengthens your
   section)
3. §5.5 update weaving in the two new precedent papers (Gupta et al. 2025, Zhu et al. 2021)
4. Optional comparison table (§2.7) for Module 4's literature
5. Whole-project Plan of Work table (needs team input on dates — hold until available)
6. Abstract + Conclusion (write last, once everything else is locked)

Nothing here requires new research beyond what's already sourced and logged — this is a writing
and assembly pass, not another literature search.

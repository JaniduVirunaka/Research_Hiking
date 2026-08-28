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
| Title Page | **DONE (2026-08-29)** | Added to `docs/PROJECT_PROPOSAL.md`. Submission date left blank pending team timeline; flagged to re-confirm the member/module table against TAF v5 before final submission |
| Abstract (~150–200 words) | **DONE (2026-08-29)** | Written last, once §0–§11 were locked, per `docs/LEC_NOTES_DIGEST.md`'s required order; covers motivation, problem, the four-module framework, Module 4's methodology, and expected outcomes (no "key findings" section — correctly using "expected outcomes" since this is proposal-, not results-, stage) |
| Table of Contents | **Placeholder added** | Real TOC still needs auto-generation once structure is final — don't hand-number |
| List of Figures / Tables | **Done, needs figures** | Existing tables listed; diagram entries (architecture diagram, Module 4's trail-graph diagram) still pending — none exist yet in `diagrams/` for this document |
| List of Acronyms | **DONE (2026-08-29)** | Full alphabetical list added, cross-checked against every acronym actually used in the current document text |

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
  **6,000–12,000 words**. Current §4 (all five subsections) is well under that overall — this
  remains the single biggest structural gap in the whole document (M1–M3 subsections are still
  short). **[M4 — your section] DONE (2026-08-29):** §4.5 has been expanded into five full prose
  paragraphs (ST-GNN architecture precedent → tourism-flow-specific precedent → small/sparse-graph
  precedent → synthetic-target precedent → local carrying-capacity grounding), each ending in an
  explicit critique sentence, drawing on 9 newly-verified sources (see
  `docs/SOURCES_LOG.md` 2026-08-29 entry and `docs/REFERENCES_BY_COMPONENT.md` Module 4 table).
  This also closed two standing gaps: the previously-unsourced "Limits of Acceptable Change"
  framing now has a real foundational citation (Stankey et al. 1985) plus a modern application
  (Dragovich & Bajpai 2022), and the dead RG 392533688 citation has been replaced with a verified
  Sri Lanka-specific source (Hewapathirana 2023/2025). §5.5 was also updated to weave in the two
  previously-logged-but-unused precedent papers (Gupta et al. 2025, Zhu et al. 2021) plus the new
  Zhang et al. 2025 and Gayathri et al. 2025 findings. M1–M3 lit-review subsections have not been
  touched — they remain in scope for whoever owns that pass, per "context, not your section."
- **2.7 Synthesis / taxonomy** — **DONE (2026-08-29).** Added §4.5.1 to
  `docs/PROJECT_PROPOSAL.md`: a 17-row comparison table of every ST-GNN/flow-forecasting precedent
  from §4.5 (domain, graph size, real-vs-synthetic ground truth, whether it tests a non-graph
  baseline) plus a final row placing Module 4 itself on the same axes. The table's punchline —
  only 2 of 17 precedents actually test graph structure against a non-graph baseline, and neither
  in a small offline wilderness setting — is stated explicitly as the gap Module 4 fills.

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
  Methodology & Plan of Work). This is already the most fully developed methodology subsection in
  the document: data/shape/size, architecture, MVP/stretch/out-of-scope, the "why GNN, why not
  circular" argument, and a 7-phase plan of work. **DONE (2026-08-29):** Gupta et al. 2025, Zhang
  et al. 2025, Zhu et al. 2021, and Gayathri et al. 2025 are now woven directly into §5.5's
  baseline-justification and synthetic-target paragraphs, plus a new paragraph grounding the
  dynamic-ECC-over-static-quota argument in the Limits of Acceptable Change framework (Stankey et
  al. 1985 + Dragovich & Bajpai 2022) — upgrading that argument from reasoned-from-first-principles
  to literature-grounded throughout.
- **3.6 Data collection & ethics summary** — existing §7 "Consolidated Dataset Plan" (table form,
  ready) and §8 "Ethics, Privacy and Risk" (ready, though the Ethics *Form* itself is a separate
  submission per `docs/GOVERNANCE_SUMMARY.md` §5, held pending your template).

---

## 4. Plan of Work

- **4.1 Whole-project timeline** — **DONE (2026-08-29), dates still TBD.** Added
  `docs/PROJECT_PROPOSAL.md` §10: a shared-milestones table (TAF ✓, Charter ✓, Proposal in
  progress, PP1/PP2/Final/Thesis all "not started — date TBD") plus a coarse three-window
  per-module phase-mapping table (Proposal→PP1 / PP1→PP2 / PP2→Final) that reuses Module 4's
  existing §5.5 7-phase plan rather than restating it. Dates are deliberately left blank — no
  team/supervisor date exists for PP1 onward as of 2026-08-29 — with an explicit note to replace
  the three coarse windows with a real Gantt-style view (per the Horizon Europe precedent) once
  dates are confirmed, not before.
- **4.2 Individual member contribution note** — **DONE (2026-08-29).** §10 explicitly points back
  to the Title Page's ownership table and `CLAUDE.md` rather than redrafting it, and states the
  no-cross-blocking claim (each member's deliverable is independent of the others').

---

## 5. Conclusion (proposal-level, not final-thesis-level)

- **DONE (2026-08-29).** Added `docs/PROJECT_PROPOSAL.md` §"Conclusion", placed after the new §10
  Plan of Work and before the renumbered §11 "Corrections" section (which stays as an internal
  erratum, not moved — it's about the document's history, not the project's contribution, exactly
  as flagged here previously). Follows `docs/LEC_NOTES_DIGEST.md`'s 4-step process: answers the
  main RQ at a proposed-approach level, reflects on the research process (the deliberate
  baseline-testing and synthetic-target-honesty discipline running through §4.5/§5.5), states
  narrow recommendations (confirm PP1/PP2 dates, start field calibration early, revisit M1–M3
  lit-review depth), and states the expected contribution without introducing any new data or
  citation not already established earlier in the document.

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

1. ~~§4.5 literature review expansion~~ / ~~§5.5 precedent weave-in~~ / ~~§2.7 comparison table~~ /
   ~~front matter~~ / ~~whole-project Plan of Work skeleton~~ — **all done 2026-08-29** (see
   `docs/SOURCES_LOG.md`). Explicitly deprioritized per team decision: M1–M3 literature-review
   subsections (§4.2–§4.4, now comparatively the thinnest in the document) — out of Module-4 scope,
   not being picked up in this pass.
2. ~~Abstract~~ / ~~Conclusion~~ — **done 2026-08-29**, written last once §0–§11 were locked, per
   `docs/SOURCES_LOG.md`. Remaining open item: fill in real PP1/PP2/Final/Thesis dates in §10 once
   the team/supervisor sets them, and upgrade the coarse 3-window per-module table to a real
   Gantt-style view at that point. This is the only substantive gap left that isn't out-of-scope
   for Module 4 (M1–M3 lit-review depth remains open but is explicitly not being picked up here).

Nothing here requires new research beyond what's already sourced and logged — this is a writing
and assembly pass, not another literature search.

# Project: J26-IT-363 — Sustainable Hiking Tourism Edge-AI Framework

SLIIT Faculty of Computing, **IT4010 Research Project**, 2026 July intake. AIMS research group
(Autonomous Intelligent Machines and Systems). Four-member final-year Information Technology
group project. Supervisor: Dr. Prasanna Sumathipala. Co-supervisor: Ms. Thisara Shyamalee.

## What this project is

**Canonical, panel-accepted topic (TAF v5, accepted 2026-07-07):**
*"A Decentralized, Edge-Native AI Framework for Sustainable Hiking Tourism in Sri Lanka"*

Four independent, hardware-free, offline-first smartphone AI modules supporting sustainable
management of Sri Lanka's Pekoe Trail and Horton Plains National Park:

| # | Module | Owner (Reg. No / Name) |
|---|---|---|
| 1 | Terrain & Effort Profiling (IMU terrain classification + route-energetics fatigue gauge) | IT23389656 — Ahamed M.N.I |
| 2 | Trail Degradation & Litter Vision (on-device YOLOv8-seg) | IT23386372 — Kankanige S.S |
| 3 | Offline Hiker Information Assistant (on-device RAG) | IT23394506 — Ahamed M.M |
| 4 | Crowd & Carrying-Capacity Forecasting (ST-GNN, fully standalone) | IT23343948 — Weerasekara J.V |

The four modules are **peers, loosely coupled** — none depends on another to function. A shared
dashboard may display all four; that dashboard is not itself a required deliverable.

## Whose seat this is

**This working directory is being driven from Module 4's seat: IT23343948 — Weerasekara J.V,
Crowd & Carrying-Capacity Forecasting (ST-GNN).** Default to treating Module 4 as the primary
focus of any work here unless told otherwise.

The other three modules (1, 2, 3) are **context, not dependencies** — read about them to
understand the overall framework, integration points, and shared dashboard story, but:
- **Do not assume their outputs, formats, timelines, or even final scope are reliable.** The
  proposal's "loosely coupled peers" architecture is a deliberate hedge against exactly this —
  Module 4 is specified to run on its own independent inputs (OSM graph, DEM/terrain, weather,
  historical/seasonal visitation) and must **not** be re-architected to require Module 1/2/3
  output as a hard input. If a "nice to have" integration is ever discussed (e.g. Module 1/2
  field signals enriching Module 4's correction factors), keep it explicitly optional/future-work,
  never load-bearing for Module 4's own MVP or evaluation.
- When asked to "consider the other modules," the right level of engagement is: understand their
  stated scope well enough to keep the shared dashboard/narrative and any cross-module thesis
  chapters coherent, not to build against their internals.

**⚠️ Open pivot risk — read before acting on module scope.** A newer, unreviewed draft (TAF v6,
`taf/TAF-J26-IT-363-v6-DRAFT.pdf`) reframes the same four modules around heavy, largely unproven
mathematical machinery (Physics-Informed Neural Networks, Unsupervised Domain Adaptation,
Mixed-Integer Linear Programming, a custom "Dynamic Inference Power Manager", "EdgeRAG").
**This draft has not been through the topic screening panel and has not been confirmed as the
team's actual direction.** Treat **v5 as the source of truth** for scope, novelty claims, and
feasibility unless the team explicitly confirms in conversation that they have adopted v6.
`docs/PROJECT_PROPOSAL.md` and `docs/TECHNICAL_AUDIT.md` are written against v5 and already flag
why an over-mathematicized rewrite is a scope-risk, not a strict improvement — see
`docs/TECHNICAL_AUDIT.md` before endorsing any v6-style addition (PINN, MILP, UDA, etc.) to a
module's scope.

## Folder map

- `docs/` — living project documentation (proposal, references, audits, presentation script, TAF
  prose, lecture-notes digest, governance summary, source ledger). Read these first.
- `taf/` — official Topic Assessment Form. `TAF-J26-IT-363-v5-ACCEPTED.*` is the panel-signed
  version. `TAF-J26-IT-363-v6-DRAFT.*` is the unreviewed pivot draft (see warning above).
  `taf/archive/` holds superseded v1–v4 drafts, kept for history only — do not cite or build from
  them.
- `governance/` — the two official SLIIT Faculty of Computing PDFs this project must comply with
  (TAF supervisor guidelines, undergraduate RP guidelines). `docs/GOVERNANCE_SUMMARY.md` is the
  condensed, agent-usable version — read that first and only open the PDFs for verbatim wording.
- `research/` — the literature-tracking spreadsheet (`Research Topics.xlsx`), the raw Gemini
  Deep Research chat exports that originated the project idea, and the reference GPX trail file.
- `diagrams/` — conceptual/architecture diagrams (HTML, drawio XML, PNG renders).
- `misc/` — anything that doesn't fit elsewhere (e.g. `SLIIT.one` personal OneNote export).
- `.claude/agents/` — the specialised subagents for this project (see below).

## Hard rules (apply to every agent and every session on this project)

1. **Minimize token usage.** Prefer reading `docs/*.md` digests over re-reading source PDFs.
   Never re-read a PDF that already has a digest in `docs/` unless verifying an exact quote/figure.
   Delegate large-document ingestion (>50 pages) to a background subagent that writes a condensed
   digest rather than reading it inline.
2. **Never commit. Stage only.** `git add` is fine; `git commit` is never allowed, under any
   phrasing of the request, without the user explicitly typing an instruction to commit in that
   exact session. Do not commit "on their behalf" even if asked to "save progress" or "finish up"
   — stage and stop.
3. **Every finding, decision, or pivot needs a source and justification.** No claim about a
   dataset, paper, statistic, or technical feasibility claim goes into any deliverable without a
   verifiable citation (link/DOI resolved, not just a plausible-looking title) and a one-line
   justification of why it supports the claim. Log it in `docs/SOURCES_LOG.md`. See
   `docs/SOURCES_LOG.md`'s "Sajana batch" entry for what fabricated/mismatched citations look
   like in this project's history — 9 of 10 entries in that batch were invented or mismatched
   DOIs; treat it as the cautionary example and re-verify anything similar from scratch.
4. **Research papers must be from the last 5 years** (2021-08-28 or later, relative to today's
   date) **unless** the paper is a foundational/classical reference that is being cited for a
   named method or formula (e.g. Cifuentes 1992 carrying-capacity cascade, Naismith's rule 1892,
   Tobler's hiking function 1993, Minetti et al. 2002, Lewis et al. 2020 RAG, Reimers & Gurevych
   2019 Sentence-BERT). Foundational citations must be explicitly labelled as such wherever used,
   not presented as recent literature.

## Working conventions

- This is a Windows machine; use the Bash tool's POSIX paths or PowerShell as appropriate.
- There is a git repository at the project root (initialized fresh; nothing committed by policy —
  see rule 2). Check `git status` before any destructive operation.
- When in doubt about which module a piece of work belongs to, check the owner table above — stay
  in that member's scope unless asked to work across modules.

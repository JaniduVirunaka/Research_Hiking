# Governance Summary — SLIIT Faculty of Computing Rules for This Project

Condensed from the two official PDFs in `governance/`. This file is the one to read day-to-day;
open the source PDFs only when you need verbatim wording for a submission.

**Source note:** digested from `governance/FoC Guidelines - TAF Guidelines.pdf` (2 pages) and
`governance/Guidelines for Undergraduate RP 2024 Oct.pdf` (v2, published October 2024, 10 pages)
on 2026-08-28.

---

## 1. Topic-approval checklist (from "Guidelines for Supervisors on Research Topic Assessment")

Before a topic (or any pivot to a topic, e.g. the v6 draft) can be considered approved, it must
satisfy all ten of these — the supervisor is required to check each one:

1. **Research gap** — a clearly identified, literature-backed gap, not just an application idea.
2. **Subject-area focus** — must align with the student's specialization (IT, for this team).
3. **Impact & policy relevance** — real local/international impact; SDG alignment is the
   explicit example given.
4. **Data availability** — feasibility of data collection must be checked before the topic is
   picked, not discovered mid-project. Secondary data sources must be verified for accessibility,
   reliability, and completeness.
5. **Theoretical background** — clear grounding in established theory/concepts in the area.
6. **Methodology** — the *research* methodology (quantitative/qualitative/experimental/case
   study/action research/etc.) must be distinguished from the *system development* methodology.
7. **Personal interest/motivation** — supervisors are expected to ask why the topic was chosen.
8. **Scope** — not too broad (unfocused) or too narrow (nothing to find); scope must show clearly
   in the title.
9. **Stakeholders** — real-world stakeholders must be identified, ideally with actual
   collaboration sought (for this project: DWC, SLTDA, trail/park operators).
10. **Expected outputs/outcomes** — the topic should state what kind of output results
    (framework, model, new method, tool, dataset, etc.), beyond just "thesis + demo".

**Use this list as the guardrail-agent's checklist** whenever reviewing a proposed scope change.

---

## 2. Project alignment (Part 1 of the RP Guidelines)

- **Research group:** must align with one FoC research cluster. This project is **AIMS**
  (Autonomous Intelligent Machines and Systems) — robotics, embedded/smart systems, IoT, sensor
  networks, real-time operations. *(Note: this project's "no IoT hardware" constraint is a
  deliberate scoping choice, not a conflict with the AIMS cluster — AIMS covers the broader
  autonomous-systems space.)*
- **SDG alignment required.** This project claims **SDG 15** (Life on Land — ecosystem/trail
  damage), **SDG 12** (Responsible Consumption and Production — fair/lower-impact tourism), and
  **SDG 3** (Good Health and Well-being — hiker safety). Any new claim or module must be traceable
  to at least one of these three, or the SDG list must be formally revised with the supervisor.
- **Industry vertical:** Hospitality & Tourism (primary), Environment and Climate (secondary).

## 3. Specialization requirements (Part 2)

- **RP (IT4010) Learning Outcomes — all five are mandatory**, not optional:
  - LO1: creative/innovative solution to an open-ended, complex problem.
  - LO2: apply key pillars of the computing domain.
  - LO3: apply project-management methodology under ethical/security/social/legal/professional
    constraints.
  - LO4: communicate effectively to technical **and non-technical** audiences.
  - LO5: assess the **commercial viability** of the project.
- **Program-specific research areas (IT):** ML, DL, Software Engineering, Mobile Applications,
  HCI, Image Processing, NLP, Algorithms, OS, Cloud Computing, IoT, Database Systems, e-learning.
  Every module's core technique should map to at least one of these.

## 4. Mandatory IT-specialization submission checklist

Per the "Summary of Specialization RP Checklists" table (IT column):

| Checkpoint | Deliverable | When | Where |
|---|---|---|---|
| TAF | Topic Assessment Form | — | (already accepted, v5) |
| Charter | Project charter + **Use of AI Policy: Student Declaration and Agreement** | 2026-08-01 | (already submitted — see `governance/Project Charter.pdf`; signed by all 4 members + Dr. Prasanna Sumathipala) |
| Proposal | + Ethics Form (common to all specializations) | — | — |
| PP1 (50%) | Status Doc 1 = **Git Repository** (with README: overview, architecture diagram, dependencies; full commit/branch/merge history) | PP1 | OneDrive "CheckList1" folder, shareable git link |
| PP2 (90%) | Status Doc 2 = **Evidence of using a PM tool** (MS Planner export) | PP2 | OneDrive "CheckList2" folder |
| Final Evaluation | Demo, Presentation, Viva | — | — |
| Thesis Submission | — | — | — |
| Logbook | **Reflective Statement** (common to all specializations) | — | — |

**Implication for this repo:** the git repository itself is a graded IT-specialization deliverable
— it needs a README with an overview, an architecture diagram, and dependency list, and a real
commit/branch/merge history. Rule 2 in the top-level `CLAUDE.md` ("never commit, only stage")
means Claude Code must never be the one to create that history — the human team members commit;
Claude prepares and stages.

## 5. Ethics

- An **Ethics Form** is a common mandatory submission for every specialization, filed at proposal
  stage. This project needs it because: (a) IMU motion data is arguably biometric/movement data
  about identifiable individuals, (b) Module 2's camera capture may incidentally capture people,
  (c) Module 3's knowledge base includes operator/pricing information that must avoid defamation.
- Privacy-by-design (on-device processing, only derived KB-scale results synced, informed consent
  at data-collection onboarding) is the documented mitigation strategy — see
  `docs/PROJECT_PROPOSAL.md` §8.

## 6. Use of AI Policy — binding on every session in this repo

**Source:** `governance/Project Charter.pdf` — "Use of AI Policy: Student Declaration and
Agreement," submitted with the Project Charter and signed by all four members and the supervisor
(Dr. Prasanna Sumathipala) on 2026-08-01.

Each member individually declared, in writing:

1. They have read and understood the AI Usage Policy for the Research Project (IT4010).
2. **AI tools are to be used only as support tools, not as substitutes for their own
   understanding and work.**
3. AI tools will be used responsibly, ethically, and transparently.
4. **Any use of AI tools will be clearly disclosed.**
5. **The student bears full responsibility and accountability for any content, code, model, or
   output generated using AI tools** — Claude's output is not a shield from that accountability.
6. **The student confirms they will be able to explain, justify, and defend all aspects of their
   work during evaluations** — including anything Claude produced or helped produce.
7. Failure to comply may result in **academic penalties**.

**What this means in practice for Claude Code working in this repo:**
- Never present AI-authored content as if it were independently produced by the student without
  the student's own understanding — the point of every agent here is to *support* Weerasekara J.V.
  (Module 4) and the team, not to generate finished work the owning member can't explain.
- When producing a document, code module, or claim, favor leaving clear, explainable reasoning
  (not just a polished final answer) so the responsible student can walk through and defend it —
  this is *why* `docs/SOURCES_LOG.md` requires a justification for every finding, not just a
  citation, and it's the same reason code comments should explain non-obvious WHY, not WHAT.
- AI involvement in a deliverable should be disclosed where the submission process asks for it
  (e.g. if a status report or reflective statement asks about tools used) — do not conceal it.
- Do not fabricate, embellish, or "smooth over" gaps in the student's actual understanding — if
  something in the docs is unverified or a limitation is real (see `docs/TECHNICAL_AUDIT.md`),
  say so plainly rather than presenting a falsely confident final product, since the student is
  the one who must defend it in a viva.

## 7. What is NOT in these two governance PDFs

The 525-page `Combined Lec Notes.pdf` (now digested at `docs/LEC_NOTES_DIGEST.md`) is the deeper
teaching material — literature review method, citation style, statistical/evaluation methodology,
thesis chapter structure. The two PDFs summarized here are the **compliance/checklist** layer;
the lecture notes are the **how-to** layer. Use both.

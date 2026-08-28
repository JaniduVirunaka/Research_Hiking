# Technical Feasibility Audit — J26-IT-363 (CPS-ES)

*Honest engineering review: is this buildable by a 4-member final-year SLIIT team, and what will bite you?*

## Verdict

**Doable — but only if you reframe it and scope each component to a defensible MVP.** As written (taken literally: RT-DETR+DenseNet quantised on-device, ClimateBERT+RAG+knowledge-graph, agent-based modelling, ST-GNN, *and* federated learning, *and* a live fused real-time loop), it is **over-scoped and over-promised**. The four-way split is sound (each component is a legitimate standalone final-year project). The danger is not any single component — it's (a) two genuinely unproven research claims, (b) self-collected data being the real bottleneck, and (c) a "fully integrated live system" story the project cannot actually deliver.

**Traffic-light per component:** C1 🔴 high-risk · C2 🟡 doable with fixes · C3 🟡 partly soft · C4 🟠 the integration/validation trap.

---

## The two systemic problems (read these first)

### 1. "Four independent components" vs "one integrated framework" — you can't fully have both
C4 (ST-GNN) is specified to consume C1's terrain stress, C2's degradation, and C3's operator scores as inputs. But those signals only exist at scale if hundreds of real hikers run your apps on the trail — which **will not happen during a student project**. So in practice C4 will be fed *simulated/placeholder* values for C1–C3. That's fine — but it means the honest claim is **"four independent sub-projects + a proof-of-concept integration demo,"** not "a deployed live cyber-physical-social loop." Promise the former; the panel will respect the honesty and you can't deliver the latter anyway.

### 2. The bottleneck is fieldwork and labelling, not the ML
Every component depends on **data you must collect and hand-label yourselves** (no SL trail IMU set, no ground-level erosion set, no greenwashing labels, no segment-level foot-traffic). The machine learning is the easy 30%. The hard 70% is: getting to Horton Plains/Pekoe (central highlands, hours from SLIIT Malabe), DWC permits + per-person entry (~USD 25), weather windows (mist/monsoon), recruiting hikers, ethics clearance (biometric + filming people), and **hundreds of hours of annotation**. Plan the project around *this* critical path, not around model training.

---

## Component-by-component

### C1 — IMU terrain-from-gait 🔴 (highest research risk)
**The core claim is genuinely unproven.** Separating *terrain effect* from *individual fatigue and gait style* using a **single, unconstrained pocket phone** is hard for reasons that won't go away:
- **Phone-position variance** — pocket vs hand vs backpack changes the signal more than terrain does. Most datasets that work well use *fixed, body-mounted* IMUs. UCI HAR is the only phone set and it's waist-fixed with no terrain labels.
- **Fatigue and rough terrain look alike** in gait (both slow you down and raise variability), so "isolate terrain from fatigue" is circular without strong per-user calibration.
- **Ground-truth is painful** — to train "this is mud/erosion" you need terrain labelled at each moment (synced video + manual labelling outdoors). Labelling *degradation* (not just terrain type) objectively is harder still.
- The Gemini report's "anomaly score `A(x,y)` = deviation from expected fatigue curve" is hand-wavy: it assumes you can model each user's fatigue baseline, which is itself an open problem.

**Realistic MVP:** terrain *type* classification (flat / rocky / muddy / steps / slope) from a **fixed phone position**, plus a coarse fatigue flag. That's well-supported (~80–95% in the literature) and a solid FYP. **Downgrade** "map trail degradation without hardware" → "classify terrain type and flag anomalies/fatigue." Battery/sampling at 50 Hz is fine; the risk is entirely scientific, not computational.

### C2 — Edge computer vision 🟡 (doable; needs two concrete fixes)
- **Litter detection: low risk.** TACO/SortWaste transfer + a small custom set; counting via detection is standard.
- **Fix #1 — drop RT-DETR + DenseNet121; use YOLOv8/v11-seg.** RT-DETR is transformer-heavy with immature mobile export; DenseNet121 *isn't a segmentation architecture* (it's a classifier — needs a U-Net/FPN decoder bolted on). **YOLO-seg does detection + instance segmentation in one model with mature TFLite/NCNN/CoreML export** — it's the pragmatic edge choice and removes a whole class of deployment pain. (Keep RT-DETR only as an accuracy-comparison stretch goal.)
- **Fix #2 — sample frames, don't analyse full video.** Continuous on-device video inference cooks the battery and thermally throttles the phone. Run at 1–2 fps.
- **Degradation segmentation is the hard half.** No public ground-level erosion dataset exists, so you hand-annotate masks. Budget honestly: ~1,800 images × 5–8 min ≈ **150–240 annotation-hours** across the team, and "erosion/braiding" masks are subjective → **inter-annotator agreement will be low** unless you write a strict labelling rubric and measure κ. mAP@50 > 0.80 is realistic for litter, **optimistic** for degradation.

### C3 — NLP greenwashing + ABM 🟡 (partly soft; descope the ambitious bits)

> **UPDATE (superseded):** Module 3 has since been **pivoted to an offline, on-device RAG hiker information assistant** (small LLM + curated knowledge base), which resolves the three concerns below: no subjective greenwashing labels are needed, there is no scraping/ToS problem (the knowledge base is curated from official/open sources), and there is no operator-scoring defamation risk. The verified operator/fair-price information now lives in the assistant's knowledge base. The original critique is kept below for the record.

- **ClimateBERT domain mismatch.** It's trained on *large-firm corporate ESG/climate reports*; SL SME tour-operator copy is short, informal, and code-mixed (Sinhala/Tamil/English). Transfer will be weak without real fine-tuning on your custom set — and **greenwashing has no labelled data**, so you must define and label it (subjective → agreement risk again).
- **Data availability risk.** Many SL operators have thin web presence; gathering enough "green claim" text may be hard, and TripAdvisor/Booking ToS forbid scraping (use the CC-BY SL review set + official APIs; store derived features only).
- **Descope RAG + knowledge-graph fact-checking to a stretch goal** — it needs structured "verified environmental data / DWC certifications" to check claims against, which largely **doesn't exist** in usable form. Core deliverable = a greenwashing-risk classifier + a pricing-complaint detector.
- **ABM is legitimate but un-validatable as "prediction."** You have no SL pricing time-series to validate "predict a 90% local-arrivals decline." Frame the ABM as **scenario simulation** (replicating/extending the cited dual-pricing paper, seeded by your ~50–150 price-audit pairs), not forecasting. Make sure the NLP scores actually feed the ABM so the component is one thing, not two bolted together.

### C4 — ST-GNN dynamic carrying capacity 🟠 (the validation trap)
- **Training on synthetic foot-traffic is partly circular.** You generate the target from seasonality × permit caps × a movement model, then train a model to reproduce it — so it largely learns *your simulator's rules*, not reality (garbage-in/garbage-out risk). A few days of manual calibration counts is thin. **State this limitation explicitly**; it's the thing a sharp panellist will hit hardest.
- **The graph is tiny (25–40 nodes).** GNNs earn their keep on large networks; on a small loop a simpler model (per-node LSTM, or ST-GNN's non-graph baselines) may match it. Be ready to justify "why a GNN" (propagation modelling + methodological novelty) — and *include* those simpler baselines so you can show the GNN actually adds value.
- **ECC has no ground truth.** You compute it from the Cifuentes formula then "predict" it — again partly circular. Position the genuinely useful output as **occupancy/bottleneck forecasting** that drives *dynamic correction factors*; treat ECC as a derived management number, not a validated prediction.
- The OSM graph, DEM/TWI features, and weather feeds are **solid and real** — that part is not a risk.

---

## Other cross-cutting issues

- **Federated Learning is realistically overkill for an undergrad timeline.** Proper FL (frameworks + secure aggregation + differential privacy) is a research project in itself, and you have no real federated user base. The *privacy goal* is fully met by **on-device processing + informed consent + storing only derived KB-scale features**. Keep FL as an explicit **"future work"** line; don't promise to implement it.
- **Skill ramp-up is real:** model quantisation/edge deployment, instance segmentation, GNNs, and ABM are four different non-trivial learning curves. Front-load learning in semester 1.
- **Timeline:** IT4010 spans ~2 semesters. One member per component end-to-end (collect → label → model → evaluate → integrate → thesis) is achievable **only at MVP scope**. The literal full spec is not.
- **Ethics & permits are a milestone, not a footnote** — biometric IMU + filming people needs clearance; DWC needs to approve on-site data collection. Start this in week 1. Consider doing most collection on **accessible proxy trails near Colombo** (e.g. Hanthana, Knuckles foothills) with a few targeted Horton Plains/Pekoe trips, to de-risk the field schedule.

---

## Recommended de-risking moves (priority order)

1. **Reframe the positioning** to "four independent edge-AI sub-projects unified by a *proof-of-concept* carrying-capacity decision layer." Stop promising a live fused system.
2. **C2:** swap RT-DETR + DenseNet121 → **YOLOv8/v11-seg**; sample frames not video.
3. **C1:** narrow to **terrain-type classification + fatigue/anomaly flag** with a known phone position; "degradation mapping" becomes stretch.
4. **C3:** core = greenwashing + pricing classifier; **RAG/KG and ABM-as-prediction → stretch/scenario.**
5. **C4:** publish the **synthetic-data caveat**, include simple baselines vs the GNN, and present **ECC as a derived output**, occupancy-forecasting as the validated result.
6. **Demote Federated Learning to future work**; use privacy-by-design instead.
7. **Make a data-collection + ethics + annotation plan your first deliverable** (proxy trails, rubrics, κ targets, who labels what). This is the real critical path.
8. Add an explicit **MVP-vs-stretch table** per component so the panel sees you know the difference.

## Bottom line
The architecture is coherent and the components are each a valid final-year project — **the science is sound where it's incremental and shaky exactly where the proposal calls it "novel"** (C1 gait-inversion, C4 fused ECC). Build the incremental MVPs solidly, be transparent about the synthetic-data and integration limits, drop the over-reach (RT-DETR, RAG/KG, real FL, live fusion), and this is a strong, deliverable project. Pitch it as more than that and you'll be over-committed by mid-semester.

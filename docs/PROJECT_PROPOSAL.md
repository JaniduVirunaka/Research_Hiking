# Project Proposal — J26-IT-363

## A Decentralised, Edge-Native AI Framework for Sustainable Hiking Tourism in Sri Lanka

*Topic (12 words): "A Decentralised, Edge-Native AI Framework for Sustainable Hiking Tourism in Sri Lanka."* — SLIIT IT4010 Research Project, 2026 July intake. AIMS research group. Four-member final-year IT group.

> **Topic revised** from the originally-submitted "A Cyber-Physical-Social AI Framework for Dynamic Ecotourism Carrying Capacity." The new title reflects the redesign into **four independent edge-AI modules** (terrain/effort, environmental-damage vision, an offline hiker information assistant, crowd/carrying-capacity forecasting) that are loosely coupled rather than fused — so the title is no longer centred on a single "carrying capacity" output or a hard-wired cyber-physical-social pipeline. *(Update the TAF form with your supervisor.)*

> All cited papers in this proposal were link-/title-/content-verified, and all datasets were confirmed to exist with the sizes/licences stated (see `docs/SOURCES_LOG.md` for the fabrication findings and verification method). Fabricated or mis-summarised sources from the original tracking sheet have been removed.

---

## 0. In Plain Terms (non-technical summary)

**The big idea:** four independent smartphone/edge-AI tools that help keep Sri Lankan hiking trails sustainable — each works on its own, *without installing equipment on the mountain and without needing internet up there.*

- **Module 1 — knows the trail underfoot and how hard you're working.** The phone's motion sensors classify *what the ground is like* (flat / rocky / muddy / steps / slope), and your *effort/fatigue* is estimated from how far and how high you've climbed (distance + elevation). → terrain-difficulty tags + a personal "rest / turn back" gauge.
- **Module 2 — spots litter and trail damage.** Satellites can't see under the tree canopy, so the hiker's camera looks at the ground and the phone (offline) recognises *litter* and *trail damage* (erosion, exposed roots, widening paths). → automatic litter counts + a damage map.
- **Module 3 — answers hikers' questions offline.** A small on-device assistant uses a trusted, pre-loaded knowledge base (park rules, safety/first-aid, trail guides, species, and verified operator/fair-price info) to answer questions with no internet. → grounded, source-cited guidance.
- **Module 4 — forecasts crowding and a smart capacity limit (on its own).** Using only the trail map, terrain, weather and past-visitor patterns, it *predicts where and when crowding will hit, hours ahead* and suggests a capacity limit that changes with conditions — instead of a fixed daily ticket cap. → crowd forecast + dynamic capacity recommendation.

**How they relate:** all four are *peers* — each is a complete standalone project owned by one member. A park or hiker app could optionally show them together on one dashboard, but **no module needs another to work.**

---

## 1. Background and Motivation

Sri Lanka's tourism sector is pivoting from coastal/cultural products toward **high-altitude adventure trekking**. The flagship asset is **The Pekoe Trail** — a 300 km, 22-stage long-distance route across the central highlands (Kandy → Nuwara Eliya), EU- and USAID-funded, launched November 2023. Notably, **Pekoe Stage 10 (Dayagama → Horton Plains)** physically connects the trail to **Horton Plains National Park** (3,160 ha; the World's End / Baker's Falls ~9.5 km loop), which makes the two sites a natural joint case study.

Demand is rising sharply: SLTDA recorded **2,362,521 arrivals in 2025 (+15.1%)**, strongly seasonal (Dec–Mar peak, May–Jun lean), and the Pekoe Trail demand study projects **~16,000 dedicated hikers by 2028 and ~35,000 by 2033**. *(A widely-quoted "1.2 million hikers by 2035" figure exists but originates from a paid commercial vendor forecast and should be cited as such, not as an established projection.)*

This growth produces a **two-sided carrying-capacity problem**:

- **Physical/ecological** — overuse drives soil compaction, root exposure, trail braiding/incision and litter. The Horton Plains social-carrying-capacity literature already documents weekend/holiday overcrowding, with visitor-satisfaction peaking below ~10 people per viewpoint.
- **Information & safety** — once mobile signal drops, hikers lose maps, guidance and help in demanding terrain, and have no easy way to check park rules, basic safety steps, or whether operator prices and "eco" claims are fair.

Current management is **static and reactive**: the Department of Wildlife Conservation issues fixed daily online permit quotas that cannot respond to real-time weather, erosion, or where crowds actually cluster. Existing mobile apps are closed-loop navigation aids that consume the environment without measuring it, and existing AI environmental monitoring relies on satellite/UAV imagery that **fails under dense tropical canopy** and on cloud connectivity that **fails in trail dead-zones**.

**Core constraint adopted for this project (per the team's requirement): no IoT hardware.** The framework therefore shifts all sensing and computation onto the *hiker's own smartphone* and decentralised, offline-first software.

---

## 2. Research Problem, Gap, and Question

### 2.1 The gap
There is **no hardware-free, edge-native suite** that, working **offline** in connectivity-deprived terrain, lets the hiker's own phone (a) read the terrain and effort underfoot, (b) capture ground-level evidence of trail damage, and (c) answer the hiker's questions from trusted information, while a fourth tool forecasts crowding for managers. Each ingredient exists in isolation (gait/terrain sensing, litter detection, on-device RAG, spatio-temporal forecasting) but none has been built as an offline, on-phone tool localised to Sri Lankan trail conditions (the "Global South data deficit").

### 2.2 Main research question
> **How can a decentralised, edge-native AI framework dynamically estimate and manage the effective carrying capacity of Sri Lankan hiking trails — fusing smartphone-sensed hiker biomechanics, ground-level environmental computer vision, and socio-economic operator auditing — while operating offline in low-connectivity terrain and without deploying any IoT infrastructure?**

### 2.3 Sub-questions (one per member — each independently answerable)
1. Can a smartphone **classify trail terrain type** from its IMU, and **estimate hiker effort/fatigue from distance + elevation gain** (energy-expenditure models), offline?
2. Can a **quantised, on-device** vision model quantify litter and segment ground-level trail degradation under tropical visual clutter, beating the canopy-occlusion limits of aerial sensing?
3. Can an **on-device retrieval-augmented assistant** give hikers trusted, source-grounded answers (safety, trails, rules, fair pricing) fully offline?
4. Can a **Spatio-Temporal Graph Neural Network**, using only trail-graph + terrain + weather + historical visitation, forecast micro-spatial bottlenecks and recommend a **dynamic carrying capacity** that replaces static quotas — **as a standalone system**?

---

## 3. Research Objectives and the Gaps They Close

**Main objective:** develop and validate a suite of **four independent, hardware-free edge-AI modules** that together support sustainable Sri Lankan trail management — covering terrain/effort sensing, environmental-damage vision, an offline hiker information assistant, and crowd/carrying-capacity forecasting. Each module is a self-contained final-year sub-project; the suite is loosely coupled (a shared dashboard), not a hard-wired pipeline.

| # | Module (member) | Gap it closes |
|---|---|---|
| 1 | **Terrain & Effort Profiling** — IMU terrain-type classification + effort/fatigue from distance & elevation | No offline phone tool classifies tropical-trail terrain *and* estimates hiker effort from route energetics; clinical gait work needs lab/fixed multi-sensors |
| 2 | **Trail Degradation & Litter Vision** — on-device litter detection + degradation segmentation | Environmental CV is aerial (canopy-occluded) or server-bound; no offline, ground-level, multi-task degradation tool tuned for tropical clutter |
| 3 | **Offline Hiker Information Assistant** — on-device RAG (small LLM + local knowledge base) | Digital guides/chatbots are cloud-dependent and fail in dead-zones; no offline, grounded assistant exists for safety-critical wilderness use |
| 4 | **Crowd & Carrying-Capacity Forecasting (standalone)** — ST-GNN on graph + terrain + weather + visitation → dynamic capacity | ST-GNNs are built for urban grids on live cellular data; never adapted to micro-spatial wilderness carrying-capacity forecasting from open/offline data |

---

## 4. Literature Review (Draft) — verified sources only

### 4.1 Domain: Sri Lankan trail tourism, ecology and carrying capacity
The recreational-ecology baseline is well established. Reviews of nature-based-tourism impacts (Monz et al., *Recreational Ecology: a review and gap analysis*, MDPI *Environments* 2019; and the Sri Lanka-focused *Think globally, act locally*, ScienceDirect 2020) document the "Global South data deficit" and the dominance of trail/vegetation trampling impacts. Sri Lanka-specific field studies quantify camping/biophysical degradation in dry-zone parks (PMC9132554) and mine TripAdvisor reviews to show ~75% of visitor dissatisfaction is management-driven overcrowding (ScienceDirect S2213078018300367). For the highlands specifically, the **Horton Plains social-carrying-capacity** studies (Senevirathna & Perera, *Tourism Management Perspectives*, 2015) empirically establish that satisfaction collapses with crowding (optimum < ~10 visitors/viewpoint; weekends/holidays exceed it). The **Pekoe Trail demand study** (IESC/USAID, 2023) supplies the growth forecasts. **Gap:** all of this is descriptive/static — none feeds a real-time management loop.

The **carrying-capacity backbone** is the Cifuentes (1992) cascade — **PCC → RCC → ECC** — where Physical Carrying Capacity is reduced by ecological correction factors (RCC) and then by management capacity (ECC). This proposal's novelty is making that cascade *dynamic* and *data-driven* rather than a one-off spreadsheet estimate.

### 4.2 Component 1 — IMU gait & terrain
Smartphone/wearable IMUs reliably classify walking conditions and terrain: outdoor walking-condition classification from IMU + pressure (PMC12788207); single-IMU terrain-induced gait change (Sher & Akanyeti, *Pervasive & Mobile Computing*, 2024); the canonical smartphone gait-analysis thesis showing adaptive peak-detection and ~94% surface classification at 50–100 Hz with 2–2.5 s windows (Sher, Aberystwyth PhD, 2023); terrain-topography context detection from a shoe IMU (Knuth & Groves, ION PLANS 2023); and TinyML gait recognition on a microcontroller (arXiv 2507.18627). Fatigue is detectable from gait (RF regressor energy/fatigue prediction; smartphone gait fatigue in MS, PMC11846754; fatigued-gait detection in older adults, PMC11782397). Unconstrained phone-position behaviour recognition is shown by GaitX (PMC12390545). **Gap:** every study either diagnoses the *human* or uses multiple body-worn research IMUs in the lab; none inverts the signal to map *terrain* hazards on real trails from one pocket phone.

### 4.3 Component 2 — Edge computer vision for litter & degradation
Litter detection is mature: YOLOv8 + Norfair tracking for floating bottles at >0.94 recall (*Scientific Reports*, 2025); Trashbusters litter detection/tracking (arXiv 2404.07467); and the **SortWaste** dataset + **ClutterScore** scene-hardness metric (arXiv 2601.02299) which shows accuracy degrades with visual clutter — directly relevant to forest floors. Soil-erosion CV exists but is aerial/satellite: coastal-area CNN erosion mapping (PMC9915231), and GIS-based **explainable** trail-degradation susceptibility with Random Forest + SHAP (MDPI *Forests* 16/7/1074, 2025) and erosion-susceptibility ML with SHAP (J. Hydroinformatics 26/1/72). **Gap:** aerial sensing is blocked by canopy; no offline, ground-level, multi-task (litter + degradation) model tuned for tropical clutter exists.

### 4.4 Component 3 — On-device RAG hiker assistant
**Retrieval-Augmented Generation** (Lewis et al., arXiv 2005.11401) grounds a language model's answers in retrieved documents, which sharply reduces hallucination — essential for safety-critical guidance. Retrieval relies on sentence embeddings such as **Sentence-BERT** (Reimers & Gurevych, arXiv 1908.10084) for fast local semantic search. Local tour-guidance precedent exists (TOURGURU summarises landmark info for tourists; LearningTour for itinerary recommendation; Syris/semantic models for hiking-trail difficulty), and the broader move toward field-deployable, offline AI is shown by offline RL navigation (ReViND, arXiv 2212.08244). Small open models (Gemma, Phi, Llama 3.2 1B/3B) now run quantised on phones. **Gap:** these guidance systems are cloud-dependent or non-generative; there is no fully offline, on-device RAG assistant that gives grounded, source-cited answers for hiking safety, rules and trail conditions in no-signal terrain.

### 4.5 Component 4 — Spatio-temporal graph forecasting & ECC

**ST-GNN architecture precedent.** Spatio-temporal graph neural networks are the established state of the art for flow and bottleneck forecasting on graph-structured networks. The Spatio-Temporal Pivotal GNN (AAAI 2024) and adaptive spatio-temporal-attention multi-models (PMC11723455) both target traffic-network forecasting with dedicated mechanisms for propagating congestion signals across a graph over time; the Spatio-Temporal Dual GNN (arXiv 2105.13591) extends this by modelling node- *and* edge-wise state jointly, which matters for a trail network where edge travel-time (not just node occupancy) is itself a first-class quantity; and STZINB-GNN (Stanford CS224W) addresses sparse, over-dispersed demand — the same distributional shape expected from a low-traffic wilderness trail rather than a dense urban corridor. **Critique:** all four are demonstrated on data-rich, continuously-instrumented, live-connectivity networks (hundreds of sensor nodes, minute-level cadence); none has been tested on a network an order of magnitude smaller or on offline/batch data, which is precisely the gap Module 4 occupies.

**Tourism-flow-specific precedent.** GNNs have been applied directly to tourism and pedestrian flow rather than only vehicle traffic: GCN-LSTM node-centrality forecasting in tourism flow networks (Jia & Chen, Informatica 49(14) art. 10973, 2025) is the closest architectural analogue, forecasting how a tourism network's structural importance shifts over time; pedestrian-flow prediction using a multi-head-attention GCN integrated with a knowledge graph (Du et al., *Applied Intelligence* 55(13):896, 2025) and pedestrian-volume prediction via diffusion-convolutional GRU with dynamic time warping (Dong et al., *J. Agric. Biol. Environ. Stat.*, 2025) both confirm that graph-based spatio-temporal methods transfer from vehicle traffic to pedestrian-scale movement. Outside the GNN family specifically, forest-trail visitor-count prediction using Random Forest/Gradient Boosting/LightGBM with weather, social-media activity, and calendar covariates (Ryu et al., *Sustainability* 17(13):6061, 2025, Daegwallyeong forest trail, six trail sections) is a directly on-domain precedent for the *feature design* Module 4 uses (weather + calendar), even though it does not use a graph model. **Critique:** the tourism/pedestrian-GNN papers still operate at urban or regional scale with continuous data feeds; the closest domain match (Ryu et al.) is methodologically simpler (tree ensembles, no graph structure) precisely because its trail network is small — which is itself evidence for, not against, Module 4's plan to test whether graph structure is worth the added complexity at this scale (see the falsifiable-hypothesis framing in §5.5).

**Small/sparse-graph precedent — the load-bearing strand for a 25–40 node network.** Because Horton Plains' World's End loop is far smaller than any benchmark above, the more important precedent is work that explicitly tests spatio-temporal graph models under sparsity. "No One-Model-Fits-All" (Gupta et al., ACM BuildSys '25, arXiv:2511.05179, 2025) compares ST-GNNs against classical (VAR), neural (GRU, Transformer), and time-series foundation models on *sparse IoT sensor-network graphs* rather than dense urban telemetry, and finds no single architecture dominates — direct precedent for budgeting a baseline comparison rather than assuming the GNN wins. Two additional 2025–2026 papers sharpen this further: a contextualized spatio-temporal graph method built specifically to forecast **sparse geospatial sensor networks**, addressing how sparse sensing locations exacerbate interpolation problems (Uremović et al., *Expert Systems with Applications* 294:128779, 2025), and a GNN for continuous traffic-density estimation on *unmonitored* roads from very few scattered measurements (Acciai et al., *Expert Systems with Applications* 327:132713, 2026) — the latter is a close structural analogy to Module 4's own situation of a dense trail graph with only a handful of manually-counted calibration points at the entrance and the World's End/Baker's Falls junctions. Most directly, a 2025 ACM Web Conference companion paper asks "Do We Really Need GCNs in Traffic Forecasting?" and shows a graph-free, pure-MLP architecture can match state-of-the-art GCN-based forecasting (Zhang et al., ACM WWW '25 Companion, 2025) — empirical, peer-reviewed evidence that graph structure does not automatically earn its keep, which is the exact falsifiable hypothesis §5.5 commits Module 4 to testing against its own LSTM/historical-average/ARIMA baselines. **Critique:** none of these five papers is set in a wilderness/trail/rural-recreation domain — all are transportation or generic-IoT-sensor domains, applied here by structural analogy (small node count, sparse ground truth) rather than literal domain match, which should be stated plainly rather than overstated as domain-identical precedent.

**Synthetic/simulated training-target precedent.** Because no segment-level Sri Lankan trail foot-traffic data exists, Module 4's occupancy target is synthesised from permit caps, SLTDA seasonality, and a Tobler-based movement model — a design choice that needs its own precedent to avoid reading as an ad hoc workaround. Spatiotemporal multi-graph convolutional networks trained with synthetic data for traffic-volume forecasting (Zhu et al., *Expert Systems with Applications* 187:115992, 2021/2022) is a peer-reviewed precedent for synthetic-data-assisted GNN training generally; more specifically on point, behaviourally-informed synthetic datasets built from movement rules (group dynamics, age-specific speed profiles) used to train predictive deep-learning models for crowd density and level-of-service (Gayathri et al., *Results in Engineering* 28:108210, 2025) is close structurally to Module 4's own permit-cap × seasonality × movement-model pipeline — both construct a synthetic ground truth from behavioural/regulatory rules rather than measuring it directly, then train a predictive model against that construction. **Critique:** in both precedents the synthetic data is a training-time augmentation alongside at least some real measurements, not the sole target as in Module 4's MVP — which is exactly why §5.5's partial-circularity discussion and calibration-count validation remain necessary rather than optional.

**Local carrying-capacity grounding and the theoretical case for a *dynamic* ECC.** Carrying-capacity-specific ML already exists in forestry tourism (multi-source GAT-Transformer, Ma & Geng, MDPI *Forests* 17(5):534, 2026) and in a landscape-driver study of trail formation using slope, elevation, and the **Topographic Wetness Index** as explainable-ML covariates (Guo et al., *Land* 15(5):715, 2026) — the latter is a direct precedent for Module 4's own use of DEM-derived TWI as a node feature, since it shows TWI validated as a covariate for trail/hiker spatial behaviour rather than only as a hydrology metric. Explainable tourist-arrival drivers via XGBoost + SHAP (Istanbul, Emerald *JHTT*, 2025) and, replacing the previously-unverifiable RG 392533688 claim, Sri Lanka-specific hybrid ML tourism-demand forecasting comparing SVR/Random Forest/ANN against a SARIMA baseline with social-media-sentiment integration (Hewapathirana, *Journal of Tourism Futures* 11(2):261, 2023/2025) inform the temporal/seasonal feature design. The case for *why* a dynamic, condition-responsive capacity number is preferable to a fixed permit quota rests on the **Limits of Acceptable Change (LAC)** framework (Stankey et al., USDA Forest Service GTR-INT-176, 1985 — **foundational/classical citation, cited for the named LAC method itself, on the same basis as the Cifuentes 1992 exception already used for the ECC cascade**), which reframes management around monitoring condition indicators against thresholds rather than capping visitor counts outright; a recent, directly on-domain application pairs this foundational cite with an empirical case — trail erosion assessed against Thresholds of Potential Concern and LAC in a high-visitation national park, using trail width as the impact indicator (Dragovich & Bajpai, *Sustainability* 14(7):4291, 2022). Together these support the proposal's own framing (echoed from the project's early scoping notes): a fixed daily quota cannot distinguish 50 hikers in a monsoon downpour from 300 on a dry day, whereas a condition/threshold-based approach — which a dynamically forecast ECC operationalises — can. **Gap:** none of the above operates on a *micro-spatial wilderness* graph offline; Module 4 adapts urban/regional ST-GNN methodology, small/sparse-graph baseline discipline, and synthetic-target precedent into that combination for the first time on a Sri Lankan trail network.

---

## 5. The Four Components (one per member)

> Shared deployment philosophy: **edge-first**. Each component runs its heavy model locally on the phone, stores only kilobyte-scale derived results (scores + GPS + timestamp), and syncs opportunistically when connectivity returns. Privacy is preserved with **Federated Learning** (only model-weight updates leave the device; raw IMU/images/location never do) — with the explicit caveat that FL needs differential privacy / secure aggregation to be a complete guarantee.

---

### Module 1 — Terrain & Effort Profiling (smartphone, offline)
**Objective & novelty.** Two independent, tractable signals on one phone: (a) **classify terrain type** (flat / rocky / muddy / steps / slope) from the IMU; (b) **estimate hiker effort/fatigue from route energetics** — distance + cumulative elevation gain — using established energy-expenditure models rather than fragile gait-inversion. Novelty: a localised, offline tropical-trail terrain classifier combined with a route-energetics effort gauge.

**Data — source / shape / size.**
- *Terrain — public pre-training (transfer):* **Irregular & Uneven Surfaces DB** (Luo et al., *Sci Data* 2020) — 30 subjects, **9 outdoor surfaces**, 6× IMU @100 Hz, CC BY 4.0 (best terrain base); **PAMAP2**, **HuGaDB**, **MAREA** (general locomotion encoder); **UCI HAR** — waist-mounted **smartphone** accel+gyro @**50 Hz**, 2.56 s/128-sample windows (phone-domain anchor). Shape: tri-axial time series → sliding windows.
- *Effort/fatigue — no ML dataset needed:* GPS track + **barometer/DEM** elevation → distance and ascent, fed to **Naismith's rule**, **Tobler's hiking function**, and **Minetti gradient metabolic-cost** models (optionally Pandolf for load). Optional calibration against RPE (rating of perceived exertion) self-reports or heart-rate if the phone/watch exposes it.
- *Primary collection (no SL trail IMU set exists):* 6–10 hikers, Android phone in a **fixed waist position** (the deployment assumption), accel+gyro **@50 Hz** + GPS + barometer, 5–6 terrain classes, **2.56 s windows / 50% overlap**, ~**15–25 h** across an accessible proxy trail + a Horton Plains/Pekoe trip, with synced video/observer ground-truth → tens of thousands of labelled windows.

**Implementation & scope.** Pre-process (interpolation, outlier removal, z-norm); pre-train a 1-D CNN/CNN-LSTM encoder on pooled public IMU; fine-tune the **terrain classifier** on Irregular-Surfaces + custom set; deploy a lightweight **XGBoost/Random Forest** or quantised CNN-LSTM on-device. Effort module computes cumulative energy expenditure along the route and raises a graded fatigue alert.
- **MVP:** terrain-type classifier (fixed phone position) + route-energetics effort gauge with a "rest/turn-back" alert.
- **Stretch:** unconstrained phone position; terrain *anomaly* flagging (loose/eroded patches); fusing effort + terrain into a personal difficulty score.
- *Out of scope:* clinical gait diagnosis, multi-sensor body networks, inferring terrain *degradation severity* from gait (that's Module 2's job).

**End output.** An on-device app that tags terrain type along the route and shows a personal effort/fatigue gauge with offline safety alerts; exportable per-segment terrain-difficulty summary.

---

### Module 2 — Trail Degradation & Litter Vision (edge)
**Objective & novelty.** A quantised, **offline** smartphone model performing two ground-level tasks: (a) detect/count litter; (b) segment degradation (root exposure, gully/erosion, trail braiding/widening) — overcoming canopy occlusion that defeats aerial sensing, with **explainable** outputs for policy.

**Data — source / shape / size.**
- *Litter pre-training (all verified):* **SortWaste** — **5,261 images / 87,252 bounding boxes / 8 classes**, 1920×1080, COCO+YOLO, **CC BY 4.0** (+ ClutterScore); **TACO** — 1,500 images / 4,784 **instance masks** / 60 classes, **CC BY 4.0**; **TrashNet** — 2,527 images / 6 classes (classification), MIT; **UAVVaste** — 772 images / 3,718 COCO bbox+mask, Apache-2.0 (aerial, for robustness); **OpenLitterMap** — 500k+ geotagged ground-level observations, **ODbL**. *(Note: "LWW" is a small food-tray sorting set, not outdoor litter — do not use as an in-the-wild benchmark.)*
- *Degradation:* **no public ground-level *soil-erosion* segmentation dataset exists** (every erosion dataset found is satellite/UAV). Closest ground-level transfer sources: **Hiking-Trail Semantic Segmentation** (IEEE DataPort, >1,250 imgs, has `root`/`trail`/`rough trail` classes — the single best match), **RUGD** (~7,456 frames, dirt/gravel/grass), **GOOSE** (10,000 pairs, CC BY-SA 4.0, finest off-road ontology), **RELLIS-3D** (RGB subset, has `mud`/`puddle`), **Freiburg Forest** (explicit `trail` class); plus crack/rill proxies **Crack500** (~3,368) and **DeepCrack** (537). Then fine-tune on a **custom set**.
- *Primary collection:* **~1,000–2,000 ground-level Horton Plains/Pekoe images**, dual-annotated — bounding boxes (litter classes) + segmentation masks (degradation severity: healthy / moderate exposed soil / severe); heavy augmentation (flip, rotate, mosaic, lighting); 70/15/15 split.

**Implementation & scope.** Use **a single YOLOv8/v11-seg model** (detection + instance segmentation in one network, with mature TFLite/NCNN/CoreML export) rather than RT-DETR + DenseNet121 — simpler and genuinely edge-deployable (RT-DETR is heavier and DenseNet121 isn't a segmentation architecture). **Sample frames at ~1–2 fps**, not full video, to avoid battery drain/thermal throttling. **INT8 quantisation → TFLite**; **ClutterScore** to gate noisy frames; **SHAP** for explainability of the degradation classifier.
- **MVP:** litter detection + count, and segmentation of 2–3 degradation classes (erosion, exposed roots) on the custom set.
- **Stretch:** trail-braiding/widening, severity grading, RT-DETR accuracy comparison.
- *Out of scope:* cloud video upload, 3-D reconstruction, gem/forgery tasks (dropped — not in this framework).
- *Note:* litter detection ~mAP@50 > 0.80 is realistic; degradation segmentation will be lower and subjective — write a labelling rubric and report inter-annotator agreement.

**End output.** An offline mobile CV module emitting **geotagged litter counts + degradation-severity masks** as KB-sized records → synced to a park dashboard as a **degradation map** (a Component-4 node feature).

---

### Module 3 — Offline Hiker Information Assistant (on-device RAG)
**Objective & novelty.** Give hikers an **offline question-answering assistant** that returns short, trusted, source-grounded answers about safety, trails, park rules, and fair pricing, with no internet — the first fully on-device RAG assistant for a safety-critical, no-signal wilderness setting.

**Data — source / shape / size.**
- *Knowledge base (curated, not scraped):* official **DWC** rules/permits/emergency contacts, **Pekoe Trail** and **Horton Plains** guides, standard **first-aid** references, weather guidance, open notes on local species, leave-no-trace advice, and **verified operator/permit and fair-price info**. Shape: text chunked into passages, each stored with a vector embedding in an on-device index. Size: modest (hundreds to a few thousand passages); content is official, open, or licensed (no ToS-violating scraping).
- *Models:* an open **small language model** (e.g. Gemma / Phi / Llama 3.2 1B–3B in 4-bit) for generation, plus a small **embedding model** (Sentence-BERT family) for retrieval; both quantised for the phone.
- *Evaluation set:* ~100–200 realistic hiker questions with reference answers, written with domain input, to measure answer quality and grounding.

**Implementation & scope.** Build the vector index from the knowledge base; on a question, run local semantic search and feed the top passages to the SLM, which answers using only that text (RAG) and cites the source.
- **MVP:** offline RAG assistant answering safety/trail/rules/fair-price questions, with sources shown, on an Android phone.
- **Stretch:** voice input/read-aloud; Sinhala/Tamil support; light navigation hints.
- **Fallback:** if a phone cannot run the generative model, return the best-matching trusted passage (retrieval-only).
- *Out of scope:* open-web chat, medical diagnosis, anything not grounded in the curated base; consuming other modules.

**End output.** Short, grounded, source-cited answers to hiker questions, fully offline — acting as a combined safety, trail, rules, and fair-price guide. (Anonymised query categories and price-fairness reports can optionally inform the park dashboard.)

---

### Module 4 — Crowd & Carrying-Capacity Forecasting (fully standalone)
**Objective & novelty.** Forecast **micro-spatial crowding/bottlenecks** on a graph of the trail network and compute a **dynamic Effective Carrying Capacity (ECC)** — replacing static permit quotas. **This module is self-contained: it relies only on its own independent inputs (trail graph, terrain, weather, historical/seasonal visitation) and does NOT consume Modules 1–3.** Novelty: adapting urban ST-GNN forecasting to a data-sparse wilderness trail using only open/offline data.

**Data — source / shape / size.**
- *Graph (confirmed mapped):* **OpenStreetMap** (Geofabrik SL 136 MB `.osm.pbf` or targeted Overpass query, **ODbL**) — an Overpass bbox query returns **49 `highway=path/footway/track` ways** inside Horton Plains, and the **Pekoe Trail is mapped as 23 relations / 46 ways**; official GPX (Wikiloc/AllTrails) supplements. Nodes = segments/POIs/junctions; edges = connectivity.
- *Node terrain features:* **30 m DEM** — Copernicus GLO-30 or SRTM GL1/NASADEM (public, via OpenTopography/AWS) → elevation, slope, aspect, and **Topographic Wetness Index** `TWI = ln(a/tan β)` (SAGA/QGIS/`pysheds`).
- *Temporal features (all independent of other modules):* **weather** from **Open-Meteo** (ERA5 archive 1940–present, hourly, no API key, CC BY) + **NASA POWER** + high-res rainfall **CHIRPS** (0.05°); calendar features (hour, day-of-week, poya/holiday, season). Terrain difficulty comes from the **DEM** directly (slope/TWI), not from Module 1.
- *Foot-traffic — the one hard gap:* **no public segment-level SL trail counts exist** (DWC publishes only park aggregates, e.g. ~166k–246k visitors/yr; the Atlantic-Area people-counter dataset behind RG 375226880 is **not released**). So the target is **proxy-modelled**: (1) anchor on DWC daily permit cap + annual total; (2) disaggregate to daily via **SLTDA** monthly seasonality (Dec/Jan ≈1.3×, May ≈0.67×) + poya/holiday/weekend factors; (3) disaggregate intra-day & per-segment via a movement model (morning start-surge, loop geometry, Tobler's hiking-time over edges); (4) **calibrate with a few days of manual/clicker counts** at the entrance + World's End/Baker's Falls junctions. Transfer analogues for pre-training: **NPS Visitor-Use Statistics (IRMA)** (CC0, monthly, 1979–2025) and **Eco-Counter open daily trail counts** (e.g. City of Austin, open data).
- *Methodology/transfer benchmarks (verified specs):* **METR-LA** (207 nodes × 34,272 × 5 min), **PEMS-BAY** (325 × 52,116), **PeMS04** (307 × 16,992 × 3), **PeMS08** (170 × 17,856 × 3) — architecture prototyping/pre-training.
- *Pilot graph (Horton Plains World's End loop — single controlled entry, real bottlenecks):* ~**25–40 nodes**, ~**30–50 directed edges** (loop is largely one-way), **1-hour** resolution over the 06:00–18:00 window, **≥2 years** synthesised hourly per-segment occupancy (≈9,000 steps/node — comparable to PeMS04/08), driven by real ERA5 weather + SLTDA seasonality + DWC caps. **ECC labels derived** via the Cifuentes cascade (no ECC ground-truth exists).

**Implementation & scope.** **GCN** (spatial) + **LSTM/Transformer** (temporal) with **adaptive spatio-temporal attention**; node features are DEM-derived terrain + weather + calendar (no other-module inputs). Compute the **PCC→RCC→ECC** cascade dynamically (correction factors driven by weather/season). **Include simpler baselines (per-node LSTM, historical-average, ARIMA)** to prove the GNN actually adds value on a small graph. Validate with **spatial block cross-validation**.
- **MVP:** occupancy/bottleneck forecast on the calibrated synthetic series, with baselines, on the Horton Plains loop.
- **Stretch:** dynamic ECC cascade + hazard-routing ensemble (XGBoost/LightGBM → MLP) for flash-flood/landslide probability; second trail.
- *Honest limitation to state:* the foot-traffic target is **synthetic (permit-cap × seasonality × movement model)**, calibrated with a few days of manual counts — so the model is validated against a simulator + thin real data, not a full real footfall record.
- *Out of scope:* consuming Modules 1–3, physical IoT counters, nationwide rollout, automated permit revocation (human-in-the-loop only).

**End output.** A **dynamic ECC per node**, bottleneck forecasts hours ahead, **dynamic ticketing thresholds** for park management, and **offline hazard-rerouting** alerts to hikers.

---

### 5.5 Module 4 — Extended Methodology & Plan of Work

*(This subsection expands Module 4 beyond the TAF word limit for the full Proposal document. Owner: IT23343948 — Weerasekara J.V.)*

**Why a Spatio-Temporal GNN, and why that choice is defensible on a 25–40 node graph.**
The literature review (§4.5) establishes ST-GNNs as the state-of-the-art for flow/bottleneck
forecasting on graph-structured networks (AAAI 2024 Spatio-Temporal Pivotal GNN; PMC11723455
adaptive attention; Jia & Chen 2025 GCN-LSTM tourism-flow networks), but every one of those
precedents operates on data-rich, live-connectivity urban or regional networks with hundreds of
nodes and continuous telemetry — none has been applied to a small, offline, wilderness trail
graph. `docs/TECHNICAL_AUDIT.md` flags this honestly as a real risk, not just a novelty claim:
GNNs "earn their keep" on large networks, and on a small loop like Horton Plains World's End
(~25–40 nodes), a simpler per-node model could plausibly match a GCN's performance. Two design
decisions respond directly to that risk rather than assuming the GNN wins by default:
1. **Mandatory baseline comparison.** Per-node LSTM (no graph structure), historical-average, and
   ARIMA baselines are trained and evaluated on the identical synthetic-occupancy series and
   identical spatial-block CV splits as the ST-GNN. The GNN is only reported as adding value if it
   beats these baselines by a statistically significant margin (paired t-test, p < 0.05, per the
   evaluation protocol in §9) — not by construction. This is not a hedge invented for this
   proposal: Gupta et al. (ACM BuildSys '25, 2025) show no single architecture — GNN, classical, or
   foundation-model — dominates on sparse sensor graphs, and Zhang et al. (ACM WWW '25 Companion,
   2025) empirically demonstrate a graph-free pure-MLP architecture matching state-of-the-art GCN
   traffic forecasting; both are peer-reviewed, 2025, and directly on point for why "does the graph
   actually help here" must be tested, not assumed, at this node count (see §4.5).
2. **The propagation argument, stated explicitly as the falsifiable hypothesis being tested:**
   because Horton Plains is a loop with a single controlled entry point, congestion at one node
   should be *predictable from* upstream occupancy and travel time to that node (Tobler's hiking
   function gives the expected lag). A graph model can encode that propagation structurally; a
   per-node LSTM cannot see other nodes at all. If the baselines match the GNN anyway, that is
   itself a valid, reportable finding — it would mean the loop's small size makes graph structure
   unnecessary at this scale, which is worth stating plainly rather than obscuring.

**Why the synthetic foot-traffic target is not purely circular, and what breaks that circularity.**
`docs/TECHNICAL_AUDIT.md` is direct about this: training a model to reproduce a target built from
the same seasonality/permit-cap rules used to generate it risks the model just learning the
simulator, not reality. Three things are done specifically to reduce (not eliminate) that risk,
and all three must be reported as partial mitigations, not a solved problem:
- The **seasonality and permit-cap inputs** (SLTDA monthly multipliers, DWC daily caps) are
  independently sourced, real, published figures — not fitted parameters — so the simulator's
  macro-shape is externally grounded, even though its micro-shape (the movement model) is not.
  Constructing a synthetic training target from real behavioural/regulatory rules rather than
  measuring it directly is itself a published pattern, not an ad hoc workaround: Zhu et al.
  (*Expert Systems with Applications*, 2021/2022) train a spatiotemporal multi-graph CNN with
  synthetic traffic-volume data, and Gayathri et al. (*Results in Engineering*, 2025) build
  behaviourally-informed synthetic crowd datasets — from movement rules, not measurement — to
  train predictive density models, structurally the closest precedent to this pipeline.
- **Manual/clicker calibration counts** at the entrance and the World's End / Baker's Falls
  junctions provide a small held-out real signal the synthetic series must be checked against —
  the model's per-segment predictions should be validated against these counts specifically, not
  just against the synthetic training series, and any divergence must be reported rather than
  smoothed over.
- **Weather-driven variation is exogenous, not self-generated** — ERA5/Open-Meteo rainfall and the
  DEM-derived Topographic Wetness Index enter the model as real, independently measured covariates
  that were not used to construct the foot-traffic target, so at minimum the model's response to
  weather is being tested against real data, even where its baseline occupancy level is not.

**Why a dynamic ECC over a static quota is a management-theory claim, not just a modelling
preference.** The stated advantage of a condition-responsive capacity number — that 50 hikers in a
monsoon downpour can degrade a trail more than 300 on a dry day, which a fixed daily quota cannot
see — is grounded in the **Limits of Acceptable Change (LAC)** framework (Stankey et al., USDA
Forest Service GTR-INT-176, 1985; foundational/classical citation for the named LAC method, cited
on the same basis as the Cifuentes 1992 exception used for the ECC cascade itself), which reframes
wilderness management around monitoring condition indicators against thresholds rather than
capping visitor counts outright. A recent application pairs that foundational framework with an
empirical case directly relevant to Module 4's own erosion/degradation context: trail erosion
assessed against Thresholds of Potential Concern and LAC in a high-visitation national park, using
trail width as the impact indicator (Dragovich & Bajpai, *Sustainability*, 2022). Module 4's
weather- and season-responsive ECC is presented as one operationalisation of that same
condition-based logic, not a novel management theory in its own right.

**ECC is reported as a derived management output, not a validated prediction.** Because no ECC
ground truth exists anywhere for these trails, Module 4's evaluation claims are scoped to what is
actually checkable: occupancy/bottleneck forecasting accuracy (RMSE/MAE under spatial block CV)
against the calibrated series and the manual counts. The Cifuentes PCC→RCC→ECC cascade is then
applied deterministically on top of the forecast to produce the dynamic capacity number — this
conversion step is a formula application, not a model output, and is presented as such.

**Plan of work (indicative, module-level; align with the team's shared TAF/Proposal timeline
once the Charter sets exact dates).**

| Phase | Work | Key output |
|---|---|---|
| 1 — Graph & feature build | Extract OSM graph (Overpass query, Horton Plains World's End loop), build DEM-derived slope/TWI features, pull ERA5/Open-Meteo weather history | Static graph + node/edge feature tables |
| 2 — Synthetic target construction | Implement the permit-cap × SLTDA-seasonality × Tobler-movement-model pipeline; generate ≥2 years of hourly synthetic occupancy | Calibrated synthetic occupancy series |
| 3 — Field calibration | Collect a few days of manual/clicker counts at entrance + World's End/Baker's Falls junctions | Real held-out calibration sample |
| 4 — Baseline models | Implement and tune historical-average, ARIMA, per-node LSTM on identical CV splits | Baseline performance table |
| 5 — ST-GNN development | Implement GCN + LSTM/Transformer with adaptive spatio-temporal attention; hyperparameter tuning | Trained ST-GNN model |
| 6 — Evaluation | Spatial block CV, baseline comparison with significance testing, calibration-count validation, feature ablation (weather/terrain/calendar) | Evaluation chapter results |
| 7 — ECC cascade & outputs | Apply Cifuentes cascade to forecasts; produce dynamic ticketing-threshold recommendation format | Final deliverable + dashboard-ready output |

**Stretch, time permitting:** hazard-routing ensemble (XGBoost/LightGBM → MLP) for flash-flood/
landslide probability at each node; a second trail graph (e.g. a Pekoe Trail segment) to test
generalization beyond the single Horton Plains loop.

---

## 6. How the Modules Relate (loose coupling — no hard dependency)

The four modules are **peers**, each a complete sub-project with its own data, model, metrics and output. They are *not* a pipeline — **none requires another to function.** A shared dashboard/app can simply *display* all four side by side:

```
   ┌─────────────── HIKER'S PHONE (offline) ───────────────┐     ┌──── PARK / ADMIN ────┐
   │  M1 Terrain + effort   →  difficulty + fatigue gauge   │     │  M4 Crowd forecast    │
   │  M2 Camera CV          →  litter + degradation map     │     │  (graph+DEM+weather+  │
   │  M3 Hiker assistant*   →  offline Q&A (safety / rules)  │     │   visitation, ALONE)  │
   └────────────────────────────────────────────────────────┘     │  → dynamic capacity   │
        (*text cached offline, scored on sync)                     └───────────────────────┘
                         ▼  optional shared dashboard  ▼
   ┌──────────────────────────────────────────────────────────────────────────────────┐
   │  Unified view: trail condition (M1+M2) · hiker assistant (M3) · crowd/ECC (M4)     │
   └──────────────────────────────────────────────────────────────────────────────────┘
```

**Optional future synergy (explicitly NOT a dependency):** if all four are deployed and adopted, M1/M2 field signals *could* later enrich M4's correction factors — but M4 is built and evaluated entirely on its own data, so the project does not rely on that happening.

---

## 7. Consolidated Dataset Plan

| Component | Public data (transfer) | Primary collection | Shape | Approx. size |
|---|---|---|---|---|
| M1 Terrain+Effort | Irregular-Surfaces (CC BY 4.0), PAMAP2, HuGaDB, MAREA, UCI HAR (terrain); energy-expenditure models (Naismith/Tobler/Minetti) for effort — no ML dataset needed | 6–10 hikers, phone @50 Hz + GPS + barometer, 5–6 terrain labels | tri-axial IMU windows + GPS/elevation track | ~15–25 h labelled |
| M2 Vision | *Litter:* TACO (best viewpoint, CC BY 4.0) + SortWaste (5,261/87,252/8, CC BY 4.0) + TrashNet; *Degradation:* Hiking-Trail Semantic Seg, RUGD, GOOSE (CC BY-SA), RELLIS-3D, Freiburg Forest, Crack500/DeepCrack | ~2,500 Horton Plains/Pekoe images (no ground-level erosion set exists) | RGB + bbox (litter) + masks (degradation) | ~2.5k images, 70/15/15 split by segment |
| M3 RAG assistant | Curated knowledge base (DWC rules, trail guides, first-aid, species, fair-price info); small LLM (Gemma/Phi/Llama 3.2 1–3B 4-bit) + Sentence-BERT embeddings | Build KB from official/open sources; ~100–200 Q&A eval set | text passages + vector index | hundreds–few thousand passages |
| M4 ST-GNN | OSM/Geofabrik (ODbL), Copernicus/SRTM DEM, Open-Meteo/NASA POWER/CHIRPS, NPS IRMA (CC0) + Eco-Counter (transfer), METR-LA/PEMS benchmarks | trail graph build + **synthesised foot-traffic** (no public SL counts) + few-day calibration counts | graph adjacency + node/edge feature time series | ~25–40 nodes, 1-hr, ≥2 yr (~9k steps/node) |

---

## 8. Ethics, Privacy and Risk
- **Ethical clearance required** (IMU = movement data; image capture of people possible). Mitigations via **privacy-by-design**: informed consent at onboarding; on-device processing; store/sync only KB-scale derived features (scores, GPS, timestamps), never raw IMU/images. **Federated Learning is descoped to future work** — it is overkill for a student timeline with no real federated user base, and the privacy goal is already met by on-device processing + minimal sync.
- **Data-licensing/ToS compliance:** respect dataset licences (CC-BY-NC-SA datasets = research only; commercialisation needs permission); do **not** scrape sites whose ToS forbid it — prefer CC-BY data and official APIs; store derived features, not review corpora.
- **Operator/price information** in the assistant is presented factually from verified or official sources (e.g. published permit tariffs), not as accusations against named operators, to avoid defamation; the assistant also makes clear that answers are guidance, not emergency services.
- **Key research risks:** (i) the IMU terrain-vs-fatigue *inversion* is novel and unproven on heterogeneous untrained hikers — treat as the project's highest-risk hypothesis and benchmark honestly; (ii) RT-DETR/DenseNet121 are heavier than YOLO — budget for accuracy loss under quantisation; (iii) **the foot-traffic target for C4 has no public ground-truth** (DWC publishes only aggregates; no segment-level counts) — the pilot runs on a permit-cap-anchored *synthetic* occupancy series and must be calibrated with a few days of manual counts and validated against the Cifuentes ECC cascade rather than over-claiming; (iv) no ground-level soil-erosion segmentation dataset exists, so C2 degradation depends on the custom-collected set (public sets only pre-train the backbone).

## 9. Evaluation (per component)
- **M1:** Leave-One-Subject-Out cross-validation for terrain accuracy/F1 on the custom set; effort/fatigue estimate validated against RPE self-reports (and route time vs Naismith prediction).
- **M2:** mAP@50/mAP@50-95 (litter) and IoU/Dice (degradation) on held-out tropical images; on-device latency/battery; κ inter-annotator agreement on degradation masks.
- **M3:** answer quality on the ~100–200 Q&A eval set (correctness + is it grounded in a real source), retrieval hit-rate, hallucination rate, and on-device latency; human rating of helpfulness.
- **M4:** RMSE/MAE under **spatial block CV** vs simpler baselines (per-node LSTM, historical-average, ARIMA) to justify the GNN; feature-ablation over weather/terrain/calendar; bottleneck lead-time; statistical significance (paired t-test, p<0.05). State the synthetic-target caveat in every result.

## 10. Corrections carried over from the source-material audit
- The **gem-verification / document-forgery** topics in the original tracking sheet are **not** part of this framework and were dropped.
- **GEMTELLIGENCE** (if referenced anywhere) is spectroscopy-based (XRF/FTIR), **not** image-based — corrected.
- Several tracking-sheet summaries were copy-pasted from the wrong paper and the entire **"Sajana" batch was fabricated**; none of those are cited here. Only verified sources appear above.

---

### Key references (verified, except one flagged item — see note)
Cifuentes (1992) carrying-capacity (PCC/RCC/ECC) · Stankey et al. 1985 (USDA GTR-INT-176, Limits of Acceptable Change — foundational) · Dragovich & Bajpai 2022 (*Sustainability*, trail erosion/LAC/TPC) · Senevirathna & Perera 2015 (Horton Plains crowding, *Tourism Mgmt Perspectives*) · IESC/USAID 2023 Pekoe Trail demand · Monz et al. 2019 (*Environments*, recreational ecology review) · PMC12788207, Sher & Akanyeti 2024, Sher 2023 thesis, Knuth & Groves 2023, arXiv 2507.18627, PMC12390545, PMC11782397 (IMU/gait) · *Sci Reports* 2025 (YOLOv8+Norfair), arXiv 2404.07467 (Trashbusters), arXiv 2601.02299 (SortWaste), PMC9915231, MDPI Forests 16/7/1074, J.Hydroinformatics 26/1/72 (CV/erosion) · arXiv 2005.11401 (RAG, Lewis et al.), arXiv 1908.10084 (Sentence-BERT), TOURGURU (RG 341757650), arXiv 2212.08244 (ReViND) (RAG/assistant) · AAAI 2024 (ST Pivotal GNN), PMC11723455, Informatica 49(14)/2025 art. 10973, arXiv 2105.13591, MDPI Forests 17(5):534/2026, Stanford CS224W STZINB-GNN, RG 375226880, Emerald JHTT 2025 (ST-GNN/forecasting), Hewapathirana 2023/2025 (*J. Tourism Futures*, SL demand ML — replaces the previously-unverifiable RG 392533688), Gupta et al. 2025 (ACM BuildSys, sparse-graph baseline discipline), Zhang et al. 2025 (ACM WWW Companion, graph-free MLP vs GCN), Uremović et al. 2025 & Acciai et al. 2026 (*Expert Systems with Applications*, sparse geospatial forecasting), Zhu et al. 2021/2022 & Gayathri et al. 2025 (synthetic-target GNN/crowd precedent), Ryu et al. 2025 (*Sustainability*, forest-trail visitor forecasting), Guo et al. 2026 (*Land*, TWI/slope trail-formation drivers).

*Datasets:* Irregular & Uneven Surfaces DB, DUO-GAIT, PAMAP2, HuGaDB, MAREA, UCI HAR; SortWaste, TACO, TrashNet, UAVVaste, OpenLitterMap; curated KB (DWC/Pekoe/Horton Plains guides, first-aid, species, fair-price info), small LLM (Gemma/Phi/Llama 3.2) + Sentence-BERT; OSM/Geofabrik, Copernicus GLO-30/NASADEM, Open-Meteo/NASA POWER/CHIRPS, METR-LA/PEMS-BAY/PeMS04/PeMS08.

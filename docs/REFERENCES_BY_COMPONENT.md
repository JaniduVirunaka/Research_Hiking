# Verified References by Module — J26-IT-363

Only papers confirmed real and on-topic by the fact-check are listed (fabricated "Sajana" entries and unverifiable items excluded). ResearchGate links resolve by publication ID even where the slug is shortened.

---

## Module 1 — Terrain & Effort Profiling (IMU + route energetics)

| Paper | Venue / Year | Link | Used for |
|---|---|---|---|
| Outdoor Walking Classification using IMU + foot-pressure | PMC, 2025 | https://pmc.ncbi.nlm.nih.gov/articles/PMC12788207 | Terrain/condition classification from IMU |
| Minimum data sampling for terrain-induced gait change (single IMU) | Sher & Akanyeti, 2024 | https://irep.ntu.ac.uk/id/eprint/52413/1/2250536_Sher.pdf | Single-IMU terrain recognition; sampling/window choices |
| Automating gait analysis using a smartphone (PhD thesis) | Aberystwyth, 2023 | https://pure.aber.ac.uk/ws/portalfiles/portal/74587204/Sher_Arshad.pdf | Smartphone IMU pipeline; 50–100 Hz, 2.56 s windows |
| IMU-based context detection of terrain topography | Knuth & Groves, ION 2023 | https://www.ion.org/publications/abstract.cfm?articleID=18852 | Terrain-type classification feature design |
| Gait recognition with TinyML on IMU | arXiv 2507.18627, 2025 | https://arxiv.org/html/2507.18627v1 | On-device (edge) gait inference |
| Real-time distracted-walking detection, smartphone IMU (GaitX) | PMC, 2025 | https://pmc.ncbi.nlm.nih.gov/articles/PMC12390545 | Unconstrained phone-position handling |
| Real-time foot-height & activity from foot-mounted IMU | MDPI Sensors 26(10):3166, 2026 | https://www.mdpi.com/1424-8220/26/10/3166 | Real-time on-phone gait segmentation |
| IMU prediction of energy & fatigue in walking | RG 379267773 | https://www.researchgate.net/publication/379267773 | Fatigue context (supporting) |
| Smartphone gait analysis of fatigue (MS) | PMC11846754 | https://pmc.ncbi.nlm.nih.gov/articles/PMC11846754 | Fatigue measurement context |

**Foundational effort models** (classic, not from the tracking sheet):
- Minetti et al. (2002), metabolic cost of gradient walking — https://journals.physiology.org/doi/10.1152/japplphysiol.01177.2001
- Tobler (1993), hiking function — https://escholarship.org/uc/item/05r820mz
- Naismith's rule (1892).

---

## Module 2 — Trail Degradation & Litter Vision

| Paper | Venue / Year | Link | Used for |
|---|---|---|---|
| Plastic-bottle detection (YOLOv8 + Norfair), aquatic | Scientific Reports, 2025 | https://www.researchgate.net/publication/393587342 | Litter detection + counting |
| SortWaste: dense waste-detection dataset + ClutterScore | arXiv 2601.02299, 2026 | https://arxiv.org/abs/2601.02299 | Litter pre-training; clutter metric |
| Trashbusters: DL litter detection & tracking | arXiv 2404.07467, 2024 | https://arxiv.org/html/2404.07467v1 | Litter detection/tracking |
| TACO: Trash Annotations in Context (dataset paper) | arXiv 2003.06975, 2020 | https://arxiv.org/abs/2003.06975 | Best-viewpoint litter pre-training |
| CNN soil-erosion mapping (coastal) | PMC9915231, 2023 | https://pmc.ncbi.nlm.nih.gov/articles/PMC9915231 | Erosion CV (aerial baseline / gap) |
| Forest trail-degradation susceptibility, GIS + XAI (RF + SHAP) | MDPI Forests 16(7):1074, 2025 | https://www.mdpi.com/1999-4907/16/7/1074 | Explainable degradation modelling |
| Soil-erosion susceptibility ML (SHAP), Nghe An | J. Hydroinformatics 26(1):72, 2024 | https://iwaponline.com/jh/article/26/1/72/99420 | Erosion feature/XAI methodology |

---

## Module 3 — Offline Hiker Information Assistant (on-device RAG)

| Paper | Venue / Year | Link | Used for |
|---|---|---|---|
| Retrieval-Augmented Generation (Lewis et al.) | arXiv 2005.11401, NeurIPS 2020 | https://arxiv.org/abs/2005.11401 | Core RAG method (grounded answers) |
| Sentence-BERT (sentence embeddings) | arXiv 1908.10084, EMNLP 2019 | https://arxiv.org/abs/1908.10084 | Embeddings for local semantic search |
| TOURGURU: tour-guide mobile app (SLIIT) | RG 341757650 | https://www.researchgate.net/publication/341757650 | On-the-go guidance precedent (local) |
| LearningTour: ML tour recommendation | RG 332595961 | https://www.researchgate.net/publication/332595961 | Tour information / recommendation |
| Semantic data models for hiking-trail difficulty (Syris) | RG 337989394 | https://www.researchgate.net/publication/337989394 | Structured trail-knowledge representation |
| Offline RL for visual navigation, ReViND | arXiv 2212.08244, 2022 | https://arxiv.org/abs/2212.08244 | Offline, in-field AI (no live connection) |
| On-device AI engineering (developer report, grey lit) | Reddit r/reactnative, 2026 | https://www.reddit.com/r/reactnative/comments/1renp0x/ | Fitting LLMs to phone RAM/battery limits |

*Notes:* Lewis et al. (RAG) and Sentence-BERT are foundational method references (not from the tracking sheet). The on-device engineering link is grey literature, cited for practical edge-deployment, not as an academic result. Small open models suitable for the device (for example Gemma, Phi, or Llama 3.2 1B/3B in 4-bit) are the candidate generative models.

---

## Module 4 — Crowd & Carrying-Capacity Forecasting (ST-GNN)

| Paper | Venue / Year | Link | Used for |
|---|---|---|---|
| Spatio-Temporal Pivotal GNN for traffic flow | AAAI 2024 | https://ojs.aaai.org/index.php/AAAI/article/view/28707 | Core ST-GNN architecture |
| Adaptive spatio-temporal attention, traffic flow | PMC11723455, 2024 | https://pmc.ncbi.nlm.nih.gov/articles/PMC11723455 | Adaptive attention mechanism |
| GCN–LSTM Analysis of Spatiotemporal Evolution of Node Centrality in Tourism Flow Networks (Jia & Chen) | Informatica 49(14), 2025 | https://www.informatica.si/index.php/informatica/article/view/10973 | Tourism-flow GNN precedent |
| Spatio-Temporal Dual GNN for travel-time estimation | arXiv 2105.13591, 2021 | https://arxiv.org/abs/2105.13591 | Node + edge graph modelling |
| Forestry Tourism Resource Carrying Capacity Prediction Model Based on Multi-Source Data Algorithm (Ma & Geng) | MDPI Forests 17(5):534, 2026 | https://www.mdpi.com/1999-4907/17/5/534 | Carrying-capacity ML precedent |
| Travel-demand forecasting, STZINB-GNN (sparse data) | Stanford CS224W (blog) | https://medium.com/stanford-cs224w/revolutionizing-travel-demand-forecasting-with-spatial-temporal-graph-neural-networks-c7a208eef7ba | Sparse/over-dispersed targets |
| Forecasting daily foot traffic on recreational trails | RG 375226880, 2023 | https://www.researchgate.net/publication/375226880 | Foot-traffic forecasting method |
| ⚠️ Hybrid tourist-arrivals forecasting, Sri Lanka — **UNVERIFIED, re-check before use (see `docs/SOURCES_LOG.md`)** | RG 392533688 (unconfirmed) | https://www.researchgate.net/publication/392533688 | National arrivals covariate |
| ML drivers of tourist arrivals (XGBoost + SHAP), Istanbul | Emerald JHTT, 2025 | https://www.emerald.com/jhtt/article/doi/10.1108/JHTT-08-2025-0686 | Explainable demand drivers |
| No One-Model-Fits-All: STGNN vs. foundation-model forecasting trade-offs on sparse sensor graphs (Gupta et al.) | ACM BuildSys '25, 2025 (arXiv:2511.05179) | https://doi.org/10.1145/3736425.3771958 | Precedent: GNN must be compared against non-graph baselines on small/sparse graphs, not assumed to win |
| Spatiotemporal multi-graph CNN with synthetic data for traffic-volume forecasting (Zhu et al.) | Expert Systems with Applications 187:115992, 2021/2022 | https://doi.org/10.1016/j.eswa.2021.115992 | Precedent: synthetic-data-assisted GNN training is an accepted published pattern |
| Pedestrian flow prediction, multi-head attention GCN + knowledge graph (Du et al.) | Applied Intelligence 55(13):896, 2025 | https://doi.org/10.1007/s10489-025-06793-8 | Domain-relevant (pedestrian, not vehicle) GNN precedent |
| Pedestrian volume prediction, diffusion conv. GRU + DTW (Dong et al.) | J. Agric. Biol. Environ. Stat., 2025 | https://doi.org/10.1007/s13253-025-00696-4 | Domain-relevant (pedestrian volume) GNN-adjacent precedent |
| Social carrying capacity / crowding, Horton Plains | Senevirathna & Perera, 2015 | https://www.sciencedirect.com/science/article/abs/pii/S2211973615000781 | ECC grounding (local) |
| Carrying-capacity methodology (PCC→RCC→ECC, Cifuentes) | **Cifuentes 1992 — foundational/classical exception (rule #4): the PCC→RCC→ECC cascade is the named methodology this project makes dynamic; cited via a JOTR review article that restates the formulas** | https://indexing.jotr.eu/Jotr/Volume12/V12-5.pdf | ECC cascade computation |

---

## Cross-cutting / domain (for §5–§6)

| Paper | Link |
|---|---|
| Pekoe Trail Demand Study (IESC/USAID, 2023) | https://iesc.org/wp-content/uploads/2023/03/06.-The-Pekoe-Trail-Demand-Analysis.pdf |
| Recreational Ecology: review & gap analysis | https://www.researchgate.net/publication/334310994 |
| Camping impacts in SL dry-zone parks | https://pmc.ncbi.nlm.nih.gov/articles/PMC9132554 |
| Horton Plains GIS hiking-routes app | https://www.researchgate.net/publication/387361094 |

---

### Notes
- **Stanford CS224W** (Module 4) is a high-quality blog; for a formal reference cite the underlying STZINB-GNN paper.
- The three **foundational effort models** (Module 1) are classic textbook references, not from the literature-tracking sheet; include them to ground the Naismith/Tobler/Minetti calculation.
- **SortWaste** and **TACO** are dataset papers (useful both as citations and as training data).

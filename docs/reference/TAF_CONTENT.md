# TAF Content (J26-IT-363): paste into Template.docx

Plainer wording, no em-dashes. Facts and fixes kept. Word counts checked and noted in [brackets].

---

## Header / top table
- **Project ID:** J26-IT-363
- **Year:** 2026

## 1. Topic (12 words max)
**A Decentralised, Edge-Native AI Framework for Sustainable Hiking Tourism in Sri Lanka** [12 words]

## 2. Research group the project belongs to
**AIMS (Autonomous Intelligent Machines and Systems)**

## 3. Specialization of the project belongs to
**Information Technology (IT)**

## 4. If a continuation of a previous project
**No. This is a new project.**

---

## 5. Brief description of the research problem (300 words max) [≈275]

Sri Lanka's high-altitude trekking sector is growing fast. The 300 km Pekoe Trail and Horton Plains National Park are the main draws, and demand studies expect around 35,000 dedicated long-distance hikers a year by 2033. This growth is creating two linked problems.

The first is a carrying-capacity problem. Heavy foot traffic wears the trails down, with soil compaction, exposed tree roots, paths splitting into several braided tracks, and litter. A study of visitor satisfaction at Horton Plains (Senevirathna and Perera, 2015) found that people enjoy the experience far less once a viewpoint becomes crowded, yet weekends and holidays regularly push past that point. The sites are managed with a fixed daily permit cap that ignores where crowds actually gather, where erosion is happening, and sudden changes in weather.

The second is an information and safety gap. On remote trails the mobile signal usually drops, so hikers lose access to maps, guidance, and help exactly where the terrain is most demanding. They also have no easy way to check park rules, basic safety steps, or whether an operator's prices and "eco-friendly" claims are fair and genuine. The dense forest canopy further blocks satellite and drone monitoring, and cloud-based apps fail in these dead zones.

The problem maps onto three Sustainable Development Goals: SDG 15 (Life on Land) through physical ecosystem damage, SDG 12 (Responsible Consumption and Production) through better-informed, lower-impact and fairer tourism, and SDG 3 (Good Health and Well-being) through hiker safety in remote terrain. A low-cost, offline approach is needed to track trail conditions, guide and protect hikers, and forecast crowding, all without putting hardware into protected areas.

**References** (not counted): Senevirathna and Perera (2015), *Tourism Management Perspectives*; IESC/USAID (2023) *Pekoe Trail Demand Study*.

---

## 6. Brief description of Existing Research and Systems (300 words max) [≈285]

Today's ecotourism monitoring tools each work in a narrow area, and little of the research is built for conditions like Sri Lanka's (often called the "Global South data deficit").

For movement sensing, IMU gait studies can read terrain from the way a person walks with good accuracy, but they usually need several sensors strapped to the body in a controlled lab. Doing this reliably from one ordinary smartphone on a real tropical trail has not been solved.

For computer vision, deep-learning models measure soil erosion well, but they rely on drone or satellite images (for example PMC9915231). That approach fails under a thick tree canopy, which hides the trail surface itself, and there is no public dataset of ground-level trail damage to train on.

For on-trail guidance, digital tour guides and chatbots can answer hiker questions, but almost all of them depend on the cloud, so they stop working in the no-signal areas where hikers need them most. Running a question-answering assistant entirely offline on a phone, grounded in trusted safety and trail information, has not been done for this setting.

For forecasting, Spatio-Temporal Graph Neural Networks are the leading method for predicting crowds, but they were designed for busy city road networks with constant live data. They do not transfer easily to remote trails where there is no connection and no segment-level visitor count.

On top of this, most working systems depend on cloud servers and physical IoT sensors, which are costly, intrusive in a protected park, and useless without signal. Consumer hiking apps only handle navigation; they do not measure effort or trail health.

So there is no offline, hardware-free option covering these problems on one phone. This project fills that gap with four separate phone-based modules, each solving one problem on its own.

---

## 7. Brief description of the solution's nature, including a conceptual diagram (500 words max) [≈420]

*(Insert Figure 1, the conceptual diagram, from `architecture-diagram.html`.)*

The solution is a hardware-free system made of four separate modules that run on a hiker's smartphone. Modules 1 and 2 run live on the phone, Module 3 runs offline on text saved in advance, and Module 4 runs as a back-end service. Each module is complete on its own and does not need the others, so any one of them can be built, tested, and used by itself. Keeping the work on the phone avoids the cost of cloud servers, removes the need for sensors in the park, gets around the canopy problem, and keeps things working offline. A shared dashboard simply shows the four results together (see Figure 1).

**Module 1, Terrain and Effort.** It reads the phone's motion sensors (accelerometer and gyroscope) along with GPS distance and elevation from the barometer or a digital elevation model. A small quantised CNN-LSTM model sorts the ground into terrain types from short 2.56-second windows, with the phone kept in a known position. At the same time it works out how hard the hiker is working from distance and climb, using the Naismith and Tobler hiking formulas. It produces terrain-difficulty tags and a personal "rest or turn back" alert.

**Module 2, Vision.** It takes ground-level camera frames, sampled at one or two per second so the phone does not overheat. One INT8 YOLOv8-seg model counts litter and marks how badly the trail is damaged (erosion, exposed roots), using a ClutterScore step to ignore visual noise. It produces geotagged litter counts and a damage map.

**Module 3, Offline Hiker Assistant.** Before the hike, the app loads a curated, trusted knowledge base (park rules and permits, trail and stage guides, safety and first-aid steps, weather guidance, plants and animals, leave-no-trace advice, and verified operator and fair-price information) and turns it into a searchable on-device index. When a hiker asks a question, a local semantic search finds the relevant trusted text and a small, compressed language model writes a short, plain answer using only that text (retrieval-augmented generation), with the source shown. It runs fully offline. Output: grounded answers that act as a safety, trail, and rules guide.

**Module 4, Crowd and Carrying-Capacity Forecasting (standalone).** It uses OpenStreetMap trail maps, Copernicus GLO-30 elevation data (slope and wetness index), and historical ERA5 weather, and takes nothing from the other modules. A Spatio-Temporal Graph Neural Network predicts where and when the trail will get congested. Because real visitor counts are not published, the target is estimated from permit caps and seasonal patterns, then checked against a few days of manual counts and simpler baseline models. It produces crowding forecasts and a changing capacity limit to replace the fixed quota.

For privacy, everything is processed on the device. Only small, kilobyte-sized results (tags, scores, timestamps, GPS) are sent up when a connection returns. Raw sensor data and images never leave the phone.

---

## 8. Availability of specialized domain expertise, knowledge, and data (500 words max) [≈430]

This project needs a mix of skills: mobile and edge computing, computer vision, natural language processing, and graph machine learning. The four team members, all IT specialisation students, will build these skills by adapting existing, well-tested methods with guidance from the supervisor. The edge side, meaning shrinking models to INT8 with TensorFlow Lite or NCNN so they fit a phone's battery and heat limits, will be picked up through focused self-study.

Because local data is scarce, every module relies on transfer learning.

**Module 1** pre-trains its CNN-LSTM on open IMU datasets (Irregular and Uneven Surfaces DB under CC BY 4.0, plus UCI HAR, PAMAP2, and HuGaDB). For local data, 6 to 10 willing hikers will record about 15 to 25 hours of accelerometer, gyroscope, GPS, and barometer readings (2.56-second windows, fixed phone position, 5 or 6 terrain types) on easy practice trails and at Horton Plains. The effort estimate needs no training data because it is based on physics formulas.

**Module 2** starts its litter detector from the TACO and SortWaste datasets (CC BY 4.0). Since no public ground-level erosion dataset exists, the team will photograph and label its own set of roughly 1,000 to 2,000 on-site images (boxes for litter, masks for damage), following a clear labelling guide and reporting how well the labellers agree.

**Module 3** builds a curated knowledge base from official and open sources: Department of Wildlife Conservation rules and permits, Pekoe Trail and Horton Plains guides, standard first-aid references, weather guidance, open notes on local species, and verified operator and fair-price information. It uses an open small language model (for example a 1 to 3 billion parameter model compressed to 4-bit) with a local embedding model and vector store for retrieval. No web scraping is needed because the content is official, open, or licensed. If a phone cannot run the generative model, the app falls back to returning the best matching trusted snippet.

**Module 4** uses public map and weather data: OpenStreetMap for the trail layout (Horton Plains and the Pekoe Trail are both mapped), Copernicus GLO-30 for terrain features, and Open-Meteo or NASA POWER for weather. As the authorities do not release segment-level visitor counts, the forecast target is modelled from permit caps and seasonal trends, then calibrated with a few days of manual counts and compared against simple baselines. Standard benchmarks (METR-LA, PeMS) help transfer the method.

Ethical clearance is needed. Recording movement data and ground-level photos will follow proper informed-consent steps. Because everything is processed on the phone, raw sensor streams and images stay on the device, and only the small derived results sync. Operator scores will be published carefully, in aggregate and with a right of reply, to avoid defamation risk.

On access, the sites are reachable (Pekoe Stage 10 connects to Horton Plains), and SLTDA figures, DWC permit information, and the datasets listed above are all obtainable.

---

## 9. Objectives and Novelty

### Main Objective
Build, train, and test a set of four independent, hardware-free phone-based AI modules that help manage Sri Lankan hiking trails more sustainably. Between them they cover terrain and hiker effort, environmental damage seen through the camera, an offline hiker information assistant, and standalone crowd and carrying-capacity forecasting, and they all work offline where there is no signal.

### Member table (fill the four name cells with real names and registration numbers)

| Member (Name & Reg. No) | Sub-Objective | Tasks | Novelty |
|---|---|---|---|
| **Member 1: [Name & ID]** | Work out the terrain type from the phone's motion sensors and estimate the hiker's effort and fatigue from how far and how high they have walked, all offline on the device. | 1. Clean, normalise, and pool open IMU datasets. 2. Train a 1-D CNN-LSTM sliding-window terrain classifier (fixed phone position). 3. Add the Naismith and Tobler energy formulas for effort and fatigue. 4. Quantise to INT8 and deploy to an Android app with offline alerts. | An offline, locally trained terrain classifier for tropical trails, paired with a physics-based effort gauge, running on a single ordinary smartphone. (Unconstrained phone placement is left as a future extension.) |
| **Member 2: [Name & ID]** | Count litter and mark how badly the trail surface is damaged, on the device, even in cluttered tropical scenes. | 1. Prepare the SortWaste and TACO sets for litter pre-training. 2. Collect and dual-annotate a primary ground-level damage dataset. 3. Train one YOLOv8-seg model (detection and segmentation together). 4. Quantise to INT8 and add ClutterScore gating with frame sampling for the phone. | The first offline, ground-level model that handles both litter and trail damage in one pass and is tuned for cluttered tropical scenes, getting past the canopy limits of aerial sensing. |
| **Member 3: [Name & ID]** | Give hikers an offline question-answering assistant that provides trusted, source-grounded guidance on safety, trails, rules, and fair pricing, with no internet. | 1. Curate and structure a trusted knowledge base from official and open sources. 2. Build a local embedding index and on-device vector store for retrieval. 3. Run a compressed small language model with retrieval-augmented generation, plus a retrieval-only fallback. 4. Deploy and test the assistant offline on an Android phone. | A fully offline, on-device retrieval-augmented assistant that gives grounded, source-cited hiking guidance in no-signal terrain, unlike the cloud-dependent guides used today. |
| **Member 4: [Name & ID]** | Forecast where and when the trail will get congested and work out a changing carrying-capacity limit, as a fully standalone system. | 1. Build the OpenStreetMap trail graph and Copernicus DEM features. 2. Model foot-traffic targets from permit caps and seasonality, calibrated with short manual counts. 3. Train an ST-GNN (GCN plus temporal LSTM with attention) and compare it against simpler baselines. 4. Validate with spatial block cross-validation and derive the PCC to RCC to ECC capacity figure. | Adapting city-scale, live-data ST-GNN forecasting to a data-sparse offline trail to produce a changing carrying-capacity limit instead of a fixed quota, while being open about the synthetic-target limitation. |

---

## 10. Supervisor section
Leave for the supervisor and co-supervisor. Note: identifying a **co-supervisor is compulsory at this stage**, so arrange one before submitting.

---

### Still to fill in before submission
- [ ] Four member names and registration numbers (objectives table)
- [ ] Confirm research group (AIMS) and Year (2026)
- [ ] Co-supervisor identified
- [ ] Figure 1 inserted in Section 7 (from `architecture-diagram.html`)
- [ ] Re-check each word count after edits (limits: §5 300, §6 300, §7 500, §8 500)

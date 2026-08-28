# Supervisor Presentation Script — J26-IT-363
### A Decentralised, Edge-Native AI Framework for Sustainable Hiking Tourism in Sri Lanka

**How to use this:** read it out or put it in your own words. Each component has the same seven parts in a natural presenting order. The language is kept simple on purpose. Every component ends with one honest limitation, because supervisors usually ask about that.

---

## 30-second opening (say this first)

"Our project tackles a growing problem on Sri Lankan hiking trails like the Pekoe Trail and Horton Plains. As more people hike, the trails get damaged, crowds build up at the same spots, and hikers are often left with no reliable information or help once they lose phone signal. The current control is a fixed daily ticket limit that ignores real conditions. We are building four small AI tools that run on a normal smartphone, offline, with no equipment installed on the mountain. Each tool solves one part of the problem on its own, and together they support both the hiker and the park managers. Each of us owns one tool as our individual final-year project."

Then present the four components.

---

# Component 1 — Terrain and Effort (the phone "feels" the trail)

### What it does (plain terms)
This tool uses the motion sensors already inside a phone to work out two things while you walk: what the ground is like (flat, rocky, muddy, steps, steep slope) and how tired the hiker is getting. It needs no extra device and no internet.

### Why we proposed it
Trail managers have no cheap way to know which parts of a trail are rough, slippery, or eroding, and hikers have no warning before they over-exert on a long climb. Putting sensors on the mountain is expensive and intrusive. Almost everyone already carries a phone, so the phone becomes a free, moving sensor.

### Where the research is now
Reading terrain and walking style from motion sensors is well proven, but almost always in a lab, with several sensors strapped to the body, and to study the person (for example medical gait analysis), not the trail. Doing it from a single phone, on a real tropical trail, and turning it around to describe the ground rather than the walker, has not really been done. Estimating effort is simpler: it is a known physics calculation from how far and how high you climb.

### A few key papers
- Outdoor walking classification from IMU and foot pressure (PMC, 2025): shows phone-grade motion sensors can tell apart flat ground, stairs, and slopes with high accuracy. https://pmc.ncbi.nlm.nih.gov/articles/PMC12788207
- Automating gait analysis using a smartphone (Aberystwyth PhD thesis, 2023): proves a single phone at a low sampling rate, using short 2.56-second windows, is enough for accurate surface classification while saving battery. https://pure.aber.ac.uk/ws/portalfiles/portal/74587204/Sher_Arshad.pdf
- Gait recognition with TinyML on an IMU (arXiv 2507.18627, 2025): demonstrates these models can be shrunk to run directly on tiny, low-power hardware. https://arxiv.org/html/2507.18627v1
- Effort grounding: Minetti et al. (2002) on the energy cost of walking up and down slopes gives the formula behind the fatigue estimate. https://journals.physiology.org/doi/10.1152/japplphysiol.01177.2001

### The data and how we get it
- To teach the model, we start from free public motion datasets (Irregular and Uneven Surfaces DB, UCI HAR, PAMAP2, HuGaDB).
- For local conditions we collect our own: 6 to 10 volunteer hikers carry a phone in a fixed waist position and record about 15 to 25 hours of walking on easy practice trails and at Horton Plains. We film or note the terrain as we go, so each short slice of sensor data gets a correct label (rocky, muddy, and so on).
- The effort part needs no training data, because it is a physics formula using GPS distance and the climb measured by the phone's barometer.

### How it works, step by step (simple)
1. The phone records motion about 50 times a second from its accelerometer and gyroscope.
2. We clean the signal (remove odd spikes) and scale it to a standard range.
3. We cut it into short 2.56-second windows.
4. A small neural network (a CNN-LSTM) learns the motion "signature" of each terrain type and labels every window.
5. Separately, the app adds up distance and elevation gain and uses the Naismith and Tobler formulas to estimate how much energy the hiker has spent, which becomes a fatigue level.
6. The model is compressed (INT8 quantisation) so all of this runs on the phone, offline, without draining the battery.

### What it produces
A live label of the terrain underfoot, plus a personal fatigue gauge that gives a "rest or turn back" alert. Trail-difficulty summaries can be saved for managers.

### Honest limitation (if asked)
If the phone is held in many different ways, accuracy drops, so our first version fixes the phone position. Handling any phone position is a planned extension, not the first goal.

---

# Component 2 — Trail Damage and Litter (the phone "sees" the trail)

### What it does (plain terms)
Using the phone camera, this tool spots and counts litter and marks where the trail surface is damaged (soil washed away, exposed tree roots, the path widening into several tracks). It runs offline on the phone.

### Why we proposed it
Satellites and drones cannot see the ground under a thick forest canopy, which is exactly where Sri Lankan trail damage happens. Park staff currently measure damage by hand with tapes, which is slow. A hiker's camera sees the ground from the side, which is the view that actually matters.

### Where the research is now
Detecting litter with AI is mature, and measuring soil erosion with AI exists too, but the erosion work relies on overhead drone or satellite images that the canopy blocks. There is no public dataset of ground-level trail damage, and no offline phone tool that does both litter and damage together in cluttered forest scenes.

### A few key papers
- Plastic-bottle detection with YOLOv8 and tracking (Scientific Reports, 2025): high-accuracy litter detection and counting in messy outdoor scenes. https://www.researchgate.net/publication/393587342
- SortWaste dataset and "ClutterScore" (arXiv 2601.02299, 2026): a large labelled waste dataset and a way to measure how visually messy a scene is, so the model can ignore noise. https://arxiv.org/abs/2601.02299
- Forest trail-degradation prediction with explainable AI (MDPI Forests, 2025): uses Random Forest with SHAP so managers can see why a trail spot is flagged as high-risk. https://www.mdpi.com/1999-4907/16/7/1074
- CNN soil-erosion mapping (PMC9915231, 2023): a good example of the aerial approach we are replacing with a ground-level one. https://pmc.ncbi.nlm.nih.gov/articles/PMC9915231

### The data and how we get it
- For litter, we start from free labelled datasets (TACO, SortWaste).
- For damage, no public dataset exists, so we build our own: about 1,000 to 2,000 ground-level photos taken on the trails, labelled by hand (boxes around litter, painted masks over erosion and roots), following a clear guide so labellers agree.
- We can also borrow general off-road terrain datasets (such as RUGD and GOOSE) to give the model a head start.

### How it works, step by step (simple)
1. The camera grabs one or two frames a second (not full video, so the phone does not overheat).
2. One model (YOLOv8-seg) looks at each frame and does two jobs at once: it draws boxes around litter and counts it, and it paints which parts of the ground are damaged.
3. A "ClutterScore" check skips frames that are too messy or blurry, so leaves and shadows do not cause false alarms.
4. The model is compressed (INT8) to run on the phone.
5. An explainability step (SHAP) can show managers which features drove a "damaged" decision.

### What it produces
A litter count and a trail-damage map, each tagged with GPS location. Only small result files are kept, which sync to a dashboard later when there is signal.

### Honest limitation (if asked)
Labelling "damage" is partly subjective, so we will publish how strongly our labellers agree, and litter detection will be more accurate than damage segmentation at first.

---

# Component 3 — Offline Hiker Information Assistant (the phone "answers" questions)

### What it does (plain terms)
This is an offline question-and-answer assistant for hikers. With no internet, a hiker can ask things like "how hard is the next section", "what should I do for a leech bite", "is it safe to keep going if it rains", "what is this plant", "what are the rules in this park", or "is this a fair price", and the app gives a short, reliable answer from trusted information loaded in advance.

### Why we proposed it
On remote trails the mobile signal usually drops, so normal apps and online chatbots stop working at the exact moment a hiker needs guidance or help. A human guide is not always available. This puts a dependable guide in everyone's pocket, completely offline. It is safer than a generic online chatbot because every answer is built from trusted, pre-loaded content rather than guesswork.

### Where the research is now
The technique is called Retrieval-Augmented Generation, or RAG: the app looks up the relevant trusted text first, and a language model turns it into a clear answer. RAG and small "on-device" language models are improving fast, but almost all travel and guide assistants still rely on the cloud. Running the whole thing offline on a phone, for a safety-critical wilderness setting, is the new and useful part. Recent small models (a few billion parameters, compressed to 4-bit) now fit on modern phones, which is what makes this possible.

### A few key papers
- Retrieval-Augmented Generation (Lewis et al., 2020): the original method of grounding a language model's answers in retrieved documents so it does not make things up. https://arxiv.org/abs/2005.11401
- Sentence-BERT (Reimers and Gurevych, 2019): the method behind fast "meaning" search that finds the right passage in the knowledge base. https://arxiv.org/abs/1908.10084
- TOURGURU tour-guide app (SLIIT): a local example that already summarises landmark information and plays it to tourists, showing the demand for on-the-go guidance. https://www.researchgate.net/publication/341757650
- Offline reinforcement learning for visual navigation, ReViND (arXiv 2212.08244, 2022): part of the broader push toward AI that works without a live connection in the field. https://arxiv.org/abs/2212.08244

### The data and how we get it (the knowledge base)
The "knowledge" is a curated, trusted library packaged with the app at download, not scraped from the open web. It includes:
- Official park rules, permit information, and emergency contacts (for example from the Department of Wildlife Conservation).
- Trail and stage guides for the Pekoe Trail and Horton Plains.
- Safety and first-aid guidance for common trail problems (leeches, sprains, hypothermia, getting lost).
- Weather guidance, and short notes on local plants and animals.
- Leave-no-trace and responsible-hiking advice.
- Verified operator and permit details, and typical fair prices, so a hiker can quickly check they are not being overcharged.
All of this comes from official documents, the trail's own materials, standard first-aid references, and open sources, so there are no scraping or copyright problems. We turn this library into a searchable index inside the app.

### How it works, step by step (simple)
1. Before the hike, the app loads a curated knowledge library and converts each piece of text into a numeric "meaning fingerprint" (an embedding), stored in a small database on the phone.
2. When the hiker asks a question, the app turns the question into the same kind of fingerprint and finds the most relevant pieces of the library. This is a local semantic search.
3. A small, compressed language model reads those pieces and writes a short, plain answer, and it shows which source the answer came from.
4. Because the answer is built only from the retrieved trusted text, it avoids inventing facts, which matters for safety.
5. Everything runs on the phone with no signal. Voice input and read-aloud can be added for hands-free use.

### What it produces
Short, trustworthy answers to hiker questions, offline, each with its source shown. In practice it acts as a safety helper, a trail guide, and a rules-and-nature guide in one app.

### Honest limitation (if asked)
Generative models are heavy, so on low-end phones we may use a smaller model or fall back to simply showing the best matching trusted snippet (retrieval-only mode). The assistant is also only as good as the library we curate, so keeping that content accurate and current is part of the work.

---

# Component 4 — Crowd and Carrying-Capacity Forecasting (the "brain" for managers)

### What it does (plain terms)
This tool predicts where and when a trail will get crowded, hours in advance, and recommends a smart, changing limit on how many people to admit, instead of today's fixed daily number. It is a standalone system and does not depend on the other three components.

### Why we proposed it
A fixed daily ticket cap is blind. It does not know that rain makes the same number of hikers do more damage, or that everyone crowds the one famous viewpoint at the same hour. Managers need to see crowding before it happens and adjust.

### Where the research is now
The method we use, Spatio-Temporal Graph Neural Networks, is the leading way to forecast crowds and traffic, but it was built for cities with constant live data feeds. It has not been adapted to remote trails that have no connection and no per-spot visitor counts. Carrying capacity itself has a well-known formula (Cifuentes), which we make dynamic instead of a one-time estimate.

### A few key papers
- Spatio-Temporal Pivotal Graph Neural Network (AAAI, 2024): a current state-of-the-art model for predicting how congestion spreads through a network. https://ojs.aaai.org/index.php/AAAI/article/view/28707
- GCN-LSTM for tourism-flow networks (Informatica, article 10973): applies these graph models specifically to tourist movement, not just city traffic. https://www.informatica.si/index.php/informatica/article/view/10973
- Forecasting daily foot traffic on recreational trails (ResearchGate, 2023): shows weather and seasonality can predict trail visitor numbers, which guides our inputs. https://www.researchgate.net/publication/375226880
- Social carrying capacity at Horton Plains (Senevirathna and Perera, 2015): local evidence that satisfaction collapses once a viewpoint is crowded, which sets our target. https://www.sciencedirect.com/science/article/abs/pii/S2211973615000781

### The data and how we get it
- The trail map comes from OpenStreetMap (both Horton Plains and the Pekoe Trail are already mapped).
- Terrain features (slope, wetness) come from a free elevation model (Copernicus GLO-30).
- Weather, current and historical, comes from free services (Open-Meteo, NASA POWER).
- Real per-spot visitor counts are not published, so we estimate them from the permit cap multiplied by seasonal patterns, and we check this against a few days of manual counts at the entrance and the busy viewpoints.

### How it works, step by step (simple)
1. We turn the trail into a network: points are viewpoints and junctions, lines are the paths between them.
2. We attach information to each point: slope, wetness, the weather, the time of day, and the season.
3. A Spatio-Temporal Graph Neural Network learns how a crowd at one point flows to the next over time.
4. It predicts where and when bottlenecks will form, hours ahead.
5. We convert that forecast into a changing capacity number using the Cifuentes formula, tightening the limit when the trail is wet or already eroding.
6. We compare the model against simple methods to prove the graph model genuinely adds value.

### What it produces
A crowding and bottleneck forecast, and a recommended dynamic admission limit for park administration, which replaces the fixed daily quota.

### Honest limitation (if asked)
Because real visitor counts are not available, we train on an estimated (synthetic) figure calibrated with short manual counts. We will say this clearly and validate carefully rather than overstate accuracy.

---

## Closing line (say this last)

"In short, the first two tools read the trail, the third answers the hiker's questions offline, and the fourth forecasts crowding for managers on its own. Each is a complete project a single member can build, test, and defend, and each works offline with no hardware on the mountain. Together they help the hiker stay safe and informed, and they move the park from a blind fixed quota to a live, evidence-based view."

---

### Quick reference: one line per component
- **C1 Terrain and Effort:** phone motion sensors read the ground type and a physics formula estimates fatigue.
- **C2 Trail Damage and Litter:** phone camera counts litter and maps trail damage, offline.
- **C3 Offline Hiker Assistant:** an on-device language model answers hiker questions from a trusted, pre-loaded knowledge base (RAG), with no internet.
- **C4 Crowd Forecasting:** a graph model predicts crowding and recommends a changing capacity limit, standalone.

---

### If the supervisor asks the common cross-cutting questions
- **"Why four separate tools and not one system?"** Each is a full final-year project for one member, and keeping them independent means no one is blocked if another slips. A shared dashboard can still show all four together.
- **"Does everything really run offline?"** Components 1 and 2 run live on the phone. Component 3 runs on a knowledge base saved in advance. Component 4 runs on a laptop or server from open map and weather data. None needs signal on the trail; results sync later as tiny files.
- **"What is genuinely new here?"** Doing all of this on an ordinary phone, offline, tuned for Sri Lankan tropical trails, with no hardware installed in the park. Each component closes a specific gap that existing lab, cloud, or aerial methods leave open.
- **"Is the scope realistic?"** Yes, if each member builds a focused first version (the MVP) and treats the harder features as extensions. We have named the honest limitations up front.

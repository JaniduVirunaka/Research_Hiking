# Module 4 — Datasets & Resources Plan

Owner: IT23343948 — Weerasekara J.V. Working doc for the actual data-acquisition and
compute/tooling plan behind Module 4 (Crowd & Carrying-Capacity Forecasting, ST-GNN). Builds on
`docs/PROJECT_PROPOSAL.md` §5 "Module 4" and §7 "Consolidated Dataset Plan" — those sections
establish *which* datasets to use and their specs (already verified, see `docs/SOURCES_LOG.md`);
this doc is the next layer down: *how* to actually get each one onto disk in a usable form, and
what compute/tooling the pipeline runs on. Per CLAUDE.md rule #3, every access claim below is
either independently verified (marked accordingly) or explicitly flagged as unverified/TODO — do
not treat an unflagged claim as confirmed until it carries a verification note.

**Status:** Compute/tooling, storage, and per-dataset access mechanics (§§1–3) are complete as of
2026-08-29 — see `docs/SOURCES_LOG.md` for the full verification log. §4 "Open questions" lists
what's deliberately still open. This doc has not yet been checked by the supervisor-agent against
project scope/governance rules — do that before treating it as final.

---

## 1. Compute plan

**Decision (this session, 2026-08-29): free-tier cloud compute plus this local development
machine, no paid compute assumed.** The Horton Plains World's End graph is tiny by GNN standards
(~25–40 nodes, ~9,000 hourly timesteps per node) — this is nowhere near the scale that requires
paid GPU time, so a zero-budget plan is realistic, not a compromise.

### 1.1 Local machine specs (verified via direct query, 2026-08-29)

| Component | Spec | Verification |
|---|---|---|
| CPU | AMD Ryzen 5 5600G, 6 cores / 12 threads | `Get-CimInstance Win32_Processor`, direct query |
| RAM | ~19.9 GB | `Get-CimInstance Win32_ComputerSystem`, direct query |
| GPU | AMD Radeon RX 7600 XT, **16 GB VRAM** (confirmed via registry `HardwareInformation.qwMemorySize`, not the unreliable 32-bit WMI `AdapterRAM` field, which under-reports as ~4 GB) | Registry query, direct, 2026-08-29 |
| OS | Windows 10 Pro, 64-bit (current) — **upgrade to Windows 11 22H2+ unlocks native ROCm GPU support for this card, see below** | Direct query |

**Implication — the GPU is AMD, not NVIDIA.** PyTorch's default CUDA acceleration path does not
run on this card on Windows 10. **Verified update (2026-08-29): this is fixable by upgrading to
Windows 11.** AMD's official ROCm HIP SDK Windows GPU support table
(`https://rocm.docs.amd.com/projects/install-on-windows/en/latest/reference/system-requirements.html`,
fetched directly) lists the **Radeon RX 7600 XT (gfx1102) as officially supported** for both
Runtime and HIP SDK — confirmed by name, not inferred from "RDNA3 generally." The one requirement
is the OS: **Windows 11, version 22H2 or later** is the documented minimum; ROCm on Windows 10 is
not in AMD's supported matrix at all. This directly confirms the user's own note that a Windows 11
upgrade removes the GPU limitation, rather than it being a permanent constraint of the hardware.

Given that, the realistic options are:

1. **CPU-only training on the Ryzen 5600G, as the default regardless of OS.** At ~25–40 nodes and
   ~9,000 timesteps, a GCN+LSTM/Transformer ST-GNN and the baseline models (per-node LSTM, ARIMA,
   historical-average) are all small enough that CPU training is plausible within minutes-to-low-
   hours per run, not days — this is not an ImageNet-scale workload. **Recommended default**
   regardless of OS, since ARIMA/historical-average have no GPU path anyway and the graph is small
   enough that GPU speedup may not even be noticeable for the GCN/LSTM pieces.
2. **Native ROCm + PyTorch on this machine, once/if it's upgraded to Windows 11 22H2+.** This is
   now the recommended GPU path if GPU acceleration is ever wanted (e.g. for faster hyperparameter
   search) — confirmed officially supported for this exact card, and keeps everything local rather
   than depending on a cloud session. Follow AMD's own HIP SDK Windows install docs
   (`https://rocm.docs.amd.com/projects/install-on-windows/en/latest/`) when/if the OS upgrade
   happens; do not attempt this on the current Windows 10 install, since it is outside AMD's
   supported matrix.
3. **Free-tier cloud GPU (Google Colab free tier or Kaggle Notebooks free GPU quota)** remains the
   fallback if staying on Windows 10, or if a cloud session is simply more convenient than a local
   ROCm setup. Both offer free NVIDIA T4-class GPUs with session limits (Colab: ~12h/session with
   usage-based throttling; Kaggle: 30h/week GPU quota) — more than sufficient for a graph this
   small.

**Explicit conclusion: no paid compute is required or recommended for Module 4's scope**, on
either OS. If a paid tier is ever considered later (e.g. Colab Pro, ~$10/month), it should be
justified by an actual observed bottleneck (e.g. free-tier session limits interrupting a real
training run), not provisioned speculatively.

### 1.2 Software stack (to verify/pin during implementation, not yet installed)

| Layer | Candidate tools | Notes |
|---|---|---|
| Graph extraction | `osmnx` or `pyrosm` (Python) | Converts OSM data to a routable graph; osmnx is the more commonly documented option for pedestrian/path networks — verify current version compatibility when implementation starts |
| DEM processing | `rasterio`, `richdem` or `pysheds`, QGIS (GUI, optional) | `pysheds` and `richdem` both compute TWI; pick one during implementation based on which has cleaner docs for the exact `TWI = ln(a/tan β)` formula already specified in the proposal |
| Weather ingestion | `requests`/`openmeteo-requests` (Python client), plain HTTP for NASA POWER/CHIRPS | See §2.3 below for verified endpoints |
| ST-GNN implementation | PyTorch + PyTorch Geometric (PyG), or PyTorch Geometric Temporal specifically (has built-in spatio-temporal layers) | PyTorch Geometric Temporal is purpose-built for exactly this task (GCN+LSTM-style layers) — worth checking during implementation whether it has AMD/CPU-only wheels or requires CUDA-only extensions |
| Baselines | `statsmodels` (ARIMA), plain NumPy/pandas (historical-average), PyTorch or `scikit-learn`-adjacent for per-node LSTM | All CPU-friendly, no GPU dependency |
| Cifuentes cascade | Plain Python — it's a deterministic formula chain, no ML library needed | Confirmed in `docs/PROJECT_PROPOSAL.md` §5.5: "a formula application, not a model output" |

*This table is a starting point for implementation, not a final pinned dependency list — exact
versions should be locked in a `requirements.txt`/`environment.yml` once implementation begins,
and any library-specific AMD/CPU compatibility issue found during setup should be logged here.*

---

## 2. Data storage and versioning

**Decision (this session, 2026-08-29): store all Module 4 data artifacts directly in the git
repository, not an external service.** Justification: every dataset in Module 4's pipeline is
either (a) a small extracted graph/feature table (the OSM graph, DEM-derived node features,
weather time series for one small bounding box) or (b) generated locally (the synthetic
occupancy series, calibration counts) — none involves raw imagery or large binary corpora the way
Module 2's vision data does. Estimated total size is low tens of MB at most, well within normal
git repo hygiene.

**Practical layout (to create when implementation starts, not yet created):**
- `module4/data/raw/` — original downloaded extracts (OSM `.pbf`/`.osm.xml`, DEM GeoTIFF tiles,
  raw weather API responses) — commit these as-is so the pipeline is reproducible without
  re-hitting external APIs every time.
- `module4/data/processed/` — the built graph (adjacency + node/edge feature tables), the
  synthetic occupancy series, and the manual calibration-count sample once collected.
- `module4/scripts/` — the extraction/build scripts (Overpass query script, DEM feature builder,
  weather puller, synthetic-target generator) — these are what make `raw/` reproducible, so they
  matter as much as the data itself.

**Open item, deliberately not decided yet:** exact repo sub-path naming and whether Module 4's
data lives in a per-module subfolder of a shared monorepo or its own folder — depends on how the
four modules' codebases end up structured relative to each other, which hasn't been decided at
the whole-team level yet. Revisit once the shared git repository (the PP1 status-doc deliverable
per `docs/reference/GOVERNANCE_SUMMARY.md` §4) is actually being set up.

---

## 3. Per-dataset access mechanics

Verified 2026-08-29 via a dedicated research pass (see `docs/SOURCES_LOG.md` for the full log
entry). Verification strength is marked per item: **[LIVE]** = a real request was made against the
real endpoint and returned real data — the strongest evidence short of doing it yourself.
**[PRIMARY-DOC]** = the vendor's own documentation/landing page was fetched directly.
**[SEARCH-XCHECK]** = corroborated only via search snippets because a direct fetch failed or
wasn't attempted — weaker, flagged as such, re-verify before depending on it for real code.

### 3.1 OSM trail graph (Horton Plains + Pekoe Trail)

- **Overpass API — [LIVE].** Endpoint `https://overpass-api.de/api/interpreter`. A real query for
  `highway=path/footway/track` ways in a Horton Plains bounding box returned real, valid JSON
  (Overpass 0.7.62.11) including a way literally named "World's End Loop"
  (`highway=track, surface=ground, tracktype=grade4`) and "Horton Plains Visitor Center"
  (`highway=path, sac_scale=hiking`) — about as strong a confirmation as is possible without
  running it yourself. No authentication required.
- **Rate limits [PRIMARY-DOC]:** soft fair-use guidance of ~10,000 requests/day and <1GB/day;
  requests from the same IP are serialized; a request queued >15s gets HTTP 429. This is fair-use
  guidance, not a hard contractual quota — not a concern for occasional bbox pulls.
- **Format:** OSM JSON by default with `[out:json]` (not GeoJSON — Overpass does not natively emit
  GeoJSON; a converter step is needed if GeoJSON is wanted downstream).
- **Recommended tooling — confirmed against current osmnx docs:** `osmnx.graph.graph_from_bbox(bbox,
  network_type='walk', custom_filter=...)` (or `graph_from_place(...)`) calls Overpass internally
  and returns a ready-to-use `networkx.MultiDiGraph` directly — no manual XML/JSON parsing needed.
  `network_type='walk'` is the correct value for a hiking trail graph. `pyrosm` is the offline
  alternative, parsing a downloaded `.osm.pbf` instead of hitting the live API — a good fallback if
  Overpass is ever unavailable or fully-offline/reproducible extraction is preferred.
- **Geofabrik Sri Lanka extract — [LIVE for the landing page].** URL:
  `https://download.geofabrik.de/asia/sri-lanka-latest.osm.pbf`. The landing page confirms **137
  MB**, data current to 2026-08-27, updated roughly daily (close to, and consistent with, the 136
  MB already in `docs/PROJECT_PROPOSAL.md` — the small difference is expected ongoing OSM growth,
  not a discrepancy). ODbL license (confirmed directly from `openstreetmap.org/copyright`), no auth
  needed. **Caveat:** a direct fetch of the binary `.pbf` file itself returned HTTP 502 through the
  fetch tool used — most likely a tool-side limitation handling binary content, not evidence the
  file is broken (the landing page linking to it resolved fine with a plausible current size/date).
  A human should confirm with a real download (`curl -I` or an actual pull) before depending on it
  in a script.
- **Unverified, do not rely on without a follow-up check:** a claimed list of alternate Overpass
  mirrors (VK Maps, "FairwayMapper", "Overspan", a private.coffee instance) came only from an
  AI-summarized fetch of the OSM wiki page, not independently confirmed one-by-one. The primary
  `overpass-api.de` endpoint is solid regardless — this only matters if a backup mirror is needed.

### 3.2 DEM / terrain (Copernicus GLO-30, SRTM GL1/NASADEM)

- **OpenTopography API — [LIVE, including a negative result].** Endpoint
  `https://portal.opentopography.org/API/globaldem` (params: `demtype`, `south`/`north`/`west`/
  `east`, `outputFormat`, `API_Key`). A direct request with a bbox around Horton Plains and a fake
  key returned **HTTP 401 Unauthorized** — confirming both that the endpoint/parameters are exactly
  right (it got far enough to check auth, not a 404) and that **a real API key is genuinely
  required, which the proposal did not previously flag.** A free key is simple to obtain
  (self-service via the portal's "My Account"), but budget for the step. **Rate limits:** 200
  calls/24h for academic accounts, 50/24h otherwise, plus per-dataset area-size caps — trivially
  sufficient for a one-time ~25–40 node Horton Plains extract. Dataset codes confirmed present:
  `SRTMGL1`, `SRTMGL3`, `NASADEM`, `COP30`, `COP90`. Format: GeoTIFF (`outputFormat=GTiff`).
- **Better default for Copernicus GLO-30 specifically — [LIVE-adjacent, PRIMARY-DOC].** The public
  AWS Open Data bucket `s3://copernicus-dem-30m/` allows **anonymous read access, no AWS account or
  API key at all** (confirmed via the bucket's own readme and the AWS Open Data Registry page).
  Format: Cloud-Optimized GeoTIFF. Tile naming follows
  `Copernicus_DSM_COG_10_N<lat>_00_E<lon>_00_DEM/` (the "10" is an internal 10-arcsecond processing
  reference, not the delivered 30 m product — this naming pattern was read from the bucket's readme
  text, not confirmed against an actual tile listing, so do a quick real `aws s3 ls
  s3://copernicus-dem-30m/ --no-sign-request` check before writing extraction code against it).
  **Recommendation: use this S3 mirror for GLO-30 to skip the OpenTopography API-key/rate-limit
  step entirely.** SRTM GL1/NASADEM have no equivalent no-key public bucket found — use the
  OpenTopography API (with the free academic key) for those if they're ever needed instead of/
  alongside GLO-30.
- **SRTM accuracy in mountainous terrain — [PRIMARY-DOC + SEARCH-XCHECK, partially unresolved].**
  USGS EROS confirms void-filled SRTM products exist because the original radar processing failed
  quality checks in some areas — well-established for steep terrain generally. A search found
  Indian Himalaya studies showing SRTM vertical RMSE degrading from ~3.55 m (plains) to ~19.64 m
  (highly undulating terrain). **No Horton Plains/Sri-Lanka-central-highlands-specific accuracy
  figure was found** despite a dedicated search — this is a real, stated gap, not a confirmed local
  fact. Treat the accuracy caveat as a reasonable extrapolation from general mountainous-terrain
  literature, not a site-specific measurement. **This is the concrete reason to prefer Copernicus
  GLO-30 over SRTM GL1 as the default DEM source** — GLO-30 fuses newer TanDEM-X radar
  interferometry, generally more accurate than the original 2000 SRTM mission, though this
  preference is a reasoned inference, not itself a directly-measured Horton-Plains comparison.

### 3.3 Weather (Open-Meteo/ERA5, NASA POWER, CHIRPS)

- **Open-Meteo Historical/Archive API — [LIVE].** Endpoint
  `https://archive-api.open-meteo.com/v1/archive`. A real query for Horton Plains' coordinates
  returned real hourly JSON (temperature, precipitation), with the API reporting elevation ≈2,108 m
  — consistent with Horton Plains' actual elevation, a good internal sanity check that the returned
  ERA5 grid cell genuinely represents the highland location rather than a coarser, lower-elevation
  proxy. **No API key required** for non-commercial use (confirmed directly from Open-Meteo's own
  pricing page), rate-limited to 10,000 calls/day. Data: ERA5 (1940–present, 0.25°) and ERA5-Land
  (1950–present, 0.1°), updated daily with a ~5-day lag. Format: JSON by default (CSV/XLSX also
  offered).
- **NASA POWER API — [LIVE, with an important data-quality finding].** Endpoint confirmed working:
  `https://power.larc.nasa.gov/api/temporal/hourly/point` (params `parameters`, `community`,
  `longitude`, `latitude`, `start`, `end`, `format`). A real query returned valid JSON (API v2.9.9)
  with real MERRA-2-sourced values, no auth needed. **New finding: NASA POWER reported the grid
  elevation at the same Horton Plains coordinates as only ~681 m, versus Open-Meteo/ERA5's ~2,108 m
  at essentially the same lat/lon** — because POWER runs on the coarser MERRA-2 reanalysis grid
  (~50 km cells), which badly averages out Horton Plains' real elevation. **Recommendation: treat
  NASA POWER as a secondary/cross-check source only, not primary, for this project** — Open-Meteo/
  ERA5 is materially better-resolved for a site this dependent on real terrain-driven weather
  effects (rain → TWI → trail behaviour). This is a new, concrete reason to prefer one source over
  the other, not previously stated in the proposal.
- **CHIRPS rainfall — [LIVE].** Portal `https://data.chc.ucsb.edu/products/CHIRPS-2.0/`, a directly
  browsable Apache directory index, no login. Confirmed `global_daily/tifs/p05/` exists — "p05" =
  0.05° resolution, matching the proposal's stated spec — GeoTIFF format, data spans 1981 through
  at least 2026-08-14 (actively maintained). **No Sri-Lanka-specific regional subfolder exists**
  (regional convenience subsets exist for Africa, Central America/Caribbean, Indonesia, western
  hemisphere, but not South Asia) — pull from the `global_daily` product and clip to the Horton
  Plains bbox locally, a minor extra processing step not previously called out.

### 3.4 Prototyping benchmarks (METR-LA, PEMS-BAY, PeMS04, PeMS08)

This is where the most actionable findings are — **the "canonical" sources for these benchmarks
are fragile; better, actively-maintained mirrors exist and should be used instead.**

- **METR-LA / PEMS-BAY — fragile at the source, use a library loader instead.** The
  most-cited original source (`github.com/liyaguang/DCRNN`) points to a Google Drive link and a
  Baidu Yun (Chinese cloud storage) link for the actual `.h5` files, not files in the repo itself —
  **neither link was directly opened/confirmed live** [unverified, flag before depending on it].
  **Recommended path instead: PyTorch Geometric Temporal** (`benedekrozemberczki/
  pytorch_geometric_temporal`) ships built-in dataset loader classes — `METRLADatasetLoader` and
  `PemsBayDatasetLoader` — that handle download and preprocessing automatically, confirmed present
  in the library's current documentation. Prefer this over chasing the raw Drive/Baidu links.
- **PeMS04 / PeMS08 — [LIVE].** The maintained, currently-populated source is
  `github.com/Davidham3/ASTGCN/tree/master/data/PEMS04` (and `/PEMS08`) — directly fetched and
  confirmed real files present (`distance.csv`, `pems04.npz` — an actual NumPy array file, not a
  placeholder), on a repo with 428 stars / 246 forks indicating active community reliance. **Use
  this as the source.**
- **IEEE DataPort mirror — confirmed dead, do not use [LIVE negative result].** Directly fetched
  `ieee-dataport.org/documents/pems04-and-pems08-traffic-flow-datasets...` — it explicitly states
  "Files have not been uploaded for this dataset" and requires an IEEE subscription/login even to
  attempt. Genuinely broken, not just gated — do not reference this as a source.
- **Hugging Face `Salesforce/lotsa_data`** was reported by search results as also containing
  PEMS04/PEMS08 — **not independently fetched/confirmed** [search-cross-check only]. A plausible
  lead (Salesforce's LOTSA time-series corpus is real and published) but verify directly before
  relying on it as a mirror.

### 3.5 Transfer-analogue visitation data (NPS IRMA, Eco-Counter)

- **NPS Visitor-Use Statistics — [LIVE, via a better path than the interactive portal].** Direct
  fetches to the interactive `irma.nps.gov/STATS/...` query-builder pages returned only page chrome
  with no data — this is because that site is a JavaScript-rendered application the fetch tooling
  used cannot execute, not evidence the data is unavailable. **The same data is also published as a
  static download package on data.gov**, which was fetched directly with real content returned:
  `catalog.data.gov/dataset/nps-visitor-use-statistics-data-package-2025` — **CC0 license**, three
  real files listed (`Main_Data.csv` covering 1979–2025, `Main_State_Data.csv` covering 2016–2025,
  plus an XML metadata file), package last updated 2026-03-26. **Recommendation: use this data.gov
  CSV package directly rather than the interactive IRMA query builder** — fully public-domain,
  no login, no key, and far more scriptable. A search cross-check also found a working
  direct-file-download URL pattern on the `irma.nps.gov` domain itself
  (`irma.nps.gov/DataStore/DownloadFile/<id>`), corroborating that direct downloads exist there too.
- **Eco-Counter (Austin analogue) — [LIVE].** The Socrata Open Data API endpoint
  `https://data.austintexas.gov/resource/26tt-cp67.json` was queried directly and returned real
  JSON records (`date`, `sensor_id`, `sensor_name`, `count`, `record_id` — e.g. a real record for
  "Shoal Creek Blvd at 38th St PC", count 221, dated 2024-06-26). No authentication needed; standard
  Socrata (SODA) query syntax supported (`$limit`, `$where`, date filters). Confirms this transfer
  dataset is genuinely live and pullable right now in clean tabular JSON/CSV, no scraping needed.

### 3.6 Foot-traffic synthetic target and manual calibration counts
This one has no external "access" step — it is generated locally per the methodology already
specified in `docs/PROJECT_PROPOSAL.md` §5 Module 4 and §5.5 Phase 2 (permit-cap × SLTDA-
seasonality × Tobler-movement-model pipeline). The manual/clicker calibration counts (§5.5 Phase 3)
are a field-collection task, not a data-download task — see `docs/TECHNICAL_AUDIT.md`'s point on
ethics/permits being a first-week milestone, not a footnote, before planning an actual Horton
Plains site visit.

### 3.7 Consolidated link table

Every external data source and tool referenced above, in one place, as clickable links. Verified-
live links are marked; unverified ones are marked so they get a follow-up check before use, not
mistaken for confirmed.

| Source | Link | Verified |
|---|---|---|
| Overpass API (query endpoint) | [overpass-api.de/api/interpreter](https://overpass-api.de/api/interpreter) | Yes — live query returned real Horton Plains data |
| Overpass API status/fair-use policy | [overpass-api.de/api/status](https://overpass-api.de/api/status) / [wiki.openstreetmap.org/wiki/Overpass_API](https://wiki.openstreetmap.org/wiki/Overpass_API) | Yes (status), partial (mirror list unverified) |
| Geofabrik Sri Lanka extract | [download.geofabrik.de/asia/sri-lanka-latest.osm.pbf](https://download.geofabrik.de/asia/sri-lanka-latest.osm.pbf) (landing page: [download.geofabrik.de/asia/sri-lanka.html](https://download.geofabrik.de/asia/sri-lanka.html)) | Landing page yes; binary file fetch inconclusive (tool limitation) |
| OSM copyright / ODbL license | [openstreetmap.org/copyright](https://www.openstreetmap.org/copyright) | Yes |
| osmnx documentation | [osmnx.readthedocs.io](https://osmnx.readthedocs.io/) | Yes — API confirmed against current stable docs |
| pyrosm documentation | [pyrosm.readthedocs.io](https://pyrosm.readthedocs.io/) | Not independently fetched this pass — named as the offline alternative |
| OpenTopography Global DEM API | [portal.opentopography.org/apidocs](https://portal.opentopography.org/apidocs/) | Yes — live request confirmed endpoint/params, key requirement |
| OpenTopography account/API key signup | [portal.opentopography.org/myopentopo](https://portal.opentopography.org/myopentopo) | Not independently fetched — standard self-service signup page |
| Copernicus GLO-30 (AWS Open Data, no key) | [registry.opendata.aws/copernicus-dem](https://registry.opendata.aws/copernicus-dem/) (bucket: `s3://copernicus-dem-30m/`) | Yes — bucket readme + registry page fetched |
| USGS EROS on SRTM voids | [earthexplorer.usgs.gov](https://earthexplorer.usgs.gov/) / USGS EROS SRTM documentation | Yes (general void explanation), no Sri-Lanka-specific figure found |
| Open-Meteo Historical/Archive API | [archive-api.open-meteo.com/v1/archive](https://archive-api.open-meteo.com/v1/archive) (docs: [open-meteo.com/en/docs/historical-weather-api](https://open-meteo.com/en/docs/historical-weather-api)) | Yes — live query returned real Horton Plains weather data |
| Open-Meteo pricing/rate limits | [open-meteo.com/en/pricing](https://open-meteo.com/en/pricing) | Yes |
| NASA POWER API | [power.larc.nasa.gov/docs/services/api](https://power.larc.nasa.gov/docs/services/api/) | Yes — live query returned real data; flagged as secondary due to elevation-averaging issue |
| CHIRPS rainfall data | [data.chc.ucsb.edu/products/CHIRPS-2.0](https://data.chc.ucsb.edu/products/CHIRPS-2.0/) | Yes — directory listing confirmed live |
| PyTorch Geometric Temporal (METR-LA/PEMS-BAY loaders) | [pytorch-geometric-temporal.readthedocs.io](https://pytorch-geometric-temporal.readthedocs.io/) | Yes — loader classes confirmed present in current docs |
| Original METR-LA/PEMS-BAY source (fragile) | [github.com/liyaguang/DCRNN](https://github.com/liyaguang/DCRNN) | Repo page only — Drive/Baidu data links not independently opened |
| PeMS04 / PeMS08 (recommended source) | [github.com/Davidham3/ASTGCN](https://github.com/Davidham3/ASTGCN/tree/master/data) | Yes — real data files confirmed present |
| PeMS04/08 on Hugging Face (unverified alternative) | [huggingface.co/datasets/Salesforce/lotsa_data](https://huggingface.co/datasets/Salesforce/lotsa_data) | No — search-only, not independently fetched |
| NPS Visitor-Use Statistics (CC0 CSV package) | [catalog.data.gov/dataset/nps-visitor-use-statistics-data-package-2025](https://catalog.data.gov/dataset/nps-visitor-use-statistics-data-package-2025) | Yes — fetched directly, real file listing confirmed |
| NPS IRMA interactive portal (harder to script) | [irma.nps.gov/STATS](https://irma.nps.gov/STATS/) | Could not render (JS app) — use the data.gov package instead |
| Eco-Counter Austin analogue (Socrata API) | [data.austintexas.gov/resource/26tt-cp67.json](https://data.austintexas.gov/resource/26tt-cp67.json) (dataset page: [data.austintexas.gov/Transportation-and-Mobility/Shoal-Creek-Bike-Traffic-Counts/26tt-cp67](https://data.austintexas.gov/Transportation-and-Mobility/Shoal-Creek-Bike-Traffic-Counts/26tt-cp67)) | Yes — live query returned real sensor records |
| AMD ROCm HIP SDK Windows system requirements (GPU support table) | [rocm.docs.amd.com/projects/install-on-windows/.../system-requirements.html](https://rocm.docs.amd.com/projects/install-on-windows/en/latest/reference/system-requirements.html) | Yes — fetched directly, RX 7600 XT confirmed listed |
| AMD ROCm HIP SDK Windows install guide | [rocm.docs.amd.com/projects/install-on-windows](https://rocm.docs.amd.com/projects/install-on-windows/) | Yes — landing page confirmed |

---

## 4. Open questions / not yet decided

- Exact repo folder structure for Module 4's code+data relative to the other three modules
  (depends on whole-team repo setup, not yet started).
- Whether free-tier Colab/Kaggle GPU is actually needed at all, or whether CPU-only development on
  the local machine proves sufficient throughout — decide empirically once the ST-GNN
  implementation exists and a real training-time measurement can be taken, not speculatively now.
- Exact library choice for TWI computation (`pysheds` vs `richdem`) — both are viable; **the
  ST-GNN layer implementation choice is now resolved in favour of PyTorch Geometric Temporal**,
  since it ships built-in `METRLADatasetLoader`/`PemsBayDatasetLoader` classes confirmed present in
  its current docs (see §3.4) — worth checking its layer API covers the adaptive spatio-temporal
  attention design in `docs/PROJECT_PROPOSAL.md` §5 Module 4, or whether raw PyTorch Geometric is
  still needed for that specific piece, once implementation starts.
- **New from the 2026-08-29 verification pass, not yet actioned:**
  - Get a free OpenTopography API key before implementation starts (self-service, but it's a real
    step — see §3.2) — or use the no-key AWS S3 mirror for Copernicus GLO-30 specifically and skip
    the key entirely for that source.
  - Confirm the Geofabrik `.osm.pbf` binary itself downloads correctly with a real tool (`curl`/
    browser), since only the landing page was directly confirmed — the binary fetch failed through
    the research tooling used, most likely a tool limitation, not a dead file, but not yet
    double-checked with a real download.
  - Decide whether to attempt the METR-LA/PEMS-BAY Google Drive/Baidu links directly or rely
    entirely on the PyTorch Geometric Temporal loader classes (recommended default — see §3.4).
  - When TWI/slope features are actually computed, note in this doc whether Copernicus GLO-30's
    accuracy advantage over SRTM GL1 (see §3.2) makes a visible difference for Horton Plains
    specifically, since no site-specific accuracy comparison exists yet in the literature.

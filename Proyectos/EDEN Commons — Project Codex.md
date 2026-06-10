[[PROYECTOS]]
[[Solarpunk y Futuros Sostenibles]]

---
**Version:** 1.0 — Pre-Hackathon Definition  
**Author:** Daniel (Project EDEN)  
**Hackathon:** Green Hackathon "Think Globally, Build Locally" — June 12–14, 2026  
**Last updated:** June 2026

---
## 1. Context & Origin

This project is built as part of **Project EDEN** — a suite of autonomous robots for sustainable agriculture inspired by the Solarpunk movement. The first robot, ARIA (Autonomous Radar Intelligence Array), is a functioning ground rover that maps terrain, detects obstacles, and transmits spatial intelligence. EDEN Commons is the **software intelligence layer** of that ecosystem: the knowledge a robot needs to make contextual decisions, accessible to any human before the robot exists.

The developer is a systems engineer specializing in data, self-taught in robotics, applying to KAIST for a master's in robotics. This project serves dual purpose: competing in the Green Hackathon and strengthening the KAIST application portfolio.

---

## 2. Project Definition

### What is EDEN Commons?

EDEN Commons is a **collective agricultural intelligence platform** that fuses three sources of knowledge into a single annual cultivation calendar:

1. **Scientific layer** — real-time and forecast climate data (temperature, precipitation, humidity) from Open-Meteo API
2. **Astronomical layer** — lunar phases calculated locally using ephem or suncalc logic, following Bristol Almanac and Old Farmer's Almanac tradition
3. **Community layer** — ancestral and traditional agricultural practices contributed by users worldwide, validated and structured by AI

Any person — a farmer in Colombia, a community gardener in Nigeria, a maker in Bangladesh — can enter their location and crop, receive a full annual calendar with color-coded activity windows, and contribute what they know from their land.

### One-sentence pitch

> "Agricultural wisdom from the ground up — where climate data meets ancestral knowledge, for any crop, anywhere in the world."

### What it is NOT

- Not a weather app
- Not a crop prediction ML model
- Not a social network
- Not a marketplace
- Not a robot controller (that is ARIA's job)

---

## 3. Core Features — MVP Scope

### 3.1 Almanac Engine (the face)

The user arrives at a clean interface and inputs:

- **Location** — free text search, e.g. "Santander, Colombia" or "Dhaka, Bangladesh" (resolved via OpenStreetMap Nominatim geocoding)
- **Crop** — dropdown from available crops in the Commons DB

The system generates a **12-month annual calendar** with color-coded activity bands:

|Color|Activity|
|---|---|
|🟢 Dark green|Optimal planting / sowing window|
|🟡 Yellow|Fertilizing / soil preparation|
|🔵 Blue|Irrigation critical period|
|🟣 Purple|Pruning window|
|🟠 Orange|Harvest window|
|⚪ Gray|Rest / cover crop period|

Each month card shows:

- Dominant recommended activity
- Moon phase icons (new, crescent, full, waning)
- Average temperature range for location
- Precipitation expectation (dry / moderate / rainy)
- Community note count ("12 farmers in your region contributed")

Clicking any month or week opens a **detail panel** showing:

- Claude-synthesized explanation: "Why this week?" combining all three layers
- Specific community practices for that activity window
- Crop technical data card (see 3.3)

### 3.2 Crop Technical Data Card

Displayed alongside the calendar for every crop. Contains:

- **Common name + scientific name**
- **Germination time** (days)
- **Days to harvest** from transplant / direct sow
- **Optimal soil temperature** for germination
- **Water requirements** (low / medium / high)
- **Sun requirements** (full sun / partial / shade)
- **Companion plants** (beneficial neighbors)
- **Incompatible plants** (avoid planting nearby)
- **Frost tolerance** (yes / no / partial)
- **pH range** for soil
- **Typical yield** per m²

This data is stored in the Commons DB as a separate `crops` table, seeded manually at project start.

### 3.3 Commons Contribution System

Any user can contribute agricultural knowledge through a structured form:

**Form fields:**

- Region (free text — country, state, or local area)
- Crop (dropdown — must match a crop in the DB)
- Practice (free text — what they do and when)
- Season / timing (when this applies in their local year)
- Source (optional — "my grandmother", "30 years farming", "local cooperative")

**AI validation pipeline (two steps before saving):**

**Step 1 — Structuring:** Claude receives the raw form submission and converts it to a standardized JSON object:

```json
{
  "region": "Santander, Colombia",
  "crop": "maize",
  "activity": "planting",
  "lunar_condition": "new moon",
  "soil_condition": "moist after first rain",
  "timing_local": "April, after first rains",
  "timing_hemisphere": "spring",
  "source_type": "generational",
  "raw_text": "original submission preserved"
}
```

**Step 2 — Cross-validation:** Claude compares the structured entry against existing entries for same crop + region:

- **Consistent** with existing entries → saved with `status: verified`
- **Novel** (no similar entries exist) → saved with `status: unverified`, shown with a "new knowledge" tag
- **Regional variant** (contradicts entries from other regions) → saved with `status: regional_variant`, both shown as valid
- **Irrelevant or spam** → rejected with a clear explanation shown to user

The user sees the validation result in real time before the entry is saved. No entry is silently rejected.

### 3.4 Browse Commons

A simple searchable view of all community entries, filterable by:

- Crop
- Region
- Activity type
- Validation status

All data is **publicly readable without account**. Export to CSV available. No data is proprietary to the platform.

---

## 4. Technical Stack

### 4.1 Full Stack

|Layer|Technology|Rationale|
|---|---|---|
|UI|Streamlit|Python-native, fast to build, supports custom CSS, deployable to Streamlit Cloud|
|Language|Python 3.11+|Developer's primary language|
|AI|Anthropic Claude API (claude-sonnet-4-20250514)|Structuring + cross-validation of contributions, calendar synthesis|
|Climate data|Open-Meteo API|Free, no API key, global coverage, REST|
|Lunar phases|ephem (Python library)|Local calculation, no API dependency, astronomically accurate|
|Geocoding|OpenStreetMap Nominatim|Free, no key, global, returns lat/lon from text|
|Database (dev)|SQLite|Local file, zero config, Python native, no cost|
|Database (prod)|Supabase (PostgreSQL)|Free tier, Python client, dashboard visual, scales without code changes|
|Version control|GitHub (public repo)|Required for Streamlit Cloud deploy + portfolio visibility|
|Deploy|Streamlit Cloud|Free tier, connects directly to GitHub repo, secrets management|
|Secrets|Streamlit Secrets / .env local|API keys never in code|

### 4.2 Database Schema

#### Table: `crops`

```sql
id              TEXT PRIMARY KEY,   -- slug, e.g. "maize", "tomato"
common_name     TEXT NOT NULL,
scientific_name TEXT,
germination_days_min    INTEGER,
germination_days_max    INTEGER,
days_to_harvest_min     INTEGER,
days_to_harvest_max     INTEGER,
optimal_soil_temp_c     REAL,
water_requirement       TEXT,       -- low / medium / high
sun_requirement         TEXT,       -- full / partial / shade
frost_tolerant          BOOLEAN,
ph_min          REAL,
ph_max          REAL,
yield_kg_per_m2 REAL,
companion_plants        TEXT,       -- comma-separated slugs
incompatible_plants     TEXT,       -- comma-separated slugs
notes           TEXT
```

#### Table: `community_entries`

```sql
id              TEXT PRIMARY KEY,   -- UUID
crop_id         TEXT REFERENCES crops(id),
region          TEXT NOT NULL,
region_lat      REAL,
region_lon      REAL,
activity        TEXT,               -- planting / fertilizing / pruning / harvest / irrigation
lunar_condition TEXT,
soil_condition  TEXT,
timing_local    TEXT,
timing_hemisphere TEXT,             -- spring / summer / autumn / winter / dry / wet
source_type     TEXT,               -- generational / personal / cooperative / almanac
raw_text        TEXT NOT NULL,
structured_json TEXT,               -- JSON blob from Claude Step 1
status          TEXT DEFAULT 'unverified', -- verified / unverified / regional_variant / rejected
created_at      TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```

#### Table: `calendar_cache`

```sql
id              TEXT PRIMARY KEY,   -- hash of crop_id + lat + lon + year
crop_id         TEXT,
lat             REAL,
lon             REAL,
year            INTEGER,
calendar_json   TEXT,               -- full 12-month calendar as JSON
generated_at    TIMESTAMP,
expires_at      TIMESTAMP           -- cache for 7 days
```

### 4.3 Key Python Dependencies

```
streamlit>=1.35.0
anthropic>=0.25.0
supabase>=2.0.0
ephem>=4.1.5
requests>=2.31.0
python-dotenv>=1.0.0
pandas>=2.0.0
plotly>=5.20.0          # for calendar visualization
```

---

## 5. Application Architecture

```
eden_commons/
├── app.py                  # Streamlit entry point
├── requirements.txt
├── .env                    # local secrets (never committed)
├── .env.example            # template without values
├── README.md
│
├── core/
│   ├── almanac.py          # Almanac Engine: calendar generation
│   ├── lunar.py            # Lunar phase calculations via ephem
│   ├── climate.py          # Open-Meteo API wrapper
│   ├── geocoding.py        # Nominatim wrapper
│   └── synthesis.py        # Claude API: calendar synthesis + contribution pipeline
│
├── db/
│   ├── connection.py       # SQLite (dev) / Supabase (prod) connection manager
│   ├── queries.py          # All DB read/write operations
│   └── seed/
│       ├── crops.json      # Crop technical data — 10 crops
│       └── entries.json    # Community seed entries — ~50 entries
│
├── ui/
│   ├── calendar_view.py    # Annual calendar component
│   ├── crop_card.py        # Crop data card component
│   ├── contribute_form.py  # Contribution form + live AI validation
│   └── browse_commons.py   # Public browse view
│
└── assets/
    └── style.css           # Custom Streamlit CSS
```

---

## 6. Seed Data — What to Prepare Before Thursday

### How many entries?

**10 crops × 5 regions × 1 entry per activity type (plant, fertilize, harvest) = ~50 entries minimum**

This is enough to make the Commons feel alive from the first demo without being overwhelming to prepare manually. Each entry takes 3–5 minutes to write well.

### The 10 seed crops (globally relevant, high universality score)

|Crop|Why this crop|
|---|---|
|Maize / Corn|Staple in Latin America, Africa, Asia|
|Tomato|Universal, well-documented, high community knowledge|
|Rice|Staple for 3.5 billion people, strong ancestral practice|
|Potato|Andean origin, global reach, cold-climate relevance|
|Cassava / Yuca|Tropical staple, West Africa + Latin America|
|Beans (common)|Companion plant for maize, universal|
|Garlic|Strong lunar cultivation tradition, Old Farmer's Almanac staple|
|Lettuce / Leafy greens|Fast cycle, urban farming relevance|
|Chili pepper|Global, strong regional practice variation|
|Sunflower|Solarpunk aesthetic, pollinator value, oil crop|

### The 5 seed regions

|Region|Crops to focus|
|---|---|
|Andean Colombia / Santander|Maize, potato, beans, yuca|
|West Africa (Nigeria / Ghana)|Cassava, maize, chili|
|South/Southeast Asia (Bangladesh / Indonesia)|Rice, chili, beans|
|East Asia (Korea / Japan)|Rice, garlic, leafy greens|
|Mediterranean / Southern Europe|Tomato, garlic, sunflower|

### Where to get the seed information

**For crop technical data (crops table):**

- **OpenFarm** (openfarm.cc) — open database of crop growing guides, CC license, free to use
- **Wikipedia** crop pages — germination times, harvest days, pH ranges
- **Old Farmer's Almanac** (almanac.com) — planting charts by zone, companion planting, frost dates
- **FAO crop pages** (fao.org) — yield data, water requirements

**For community entries (entries table):**

- **Old Farmer's Almanac historical editions** (pre-1900, public domain) — lunar planting traditions, seasonal heuristics
- **Bristol Almanac** — lunar and astronomical farming correlations
- **OpenFarm community notes** — user-submitted growing tips
- **Manual research** — 2–3 hours searching regional agricultural extension services (USDA, CORPOICA Colombia, EMBRAPA Brazil)
- **Your own knowledge** — the entry about maize in Santander after first April rains is valid seed data

**Key heuristics to include as entries (from almanac tradition):**

- Plant root vegetables during waning moon (energy goes downward)
- Plant leafy crops during waxing moon (energy goes upward)
- Avoid planting on full moon and new moon days
- Harvest root vegetables after full moon for better storage
- Prune fruit trees during waning moon to reduce sap loss
- Sow after first rains of the season when soil temperature stabilizes
- Companion plant maize + beans + squash (Three Sisters system)

---

## 7. Development Phases

### Phase 0 — Before Thursday June 12 (today–Wednesday)

**Goal: Infrastructure ready, no waiting on setup during hackathon**

- [ ] GitHub repo created (public): `eden-commons`
- [ ] Streamlit app skeleton running locally (`streamlit run app.py`)
- [ ] SQLite connection working, schema created
- [ ] Open-Meteo API tested with a real location
- [ ] ephem library tested, lunar phase output verified
- [ ] Nominatim geocoding tested
- [ ] Anthropic API key configured in `.env`
- [ ] `crops.json` seed file written (10 crops, full technical data)
- [ ] `entries.json` seed file written (~50 entries across 5 regions)
- [ ] DB seeded and queryable

### Phase 1 — Friday June 13 evening (post-kickoff, ~2–3 hours)

**Goal: Core almanac engine working end-to-end**

- [ ] Location search → geocoding → lat/lon working
- [ ] Open-Meteo returns monthly climate data for any location
- [ ] ephem returns lunar phase for any date
- [ ] Claude synthesizes both + community entries into a calendar recommendation
- [ ] Basic 12-month calendar displayed in Streamlit (can be simple table first)
- [ ] Crop data card displayed alongside calendar

### Phase 2 — Saturday June 14 (full build day)

**Goal: Full MVP feature complete**

- [ ] Calendar color coding implemented (plotly heatmap or custom HTML/CSS)
- [ ] Month/week detail panel working
- [ ] Contribution form built
- [ ] Claude Step 1 (structuring) working
- [ ] Claude Step 2 (cross-validation) working
- [ ] Entry saves to DB, confirmation shown to user
- [ ] Browse Commons view (filterable table)
- [ ] Custom CSS applied (Solarpunk color palette: earth tones + green)
- [ ] Supabase connection configured and tested
- [ ] Switched from SQLite to Supabase
- [ ] Deployed to Streamlit Cloud from GitHub repo

### Phase 3 — Sunday June 15 morning (polish + submission)

**Goal: Demo-ready, submission complete by 10pm EST**

- [ ] Full user flow tested end-to-end on deployed URL
- [ ] Edge cases handled (crop not found, location not found, API timeout)
- [ ] README.md written with architecture diagram
- [ ] Loom demo recorded (2 minutes)
- [ ] Submission form filled

---

## 8. Solarpunk Design Language

The UI should feel intentional and warm, not corporate. Guidelines for the custom CSS:

**Color palette:**

- Primary: `#4a7c59` (deep forest green)
- Secondary: `#8fb339` (fresh leaf green)
- Accent: `#d4a843` (harvest gold)
- Background: `#f5f0e8` (warm parchment)
- Text: `#2c2c1e` (dark earth)
- Surface: `#fffdf7` (off-white)

**Typography:**

- Headings: serif or slab serif if available, otherwise Georgia
- Body: clean sans-serif, generous line height
- Data: monospace for numbers and coordinates

**Visual language:**

- Rounded corners on cards
- Subtle earth-tone borders
- Moon phase icons (Unicode: 🌑🌒🌓🌔🌕🌖🌗🌘)
- Activity icons: 🌱 sow · 🌿 fertilize · ✂️ prune · 💧 irrigate · 🌾 harvest
- No sharp corporate blues or grays

---

## 9. Alignment Guide for Thursday's Problem Statements

When the four problem statements are published Thursday June 12, apply this decision filter in 30 minutes:

### Green light — enter with minimal framing adjustment

The problem mentions any of:

- Access to agricultural knowledge or tools
- Food sovereignty or food security
- Community-led environmental action
- Indigenous or ancestral knowledge preservation
- Climate adaptation for smallholder farmers
- Democratization of scientific or technical data
- Local food systems or urban agriculture

**Action:** Submit as-is. Adjust the opening line of the pitch to echo the problem statement's language.

### Yellow light — enter with framing pivot

The problem mentions:

- Environmental monitoring (reframe Commons as monitoring knowledge platform)
- Green jobs or climate workforce (reframe as knowledge infrastructure for green agricultural jobs)
- Climate data access (lead with the climate layer, downplay community layer in pitch)
- Biodiversity or ecosystem health (reframe crop companion planting data as biodiversity tool)

**Action:** Adjust pitch framing and demo path. Core code unchanged.

### Red light — this problem statement does not fit

The problem is primarily about:

- Urban infrastructure, mobility, or transit
- Industrial waste or manufacturing emissions
- Energy grid or renewable energy hardware
- Marine or ocean ecosystems

**Action:** Do not force the fit. Pivot to EDEN Harvest Router (the Boustrophedon algorithm as a web service) which is the second-strongest buildable idea in 48h.

---

## 10. Judging Criteria — How EDEN Commons Scores

### Scalability (can it hold 10k users?)

**Answer:** Yes. Architecture is stateless at the application layer. Open-Meteo handles unlimited requests. Claude API scales on demand. Supabase free tier handles 50,000 rows and 2GB — sufficient for initial launch. Streamlit Cloud handles concurrent users. The only scaling cost is Claude API tokens, which is a success problem, not an architecture problem.

### Universality (does it work from Hong Kong to Bangladesh?)

**Answer:** Yes, by design. Open-Meteo covers the entire globe with historical and forecast data. Nominatim geocodes any location on Earth. The Commons DB has seed data from 5 regions across 4 continents. The calendar logic works for both hemispheres (seasons are detected from latitude).

### User-Friendly (can anyone, any age, use it?)

**Answer:** Two inputs, one button. No account required to read. No technical knowledge needed. The contribution form is plain language — if you can describe what you do on your land, you can contribute. Claude handles the structuring invisibly.

### Equitable (does it inform optimism, not extract from users?)

**Answer:** All data contributed is publicly readable and exportable. The platform owns nothing — knowledge belongs to the community that contributed it. Ancestral and traditional knowledge is treated as equally valid to scientific data, not as a subordinate input. No advertising, no data selling, no algorithmic profiling.

---

## 11. Connection to Project EDEN

EDEN Commons is not a standalone app — it is the **knowledge layer** of the EDEN robotic ecosystem:

- **ARIA (current)** maps terrain and detects obstacles. It operates on physical intelligence.
- **EDEN Commons** captures what to do with that terrain — when to plant, when to harvest, what the land has taught generations of farmers.
- **CERES (planned)** — the CNC agricultural gantry — will consume the Commons calendar directly to schedule autonomous cultivation actions.

In the KAIST application portfolio, EDEN Commons demonstrates that the project thinks beyond hardware: a complete autonomous agricultural system needs physical robots, software intelligence, and community knowledge working together. That is the Solarpunk vision — technology in service of community, not extraction from it.

---

## 12. What Success Looks Like

**Minimum viable win (hackathon):**

- App runs end-to-end without errors
- Calendar renders for at least 5 crops in at least 3 regions
- One contribution goes through the full validation pipeline live in the demo
- Deployed URL accessible to judges

**Ideal win (Grand Prize criteria):**

- Judges can immediately imagine sharing this with their communities
- Coffee Jesus sees the planning layer his FarmBot system needs
- Kristy sees a tool that elevates marginalized agricultural voices
- Aiman sees AI that amplifies human knowledge without replacing it

**Portfolio win (KAIST application regardless of hackathon result):**

- Public GitHub repo with clean, documented code
- README that explains the EDEN ecosystem connection
- Functioning deployed URL
- Evidence of thoughtful system architecture decisions

---

## 13. Open Questions (resolve before or during hackathon)

- [ ] Does Streamlit Cloud free tier support concurrent users comfortably for a demo?
- [ ] Does Open-Meteo return reliable monthly aggregates (not just daily forecasts)?
- [ ] Does ephem require any calibration for Southern Hemisphere lunar phases?
- [ ] Should the calendar display full 12 months or start with current month + 11 forward?
- [ ] What happens when a user searches a crop not in the DB? (Suggest closest match? Show empty state with invite to contribute?)
- [ ] Should contributions require any friction (captcha, email) to prevent spam at scale?

---

_This codex is a living document. Update after Thursday's problem statements are published and after each development phase completes._
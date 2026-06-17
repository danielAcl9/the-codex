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
eden-commons/
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
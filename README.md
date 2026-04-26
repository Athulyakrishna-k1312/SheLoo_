<div align="center">

<br/>

<!-- LOGO / WORDMARK -->
<h1>
  👑 Sheloo
</h1>

<p><strong>Safe public toilet finder — built by women, for women.</strong></p>

<p>
  <img src="https://img.shields.io/badge/Built%20With-Vanilla%20JS-F7DF1E?style=flat-square&logo=javascript&logoColor=black"/>
  <img src="https://img.shields.io/badge/Map-Leaflet.js-199900?style=flat-square&logo=leaflet&logoColor=white"/>
  <img src="https://img.shields.io/badge/Data-OpenStreetMap-7EBC6F?style=flat-square&logo=openstreetmap&logoColor=white"/>
  <img src="https://img.shields.io/badge/Backend-None-E8526A?style=flat-square"/>
  <img src="https://img.shields.io/badge/Login-Not%20Required-4CAF87?style=flat-square"/>
  <img src="https://img.shields.io/badge/Cost-Free-blueviolet?style=flat-square"/>
</p>

<p>
  <a href="[https://your-username.github.io/sheloo/](https://athulyakrishna-k1312.github.io/SheLoo_/)"><strong>🔴 Live Demo</strong></a>
  &nbsp;·&nbsp;
  <a href="#features"><strong>Features</strong></a>
  &nbsp;·&nbsp;
  <a href="#tech-stack"><strong>Tech Stack</strong></a>
  &nbsp;·&nbsp;
  <a href="#getting-started"><strong>Get Started</strong></a>
</p>

<br/>

<!-- HERO IMAGE / MOCKUP DESCRIPTION -->
> 🚺 **73% of women in India avoid public toilets at night** due to safety concerns.  
> Existing apps tell you *where* toilets are — but not *how safe* they are.  
> **Sheloo fixes that.**

<br/>

</div>

---

## 🌟 What is Sheloo?

Sheloo is a **women-centric public toilet finder** that combines live OpenStreetMap data with crowd-sourced safety intelligence. It shows nearby toilets on an interactive map, scores them for safety and cleanliness, warns you at night, lets the community rate and report them, and gives you a one-tap SOS emergency button — all with **zero backend, zero login, and zero cost.**

Built in **2 HTML files** using pure HTML + CSS + JavaScript. No npm. No frameworks. No server. Works offline after first load.

---

## ✨ Features

### 🗺️ Map & Discovery
- **Real-time toilet finder** — fetches all public toilets within **5 km** of your location using the Overpass API (live OpenStreetMap data)
- **GPS geolocation** — one-tap "My Location" using the browser's native Geolocation API
- **Location search** — search any city, town, or area by name via Nominatim geocoding
- **Distance calculation** — Haversine formula gives precise distance from you to each toilet, shown in meters or km
- **Sorted list** — toilets displayed nearest-first in the side panel, synced with the map

### 🛡️ Scoring System
- **OSM base score** — automatically parsed from OpenStreetMap tags:
  - `operator`, `name` → cleanliness indicator
  - `female=yes`, `lit=yes` → safety bonus
  - `wheelchair=yes`, `opening_hours` → quality bonus
  - `access=private` → safety penalty
- **Crowd score** — community ratings (1–5 stars, separate for safety and cleanliness) blended in with weighted averaging
- **Weighted blending** — the more ratings a toilet has, the more the crowd score dominates over OSM base score
- **Final score out of 10** — displayed on every card and map popup

### 🌙 Night Mode *(unique feature)*
- Automatically detects current time and activates after **9 PM**
- Applies a **safety score penalty** based on hour:
  - Standard night (21:00–22:59 / 04:00–05:59): **−2.0 pts**
  - Deep night (23:00–03:59): **−3.0 pts**
  - Toilets tagged `lit=yes`: reduced penalty (**−0.8 / −1.5**)
- Shows a `🌙 −X night` badge on every affected toilet card
- Panel and header shift to a **violet night palette**
- **Auto-refreshes every 60 seconds** — activates mid-session without page reload

### 🌡️ Heat Zone Visualization
- Toggle-able color-coded **circle overlays** on the map (400 m radius per toilet)
- Color reflects the toilet's combined safety + cleanliness score:
  - 🟢 **Green** — Safe (score ≥ 7)
  - 🟡 **Orange** — Moderate (score 5–7)
  - 🔴 **Red** — Low rated (score < 5)
- Overlapping circles in dense areas blend naturally — real heatmap feel, **no extra library**
- Crowd-rated toilets are more opaque → reviewed areas visually glow brighter
- Zones update instantly when new ratings are submitted

### ⭐ Crowd-sourced Reviews
- **Star rating modal** with separate tracks for 🛡️ Safety and 🧼 Cleanliness (1–5 stars each)
- Hover preview on stars before confirming
- All data stored in **`localStorage`** — persists across sessions, no backend needed
- Cards, popups, and heat zones **update in real time** after every submission

### 🏆 Community Picks
- Horizontally scrollable strip showing the **top-rated toilets** near you
- Ranked by **trust score** = `avg_score × log(review_count + 1)` — rewards both quality and quantity
- 🥇 🥈 🥉 🏅 medals for top 5 picks
- **Re-ranks live** after every new review — great for live demo moments
- Hidden automatically when no ratings exist yet

### ⚑ Report / Flag System
- **⚑ Report button** on every toilet card and map popup
- Four issue types:
  - 🔒 Closed / Locked → **severe** (red banner)
  - ⚠️ Feels Unsafe → **severe** (red banner)
  - 🗑️ Very Dirty → moderate (yellow banner)
  - 🔧 Broken / No Water → moderate (yellow banner)
- Reports accumulate — *"⚠️ Reported unsafe (3 reports)"*
- Stored in a separate `localStorage` key so it never interferes with ratings

### 🆘 SOS Emergency Button
- Pulsing red button **fixed bottom-right**, always visible on the map
- Tapping it fetches your **live GPS coordinates** instantly
- Three emergency actions:
  - 📞 **Call 112** — direct dial
  - 💬 **WhatsApp** — pre-filled message with your Google Maps location link
  - 📋 **Copy to clipboard** — fallback if no call signal
- Gracefully handles geolocation denial

### 🧭 Navigation
- **Google Maps deep link** on every card and popup — opens turn-by-turn directions from your location to the toilet

---

## 🛠 Tech Stack

| Layer | Technology | Why |
|---|---|---|
| Map engine | **Leaflet.js** v1.9.4 | Lightweight, open-source, no API key |
| Map tiles | **OpenStreetMap** | Free, global, no usage limits |
| Toilet data | **Overpass API** | Queries OSM for `amenity=toilets` in real time |
| Geocoding | **Nominatim** (OSM) | Free place search, no API key needed |
| Navigation | **Google Maps** deep link | No API key — just a URL pattern |
| Storage | **Browser localStorage** | Persists ratings and flags — no backend |
| Fonts | **Google Fonts** — DM Serif Display + DM Sans | Premium editorial feel |
| Language | **Vanilla HTML + CSS + JS** | Zero dependencies, zero build step |
| Hosting | **GitHub Pages** | Free static hosting, no server needed |

---

## 🏗️ Architecture

```
User location (GPS / Search)
        │
        ▼
Overpass API ──────────────── Raw toilet elements (lat, lon, tags)
        │
        ▼
OSM Tag Parser ──────────────── Base safety + cleanliness score (1–10)
        │
        ▼
localStorage ───────────────── Crowd ratings blended in (weighted by count)
        │
        ▼
Night Mode Check ───────────── Safety penalty applied if hour ∈ [21:00, 06:00)
        │
        ▼
UI Render ──────────────────── Cards (panel) + Markers (map) + Heat zones
        │
        ▼
User Action ────────────────── Rate / Report / SOS / Navigate
        │
        ▼
localStorage updated ────────── UI re-renders in real time (no reload)
```

---

## 📂 File Structure

```
sheloo/
├── index.html        ← Landing page
│                        Animated split layout, device mockup,
│                        problem stats, feature highlights
│
└── sheloo.html       ← Main application
                         Map + panel + all features
                         ~700 lines, fully self-contained
```

**Two files. No build step. Open in browser and it works.**

---

## 🚀 Getting Started

### Option 1 — Open directly
```bash
git clone https://github.com/your-username/sheloo.git
cd sheloo
# Open index.html in your browser
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```
> ⚠️ For geolocation to work, open via a local server or deploy to HTTPS (GitHub Pages). Browsers block GPS on `file://` URLs.

### Option 2 — Local server (recommended)
```bash
# Python 3
python -m http.server 8080

# Node.js
npx serve .

# Then open http://localhost:8080
```

### Option 3 — Deploy to GitHub Pages
1. Push this repo to GitHub
2. Go to **Settings → Pages → Source → main branch → / (root)**
3. Visit `https://Athulyakrishna-k1213.github.io/sheloo/`

---

## 🔧 Configuration

No API keys required. No `.env` file. No config.

If you want to change the search radius (default 5 km), find this line in `sheloo.html`:

```javascript
node["amenity"="toilets"](around:5000, ${lat}, ${lon});
```

Change `5000` (metres) to any value you want.

---

## 🚫 What We Deliberately Did NOT Use

| Thing | Reason avoided |
|---|---|
| Backend server | Adds complexity, hosting cost, latency |
| Database | localStorage is sufficient for MVP crowd data |
| Login / Auth | Friction kills adoption; anonymous is fine |
| Google Maps API | Requires billing setup; Leaflet + OSM is free |
| npm / Webpack / React | Zero build step = anyone can open and run it |
| Heatmap library (Leaflet.heat) | Custom CSS circles achieve the same visual |
| Paid geocoding API | Nominatim (OSM) is free and accurate enough |

---

## 📊 Scoring Formula

```
Base Score (OSM tags)     →  safety: 1–10,  cleanliness: 1–10
                                      ↓
Crowd Blend Weight        →  w = min(review_count / 5, 1.0)
                                      ↓
Blended Score             →  base × (1 − w) + crowd × w
                                      ↓
Night Penalty             →  −0.8 to −3.0  (if hour ∈ [21, 6))
                                      ↓
Final Score               →  clamped to [1, 10]

Community Trust Score     →  avg_score × log(review_count + 1)
(used for picks ranking)
```

---

## 🗺️ Data Sources

- **Toilet locations** — [OpenStreetMap](https://www.openstreetmap.org/) via [Overpass API](https://overpass-api.de/)
- **Geocoding** — [Nominatim](https://nominatim.org/) (OSM)
- **Safety stats** — Based on NSSO / Swachh Bharat Mission reports on women's sanitation access in India

---

## 👥 Team

**Illusive Coders**
IEEE Computer Society — Kerala Chapter Hackathon

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

<div align="center">

**Built with ♥ for women's safety · Powered by open data · Zero cost to run**

</div>

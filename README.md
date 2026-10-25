# FloodVoice 🌊

**Speak, and be found.** A voice-first flood rescue system for Chennai.

Built at the *Talk to Build* AI Buildathon (Grootan Technologies, Chennai, 24 Oct 2026).

## Problem
In the 2015 Chennai floods over 500 people died and about 1.8 million were displaced. Today's systems push alerts *to* people; nothing lets a stranded person send a request for help *back*, in Tamil, without an app or internet.

## Solution: many doors, one brain, one map
- **Doors in:** voice button (Tamil / Tanglish / English), offline SMS buttons with GPS, Bluetooth relay (prototype, simulated), call / missed-call line (roadmap)
- **One brain:** Gemini turns messy speech into structured data (area, depth, category, severity, vulnerable); a rules engine ranks who gets help first
- **One output:** a live rescue map, a priority list and an AI Command Brief for responders

## Features
| Feature | Status |
|---|---|
| Voice → AI → pin on the map | Live (Gemini key set once on the server via ⚙️; built-in rule parser otherwise) |
| Shared live map across devices | Live (Cloudflare Worker + D1) |
| CSV / GeoJSON export for responders | Live |
| Priority list (rules engine) | Live |
| Merge reports within 1 km | Live |
| Category filters | Live |
| AI Command Brief | Live |
| Offline SMS buttons with GPS | Live |
| Tamil spoken reply | Live (depends on the device's Tamil voice) |
| Went-dark list | Sample data |
| Bluetooth relay | Simulated prototype |
| Call / SMS line (Exotel or Twilio) | Roadmap |

**Priority score:** `severity + depth_cm/20 + 3 if vulnerable + 2 if medical`

## Run
The app is a Cloudflare Worker (`src/worker.js`) that serves the dashboard (`public/index.html`) and a small API backed by Cloudflare D1.

```bash
npm install -g wrangler
wrangler d1 create floodvoice        # paste the database_id into wrangler.toml
wrangler dev                         # local run at http://localhost:8787
wrangler deploy                      # publish
```

Click ⚙️ in the dashboard and paste a Gemini API key to switch on live AI for every device. Without a key, the built-in Tanglish rules engine is used.

API: `/api/reports`, `/api/report`, `/api/update`, `/api/resolve`, `/api/brief`, `/api/stats`, `/api/export.csv`, `/api/export.geojson`, `/api/health`.

`seed.json` holds the 15 sample Chennai reports.

### Known limits
- `/api/config` and `/api/reset` have no login yet; add auth before real use.
- Helpline numbers in the app (1070, 1077, 1913) should be verified with the authorities before deployment.
- The "near you" card shows the top 3 reports by priority, not by distance.

## Stack
HTML / JavaScript, Leaflet + OpenStreetMap, Web Speech API, Gemini API, Cloudflare Workers + D1.

## Team
Navin Jairam M

Parts of this codebase were written with AI assistance.

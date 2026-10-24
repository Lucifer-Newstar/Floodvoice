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
| Voice → AI → pin on the map | Live (Gemini key in ⚙️; built-in rule parser otherwise) |
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
Open `index.html` in Chrome. Click ⚙️ and paste a Gemini API key for live AI (stored only in your browser). Without a key, a built-in rule parser is used.

`seed.json` holds the 15 sample Chennai reports.

## Stack
HTML / JavaScript, Leaflet + OpenStreetMap, Web Speech API, Gemini API.

## Team
Navin Jairam M

Parts of this codebase were written with AI assistance.

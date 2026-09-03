# Code for Communities

**Darjeeling Himalayan Railway Edition · GDG Siliguri**

🟢 Starter · 🟠 Medium · 🔴 Ambitious

---

## Track A — The Journey

Apps for the passenger on the toy train: Siliguri to Darjeeling, 88 km, 2 ft gauge, opened 1881, UNESCO World Heritage since 1999. No signal for most of the ride.

### A1. Offline Heritage Companion for the DHR 🟠 MEDIUM

A web app that answers questions about the route — Batasia Loop, Ghum, the Z-reverses, the B-class steam locomotives, the 1881 opening and the 1999 UNESCO inscription — with no signal. Cache a small curated knowledge base in the browser and use an on-device LLM for conversational answers (lightweight local RAG). Test: ask "why does the train loop here?" as the train passes the actual spot.

> → MediaPipe LLM Inference for Web (Gemma) or Chrome Prompt API where available; knowledge base + embeddings in IndexedDB; Geolocation API to bias answers to the current stretch of track.

### A2. Zero-Bars Phrasebook 🟢 STARTER

A two-way translator for the Nepali / Hindi / Bengali / English mix a tourist actually meets, running fully in-browser. Cover the situations that matter: bargaining at a stall, asking directions, ordering food, medical help. Bonus: an on-device LLM layer that adapts phrasing to context and politeness level.

_Judged on: does a Nepali speaker on the platform understand the output?_

> → Chrome Translator & Language Detector APIs _if_ they support the Nepali pair on your device; otherwise Transformers.js with a small NLLB/OPUS model cached in the browser. Web Speech API for speak-aloud.

### A3. Point-and-Know 🟠 MEDIUM

Open the camera in the browser, point at a tea plant, a Himalayan bird, a station sign or a landmark, and get an offline explanation. An on-device classifier finds the label; an on-device LLM turns it into a useful sentence. A natural fit for demoing out of a moving window.

> → getUserMedia + MediaPipe Tasks for Web (image classification / object detection) + on-device LLM for phrasing. Ship a small custom label set (station signs, common birds, tea) rather than a generic ImageNet model.

### A4. Trip-to-Travelogue 🟢 STARTER

Passengers jot rough notes and snap photos in the app; it stitches them into a clean travelogue or social caption on-device, with no upload. The data is generated live during the ride, so it is a strong window demo.

> → Chrome Summarizer / Prompt API where available, else MediaPipe LLM; MediaPipe image labeling for auto-tags; Web Share API to post once signal returns.

### A5. On-Device Accessibility Tool 🔴 AMBITIOUS

Make the journey usable for passengers with hearing or vision impairment, entirely client-side. Achievable core: an announcement board where staff type a message once and passengers get large-text, high-contrast display and spoken output in their language. Stretch: live captioning of spoken announcements (be aware a steam engine is loud) or scene description on demand from the camera.

> → Web Speech API (TTS) + on-device translation; MediaPipe Tasks for Web (audio / vision) + on-device LLM for phrasing on the stretch goals.

### A6. Hotspot Mesh — collaborative AI without the internet 🔴 AMBITIOUS

Lean all the way into the constraint: browsers share data directly over a local hotspot via WebRTC while an on-device model does the intelligence — a shared trivia game about the route, or a carriage-wide note board that an on-device LLM summarises for everyone. Rewards teams that treat "no network" as a feature.

> → WebRTC data channels (with a local signalling fallback — QR-code or manual SDP exchange) + MediaPipe LLM for Web or Chrome Prompt API.

---

## Track B — AI for the Hills

Apps for the people who live here: a belt where monsoon rain cuts roads and signal, where springs run dry despite ~3,000 mm of rain a year, and where tea gardens are the main livelihood.

### B1. Offline Landslide Reporter & Last-Mile Alert Relay 🟠 MEDIUM

In October 2025, over 300 mm of rain in 12 hours triggered landslides across the hills; an official high-risk warning had been issued hours earlier but never reached most people. Build both halves of that gap.

- **Report up:** a walker logs a slope observation — photo of a crack, seepage, a bulging retaining wall — and an on-device model classifies severity, explains the risk in plain language and says what to do; reports queue in browser storage and sync when a hotspot appears.
- **Relay down:** the app can receive an official alert from one connected phone and rebroadcast it peer-to-peer to phones with no signal.

_Bonus: image analysis to flag tension cracks, tilted trees, fresh debris._

> → getUserMedia + MediaPipe Tasks for Web + on-device LLM; IndexedDB + Background Sync for queue-and-sync; WebRTC / Web Bluetooth for the relay.

### B2. Know Your Hills 🟠 MEDIUM

Point the phone's browser at a ridge, peak or valley and get its name, elevation and a short story — which peak is Kanchenjunga, why Tiger Hill matters, what river runs below. Uses the camera plus the browser's compass/orientation and location APIs, so it works on a moving train with zero network.

> → getUserMedia + DeviceOrientation & Geolocation APIs + local geo-tagged knowledge base + on-device LLM; optional MediaPipe landmark detection.

### B3. Spring Health & Household Water-Saver 🟢 STARTER

Darjeeling town runs a daily water deficit estimated at 67% (about a quarter of it leakage), and only 14 of its 26 springs (dhara) are still active. Build either half:

- **Household:** log usage, get on-device tips tuned to a hill home (rainwater-harvesting sizing, greywater reuse, leak spotting) and estimate how long stored water lasts until the next supply.
- **Community:** a spring-mapping tool — log a dhara, its location, flow and season, offline, and merge logs when phones meet.

> → On-device LLM for advice; in-browser OCR (Transformers.js / MediaPipe) for meter or bill capture; data in IndexedDB; export as CSV/GeoJSON.

### B4. Terrace-Farm & Tea-Garden Advisor 🟠 MEDIUM

An agri-assistant for hill farmers, small tea growers and estates with no connectivity: snap a diseased tea leaf or crop in the browser, get an on-device diagnosis and treatment, plus slope-appropriate advice (contour planting, erosion control, monsoon timing). Small growers — who sell leaf to bought-leaf factories and have the least tooling — are the priority user.

> → getUserMedia + MediaPipe Tasks for Web (image classification, fine-tuned on a small leaf-disease set) + on-device LLM.

### B5. Homestay Helper for Garden Villages 🟠 MEDIUM

Tea-garden families increasingly look to homestays as a second income, and women make up most of the tea workforce. An offline toolkit for a first-time host: multilingual guest communication (Nepali ↔ Hindi/Bengali/English), a simple bookings-and-cash ledger, help writing a listing and pricing it, and a checklist for hosting. Should work on a low-end Android phone with no data plan.

> → On-device translation + on-device LLM for listing text; IndexedDB ledger; Web Share for posting the listing when in town.

### B6. Road Status Mesh 🟠 MEDIUM

"Is NH-55 open? Is the Rohini road blocked?" is the daily monsoon question. Crowd-sourced blockage reports (photo, location, time, still-passable-or-not) that travel phone-to-phone over hotspot or Bluetooth when there is no network, with an on-device model de-duplicating and summarising them into a route status board.

> → Geolocation + WebRTC data channels / Web Bluetooth + on-device LLM for summarisation; pairs naturally with A6 and B1.

### B7. Disaster-Ready Hills Assistant 🔴 AMBITIOUS

A broader offline companion for hill emergencies — landslide, cloudburst, road blockage, cold exposure, being cut off from the nearest hospital — giving step-by-step guidance and the nearest safe action when there is no signal to call for help. Teams choosing this should absorb B1 and B6 into one civic tool rather than build alongside them.

> → On-device LLM + curated first-response knowledge base cached in the browser; Geolocation for nearest shelter/PHC.

---

## Track C — The Railway Itself

Apps for the people who run the DHR: permanent-way staff, loco sheds, station masters and guards. Real users, real documents, and a partner who can put your app to work.

### C1. Gangman's Logbook 🟠 MEDIUM

An offline track-inspection tool for permanent-way staff walking the alignment: photo + GPS + severity for a slip, rockfall, blocked drain or damaged retaining wall, with an on-device model suggesting a first classification and a plain-language note. Reports queue and sync at the next station that has connectivity, and roll up into a simple section-wise dashboard.

> → Same stack as B1: getUserMedia + MediaPipe Tasks + on-device LLM; IndexedDB + Background Sync.

### C2. Steam-Shed Assistant 🟠 MEDIUM

On-device question answering over the B-class locomotive and rolling-stock maintenance documentation — a real local-RAG problem with a real document set. "What is the torque on this fitting?" answered from the manual, offline, in the shed at Tindharia.

_Organisers will confirm which documents DHR can share before the event._

> → On-device LLM + embeddings in IndexedDB; PDF text extraction in the browser (pdf.js).

### C3. Disruption Companion 🟢 STARTER

Monsoon cancellations and delays are routine. An offline app that reads a short status entered by station staff and explains, in Nepali / Hindi / Bengali / English, what it means for a passenger and what to do next (wait, alternative road transport, refund process). Shown on a station tablet or scanned as a QR by passengers.

> → On-device translation + on-device LLM for phrasing; QR generation; Web Speech for announcements.

### C4. Track-Side Hazard Signage Reader 🟢 STARTER

Many hazard, gradient and station boards along the line are old and in English only. Point a camera at a board and get it read aloud and translated into the user's language, offline.

> → getUserMedia + in-browser OCR (Transformers.js) + on-device translation + Web Speech.

---

## How we judge

| Criterion               | Weight | What we look for                                                                         |
| ----------------------- | ------ | ---------------------------------------------------------------------------------------- |
| Works offline           | 25%    | Airplane mode on stage. Full flow completes. No silent server calls.                     |
| Usefulness to the hills | 25%    | Would a real passenger, farmer, host or railway worker use this next monsoon?            |
| On-device AI done well  | 20%    | Model choice fits the device; graceful fallback; the AI adds something a form could not. |
| Craft                   | 15%    | Fast first load, small bundle, sensible caching, readable on a cheap phone in sunlight.  |
| Belonging               | 15%    | Nepali/Hindi/Bengali support; local names, places and facts are right.                   |

## Submission

- A public URL (GitHub Pages, Netlify, Vercel or similar) that installs as a PWA and works after one online load.
- A public repo with a README stating: which on-device model(s) you use, the minimum device you tested on, and what happens when the model is unavailable.
- A 2-minute video recorded with airplane mode visibly on.
- Teams of 2–4. One problem statement per team; you may combine statements where the brief says so (B1+B6+B7, A6+B6).

---

_Build small. Ship a link. Run it offline. Belong to the hills._

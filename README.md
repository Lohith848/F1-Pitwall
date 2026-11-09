# F1 Pit Wall Dashboard.

> A live, personalised Formula 1 season dashboard. Real-time championship data, race countdown, full calendar, and a dedicated Verstappen tracker and redbull team tracker ( can be changed )  — all in a single place.

**[→ Live Demo](https://my-f1-pitwall.vercel.app/)**

---

## What It Is

A personal "Pit Wall" web app for the 2026 F1 season. Not a template — built and personalised from the ground up. It fetches live championship data from the Jolpica F1 API, rebuilds the UI dynamically, and auto-refreshes every 5 minutes.

No npm. No React. No build step. Open in a browser, done.

---

## Features

| Section | What It Does |
|---|---|
| **Hero & Ticker** | Animated masthead with live scrolling WDC/WCC standings ticker |
| **Next Race Block** | Auto-detects upcoming race + real-time countdown to lights out |
| **Season Calendar** | All 23 rounds — completed (gold), next (pulsing blue), upcoming |
| **Drivers' Championship** | Live top-10 WDC standings, VER highlighted with ★ FAV badge |
| **Constructors' Cup** | Live all-11 WCC standings, Red Bull highlighted, animated bar fills |
| **Paddock Intel** | Last race podium fetched live + curated news in editorial layout |
| **Stats Ribbon** | Championship gap, leader points, WCC leader, Verstappen Watch |

---

## Tech Stack

```
HTML5          →  Single-file app structure
CSS3           →  900+ lines: variables, grid, flexbox, 14 keyframe animations
Vanilla JS     →  ES6+, async/await, DOM manipulation, setInterval
Fetch API      →  Promise.all() parallel requests, AbortController timeouts
Jolpica API    →  Free F1 data API (Ergast successor) — no key required
Google Fonts   →  Playfair Display · Inter · JetBrains Mono
Netlify        →  Static hosting, zero config
```

No frameworks. No build tools. No dependencies.

---

## API Endpoints

All data from [Jolpica F1 API](https://api.jolpi.ca) — free, open, no API key needed.

```
GET https://api.jolpi.ca/ergast/f1/2026/driverStandings.json
GET https://api.jolpi.ca/ergast/f1/2026/constructorStandings.json
GET https://api.jolpi.ca/ergast/f1/2026/races.json?limit=30
GET https://api.jolpi.ca/ergast/f1/2026/last/results.json
```

Data updates the Monday after each race weekend.

---

## How It Works

1. Page loads → skeleton placeholders appear immediately
2. `Promise.all()` fires all 4 API requests in parallel
3. JSON parsed → driver/constructor rows built dynamically
4. Calendar logic compares each race date to today → marks done / next / upcoming
5. Countdown targets the next race's exact start datetime
6. Status bar shows 🟢 LIVE with timestamp on success
7. `setInterval` silently refreshes everything every 5 minutes
8. If API fails → `try/catch` triggers offline fallback with last-known static data

---

## File Structure

Everything is in one file: `index.html`

```
index.html
├── <head>          — fonts, meta, title
├── <style>         — full CSS engine (~700 lines)
├── <body>          — structural HTML skeleton
└── <script>        — data engine (~380 lines)
    ├── CONFIG      — season year, refresh interval, VER/RBR IDs
    ├── fetchAllData()          — master orchestrator
    ├── renderDrivers()         — live WDC rows
    ├── renderConstructors()    — live WCC rows with bar fills
    ├── renderCalendar()        — 23-round season strip
    ├── renderNextRace()        — upcoming race block
    ├── renderLastRace()        — last race podium
    ├── renderTicker()          — scrolling data ticker
    ├── startCountdown()        — lights-out timer
    └── renderFallback()        — offline emergency data
```

---

## Personalisation

Built specifically for **LOHITH G**:

- Name in hero headline, page title, footer, and ticker
- Full accent theme switched to **Red Bull blue (#3671C6)**
- **Max Verstappen** row highlighted with blue glow + ★ FAV badge
- **Red Bull Racing** constructor row highlighted
- **Verstappen Watch** stat card tracking his championship gap
- Time-based greeting on page load

To personalise for yourself, edit the `CONFIG` block at the top of the `<script>` section.

---

## Deployment

**Netlify (current):** Drag-and-drop `index.html` → live in 20 seconds.

**Vercel:**
1. `vercel.com` → Add New Project → Deploy without Git repo
2. Drop `index.html` → done

**With GitHub auto-deploy:**
```bash
git init
git add index.html
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/pitwall-f1-2026.git
git push -u origin main
# Connect repo to Vercel/Netlify → every push auto-deploys
```

---

## Updating for Next Season

Change one line in the `CONFIG` block:

```js
const SEASON = 2026; // → change to 2027
```

The entire app — API calls, calendar, standings — updates automatically.

---

## Roadmap

- [ ] Race history modal per driver (Jolpica `/drivers/{id}/results.json`)
- [ ] Qualifying results tab (`/last/qualifying.json`)
- [ ] OpenF1 API race mode — near real-time lap positions during a live GP
- [ ] PWA — install as home screen app, offline cache

---

## Attribution

Original design concept adapted and significantly modified:
- Full API integration (Jolpica — 4 live endpoints)
- Personalisation (name, theme, favourites, Verstappen Watch)
- Offline fallback system + skeleton loading
- API status bar + auto-refresh loop
- Countdown timer logic



---

*Built by LOHITH G · [my-f1-pitwall.vercel.app](https://my-f1-pitwall.vercel.app/)*

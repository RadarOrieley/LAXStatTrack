# 🥍 LAX Stats Tracker

A fully offline-capable youth lacrosse stats tracker built as a Progressive Web App (PWA). Runs in any mobile browser and installs to the home screen on both Android and iOS. No app store required, no internet needed at game time.

---

## 📋 Features

### Team Management
- **Dual-team tracking** — toggle between your team and the opponent with one tap; each team has completely separate rosters, stats, and data
- **Custom team names** — rename both teams (e.g. "Eagles" vs "Falcons") via the pencil icon
- **Player roster** — add players with jersey number, name, and squad assignment
- **Squad management** — create multiple squads and move players between them at any time

### Live Stat Entry (per player)
| Stat | Description |
|------|-------------|
| **Goal** | Goal scored by this player |
| **Shot** | Shot taken at the opponent's goal |
| **FO Win** | Face-off won |
| **FO Loss** | Face-off lost |
| **Save** | Shot stopped (goalie) |
| **Allow** | Goal allowed (goalie) |

- Undo button on every player to correct mistakes mid-game
- Goalie stats (Save / Allow) appear automatically when a player is assigned to the GK position, or whenever any goalie stats have been recorded for them
- Live save percentage shown on the goalie's row

### Position Tracking
- Set each player's current position: **ATK · MID · DEF · GK · Bench**
- Position timers run automatically while the game clock is running
- Colored time chips update live on each player's row
- Switching positions starts the new timer and stops the old one instantly

### Against Our Goal (team-level)
Tracked as team events, not per player:
| Stat | Description |
|------|-------------|
| **Wide / Miss** | Shot at our goal that missed the net entirely |
| **We Got Rebound** | We recovered the ball after a shot on our goal |

### Ball Possession
- Persistent tracker bar always visible above the tabs
- Tap **Our Ball** or **Their Ball** to start timing possession
- Tap **Neither** to pause both timers (dead ball, timeout, etc.)
- Possession timers only run while the game clock is running
- Live percentage split shown between the two sides

### Game Clock
- Start / Stop / Reset controls in the header
- Drives both position time tracking and possession timing simultaneously

### Summary & Export
- **Team Totals** — goals, shots, shot%, FO win%, GK save%, possession %, game time
- **Goalie Summary** — per-goalie saves, allowed, save%, and total GK time
- **Position Time table** — per-player ATK / MID / DEF / GK / Bench / total on-field time
- **Player Stats table** — full stat line for every player
- **Export to CSV** — downloads a `.csv` file with both teams' full stats in separate sections, plus possession data; opens in Excel, Google Sheets, or Numbers
- **Save as PDF** — fires the browser print dialog; select "Save as PDF" to produce a clean, print-ready report (works on iPad and Android)

---

## 📁 File Structure

```
lax-pwa/
├── index.html               ← Entire app (single file)
├── manifest.json            ← PWA manifest (name, icons, theme color)
├── sw.js                    ← Service worker (offline caching)
├── icons/
│   ├── icon-72x72.png
│   ├── icon-96x96.png
│   ├── icon-128x128.png
│   ├── icon-144x144.png
│   ├── icon-152x152.png
│   ├── icon-192x192.png
│   ├── icon-384x384.png
│   ├── icon-512x512.png
│   ├── apple-touch-icon.png ← iOS home screen icon (180×180)
│   ├── favicon-32.png
│   └── favicon-16.png
└── README.md
```

---

## 🚀 Deployment

The app must be served over **HTTPS** for the service worker (and offline mode) to function. Pick any option below.

### Option A — GitHub Pages (free, recommended)

1. Create a free account at https://github.com
2. Click **+** → **New repository** → name it `lax-stats` → set to **Public** → **Create**
3. On the repo page click **"uploading an existing file"**
4. Unzip the package and drag **all files and the `icons/` folder** into the upload window
   - `index.html` must be at the **root** of the repo, not inside a subfolder
5. Click **Commit changes**
6. Go to **Settings → Pages → Source** → select branch `main`, folder `/ (root)` → **Save**
7. After ~60 seconds your URL appears: `https://YOUR-USERNAME.github.io/lax-stats/`

Share that URL with other coaches. On first visit over Wi-Fi the app caches itself and works offline from then on.

### Option B — Netlify Drop (fastest, no account needed)

1. Go to https://app.netlify.com/drop
2. Drag the entire unzipped folder onto the page
3. Get a live URL instantly (e.g. `https://random-name.netlify.app`)
4. Optionally rename the site in Netlify settings

### Option C — Any HTTPS web host

Upload all files to any web server with HTTPS enabled. The file paths must be relative (they already are), so the app works under any subdirectory.

---

## 📱 Installing on Devices

### Android — Chrome
1. Open the app URL in Chrome
2. An **"Install LAX Stats"** banner appears after a few seconds — tap **Install**
3. If the banner doesn't appear: tap **⋮** menu → **Add to Home screen**

### iPhone / iPad — Safari
> ⚠️ Must use **Safari**. Chrome on iOS cannot install PWAs.

1. Open the app URL in Safari
2. An install instructions banner appears automatically, or:
3. Tap the **Share button** (□↑) at the bottom of the screen
4. Scroll down and tap **"Add to Home Screen"**
5. Tap **Add**

Once installed, the app launches full-screen with no browser chrome and works 100% offline.

---

## 🔄 Updating the App

When you replace files on your host, any installed device will show an **"Update available — Refresh"** banner at the top of the screen. Tapping it applies the update immediately.

When making code changes, always increment the cache version in `sw.js` to trigger the update banner on installed devices:

```js
const CACHE_NAME = 'lax-stats-v7';  // bump this with every release
```

---

## 🔒 Data & Privacy

- All data is stored **locally on the device** using `localStorage`
- Nothing is transmitted to any server at any time
- Data persists between sessions and app restarts
- The app contains no analytics, tracking, or advertising of any kind
- Clearing browser/site data on the device will erase all stats — always export to CSV or PDF before doing so

---

## ⚙️ Technical Notes

- **Single HTML file** — the entire application (HTML, CSS, JavaScript) lives in `index.html`; no build tools or dependencies required
- **Service worker** (`sw.js`) uses a cache-first strategy for local assets and network-first for Google Fonts, with full offline fallback
- **Data migration** — the app automatically upgrades localStorage data from older versions; existing rosters and stats are preserved across updates
- **No external dependencies** at runtime — Google Fonts are cached on first load and served offline after
- **HTTPS required** for service worker registration (GitHub Pages and Netlify both provide this automatically)

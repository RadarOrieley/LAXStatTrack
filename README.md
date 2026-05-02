# 🥍 LAX Stats Tracker — PWA

A fully offline-capable youth lacrosse stats tracker. Works on iPad, iPhone, and Android tablets.

---

## 📁 Files

```
lax-pwa/
├── index.html          ← The whole app
├── manifest.json       ← PWA manifest (name, icons, colors)
├── sw.js               ← Service worker (offline caching)
├── icons/
│   ├── icon-72x72.png
│   ├── icon-96x96.png
│   ├── icon-128x128.png
│   ├── icon-144x144.png
│   ├── icon-152x152.png
│   ├── icon-192x192.png
│   ├── icon-384x384.png
│   ├── icon-512x512.png
│   ├── apple-touch-icon.png  ← iOS home screen icon
│   ├── favicon-32.png
│   └── favicon-16.png
└── README.md
```

---

## 🚀 Deployment Options (pick one)

### Option A — GitHub Pages (FREE, recommended)

1. Create a free account at https://github.com
2. Click **New repository** → name it `lax-stats` → set to **Public**
3. Upload all files from this folder (drag & drop in the GitHub UI)
   - Make sure `index.html` is at the **root** of the repo
4. Go to **Settings → Pages → Source** → select `main` branch → **Save**
5. Your app URL will be: `https://YOUR-USERNAME.github.io/lax-stats/`

Done. Share that URL with coaches. On first visit with Wi-Fi, it installs to their device.

---

### Option B — Netlify Drop (fastest, no account needed)

1. Go to https://app.netlify.com/drop
2. Drag the entire `lax-pwa` folder onto the page
3. Netlify gives you a URL instantly (e.g. `https://random-name.netlify.app`)
4. Optional: rename the site in Netlify settings

---

### Option C — Your own web host / server

Upload all files to any web server that serves HTTPS.
**HTTPS is required** for service workers (and therefore offline use) to work.

---

## 📱 Installing on Devices

### Android (Chrome)
1. Open the app URL in Chrome
2. A banner will appear: **"Install LAX Stats"** → tap **Install**
3. If the banner doesn't appear, tap Chrome menu (⋮) → **Add to Home screen**

### iPhone / iPad (Safari)
> Must use **Safari** — Chrome on iOS cannot install PWAs.

1. Open the app URL in Safari
2. An instructions banner will appear automatically, or:
3. Tap the **Share button** (□↑) at the bottom
4. Scroll down → tap **"Add to Home Screen"**
5. Tap **Add**

The app icon will appear on the home screen. It launches full-screen, no browser UI, works 100% offline after first load.

---

## 🔒 Data & Privacy

- All data is stored locally on the device in `localStorage`
- Nothing is sent to any server
- Data persists between sessions
- Clearing browser data / site data will erase stats — export to CSV or PDF before doing so

---

## 🔄 Updates

When you update the app files on your host, visitors will see an **"Update available — Refresh"** banner at the top of the screen. Tapping it applies the update instantly.

To force a new version, bump the `CACHE_NAME` in `sw.js`:
```js
const CACHE_NAME = 'lax-stats-v2';  // increment this
```

---

## 📋 Features

- ✅ Player roster with jersey numbers and squad assignment
- ✅ Live stat entry: Goals, Shots, FO Wins/Losses, GK Saves/Allowed
- ✅ Real-time position time tracking (ATK / MID / DEF / GK / Bench)
- ✅ Goalie-specific stats and save percentage
- ✅ Multiple squads with drag-between assignment
- ✅ Game clock with automatic position time accumulation
- ✅ Export to CSV (downloads file) and PDF (print dialog)
- ✅ Full offline support via service worker
- ✅ Installs to home screen on iOS and Android
- ✅ All data saved locally — survives app restarts

# Family Time — Project Context for Claude

> Paste this into any Claude session (mobile, desktop, or Claude Code) to instantly sync context.
> Claude Code reads this file automatically when run from the repo folder.

---

## What This App Does

**Family Time** helps parents get personalized activity recommendations to connect with their kids. Live at `skaash24.github.io/family-time`. Repo: `github.com/skaash24/family-time`. Single file: `index.html`.

The app asks 6 questions → recommends a perfect family activity with: why it works, step-by-step instructions, what you'll need, a connection tip, and a bonus twist. Users can tap "Try Another" to cycle without repeats.

---

## Tech Stack

- Single standalone `index.html` — no frameworks, vanilla JS
- Hosted on GitHub Pages
- `open-meteo.com` — free weather API (no key needed)
- `Nominatim` (OpenStreetMap) — reverse geocoding for city detection
- Google Fonts: Nunito + Fraunces
- No backend, no database

---

## Design Tokens

```css
--cr: #fdf8f2  /* cream background */
--wm: #f5efe6  /* warm white */
--sd: #e8d9c5  /* sand border */
--te: #c96a3c  /* terracotta accent */
--fo: #3d6b4f  /* forest green */
--go: #d4a843  /* gold */
--ink: #2a1f14 /* dark brown text */
--mu: #7a6a5a  /* muted text */
```

Fonts: `Fraunces` (serif headings, italic accents) + `Nunito` (UI, weights 400/700/800/900)

---

## Current Features (as of latest commit)

### Core Flow
- 6-question wizard: location → time → ages → energy → mood → budget
- Smart scoring engine matches answers to best activity
- "Try Another" cycles without repeats
- Back button on every step

### Auto-detected Context
- Season, time of day, day of week
- Live weather via open-meteo API
- Live city via browser geolocation + Nominatim
- 10+ holiday detection (Halloween, Christmas, Thanksgiving, Valentine's, etc.)
- Weekend detection

### Manual Override (Planning Mode)
- Tap day or weather pill to open override modal
- Override: day of week, season, weather condition
- Planning mode indicator shown on result
- "Clear Overrides" button to return to live data
- Use case: "what should we do this Saturday when it's raining?"

### Activity Library
- 250+ hand-crafted activities
- Categories: silly/fun, calm/close, learning, active, rainy day, holiday specials, weekend specials, outdoor, teen-specific, toddler-specific, road trip/car, restaurant/waiting room, creative arts, cooking & food, community/giving back, seasonal, screen-free evenings
- **Splurge category** (recently added): theme parks, zoos, aquariums, escape rooms, rock climbing, trampoline parks, laser tag, bowling, go-karts, axe throwing, kayaking, horseback riding, hot air balloon, zip lining, surfing, skiing, cooking classes, food tours, pottery, drive-in movies, whale watching, planetarium, overnight camping, comedy shows, sports events, concerts, museums, and more

### Rich Activity Details
Activities with `richType` get auto-populated smart sections:
- `farmersMarket` → nearby markets via Nominatim or finding guide
- `scavengerHunt` → 15-item seasonal list (4 different lists by season)
- `birdWatching` → birds common to current season + Merlin/eBird tips
- `stargazing` → planets + constellations visible this season
- `hiking` → nearby trails via Nominatim or AllTrails guide
- `splurge` → Google search link auto-generated from detected city + `activity.searchQuery`

### Scoring System
```js
// Location match: +30 (exact) or +15 (either)
// Age match: +18 per matching age group
// Mood match: +20 per matching mood
// Time match: +15
// Budget match: +10
// Weather match: +5 to +25
// Outdoor penalty in bad weather: -15 to -30
// Season match: +20
// Holiday match: +40
// Weekend match: +15
// Time of day match: +10
// Splurge boost: +25 if budget=splurge and activity has moderate/splurge budget tag
// Open budget boost: +15 if budget=open and activity has moderate/splurge budget tag
```

### Budget Options
- Free → no spend
- A Little → under $50
- Splurge → $50+, paid activities get scoring boost
- Any → all activities, paid activities get smaller boost

---

## Activity Data Structure

```js
{
  n: "Activity Name",
  t: "Tagline",
  w: "Why this works — connection psychology explanation",
  s: ["Step 1", "Step 2", "Step 3", "Step 4"],  // how to do it
  n2: ["What you need", "Item 2"],               // supplies
  tip: "Connection tip for the parent",
  e: "low" | "medium" | "high",                  // energy level
  twist: "Bonus variation idea",
  richType: "farmersMarket" | "scavengerHunt" | "birdWatching" | "stargazing" | "hiking" | "splurge",  // optional
  searchQuery: "google search string",            // for splurge richType only
  tags: {
    loc: ["inside"] | ["outside"] | ["inside","outside"],
    ages: ["toddler","young","tween","teen"],     // select applicable
    mood: ["silly","calm","learning","active"],    // select applicable
    time: ["15-20 minutes","30-45 minutes","1 hour","2+ hours"],
    budget: ["free"] | ["small"] | ["moderate","splurge"] | ["free","small"],
    weather: ["any"] | ["rainy","cold","snowy"] | ["clear","warm","cloudy"] | etc,
    season: ["spring","summer","fall","winter"],   // optional
    timeOfDay: ["morning","afternoon","evening","night"],  // optional
    dayType: ["weekend"],                          // optional
    holiday: ["halloween","christmas","thanksgiving","valentine","newyear"],  // optional
    setting: ["car"] | ["restaurant"],             // optional
  }
}
```

---

## Files in Repo

```
family-time/
├── index.html      # The entire app — all HTML, CSS, JS in one file
├── icon.png        # 180x180 home screen icon (stamp design, blue tones)
└── CLAUDE.md       # This file
```

---

## Home Screen Icon

- 180x180px PNG stamp-style design
- Blue color scheme (ocean blue serrated ring, navy FT letters, cool blue paper)
- Already added to index.html: `<link rel="apple-touch-icon" href="icon.png">`

---

## Pending / Future Ideas

- GitHub MCP integration (token already set up via Claude Code on Mac)
- More splurge activities with live event data
- User can save favorite activities
- Share an activity via link
- PWA / offline mode

---

## How to Work on This

### Claude Code (Mac Terminal)
```bash
cd ~/family-time
claude                        # starts Claude Code — reads this file automatically
```
Then just say what you want changed in plain English. Claude Code can edit `index.html` and `git push` directly.

### Claude Chat (Mobile or Desktop Browser)
1. Paste this `CLAUDE.md` content at the start of the conversation
2. Then paste the raw `index.html` from GitHub if you want code changes
3. Get back a patched file or exact edit instructions

### Getting Latest Code
- GitHub: `github.com/skaash24/family-time` → `index.html` → **Raw** → select all → copy
- Terminal: `git pull` from inside the repo folder

---

## Owner

Sharon — skaash24 on GitHub

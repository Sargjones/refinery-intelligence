# 🛢️ Global Refinery Intelligence

**Live dashboard tracking global oil refinery capacity, closures, war damage, and the fuel supply chain.**

**Live site:** [fuel.criticalto.ca](https://fuel.criticalto.ca) *(deploy after DNS setup)*  
**Sister platform:** [criticalto.ca](https://criticalto.ca) — Toronto Infrastructure Intelligence  
**CSI-Global data:** [github.com/Sargjones/csi-global](https://github.com/Sargjones/csi-global)

---

## What it tracks

| Layer | Data | Update frequency |
|---|---|---|
| Refinery locations | 37+ facilities worldwide, capacity, status | Static (manually updated on events) |
| Refinery status | Operating / Closed / War-damaged / Converted / At-risk | Event-driven |
| Hormuz war clock | Days since Feb 28, 2026 closure | Computed daily |
| Live energy indicators | Brent crude, Baltic Dry Index, FAO food index, GDELT supply shock | Via CSI-Global (6-hourly) |
| Fuel supply chain | 9-step crude-to-pump process explainer | Static |

---

## Key facts (May 2026)

- **9.69 mb/d** of global refinery capacity closed 2019–2026 (~10% of working capacity)
- **3.52 mb/d** war-damaged across Gulf and Russia (as of May 7, 2026)
- **21 days** US jet fuel supply — lowest since 1963
- **17%** of California refining capacity lost: Phillips 66 LA (closed Q4 2025) + Valero Benicia (idled Apr 2026)
- **132** US refineries operating (down from 139 in 2019)
- **Strait of Hormuz closed** since March 4, 2026 — ~20% of global oil trade blocked

---

## Repository structure

```
refinery-intelligence/
├── index.html              ← main dashboard (map + process explainer + live data)
├── widget-banner.html      ← embeddable alert banner for criticalto.ca (Wix HTML embed)
├── data/
│   └── refineries.json     ← curated refinery dataset (location, capacity, status)
├── .github/
│   └── workflows/
│       └── daily-update.yml  ← GitHub Actions: update war clock, fetch EIA weekly data
└── README.md
```

---

## Deployment

### GitHub Pages (recommended)

1. Create repo: `refinery-intelligence` (public)
2. Upload all files
3. Settings → Pages → Source: Deploy from branch → main → / (root)
4. Dashboard live at: `https://sargjones.github.io/refinery-intelligence/`

### Custom domain (`fuel.criticalto.ca`)

Add `CNAME` file to repo root containing `fuel.criticalto.ca`, then:
- In your DNS provider, add: `CNAME fuel → sargjones.github.io`
- In GitHub Pages settings, set custom domain: `fuel.criticalto.ca`

### Wix integration (criticalto.ca)

The `widget-banner.html` file is a self-contained alert banner designed to paste into a **Wix HTML embed** (`+` → Embed → HTML iframe). It:
- Shows the Hormuz war day count (computed from Feb 28, 2026)
- Shows current Brent crude and status from CSI-Global
- Links to `fuel.criticalto.ca` with a "View Refinery Dashboard" CTA
- Auto-updates — no Wix republish needed

Recommended placement: top of the CriticalTO homepage, above the fold, below the main header.

---

## Data sources

- **EIA Short-Term Energy Outlook** (monthly) — us refinery count, utilization, jet fuel supply days
- **Argus Media** — refinery closure confirmations
- **IIR Energy** — war damage estimates
- **Wikipedia List of Oil Refineries** — facility coordinates and capacity
- **CSI-Global** (Sargjones/csi-global) — live energy indicators via GitHub Actions

---

## Relationship to other platforms

```
criticalto.ca          ← Toronto-focused infrastructure intelligence (Wix)
  └── data.criticalto.ca    ← TII dashboard (GitHub Pages)
  └── fuel.criticalto.ca    ← THIS REPO — global refinery intelligence
  
global.criticalto.ca   ← CSI-Global (community supply chain, humanitarian focus)
```

---

*Built by Sarah Jones — Brantford, Ontario, Canada*  
*Part of the CriticalTO infrastructure intelligence initiative.*  
*Context: US-Iran war / Hormuz closure began Feb 28, 2026.*

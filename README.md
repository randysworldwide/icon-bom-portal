# ICON Vehicle Dynamics – BOM Reference Portal

A self-contained, browser-based Bill of Materials reference tool for ICON Vehicle Dynamics, Alloys, and Armor product lines. Built and maintained by RANDYS Worldwide.

---

## What It Does

The portal gives internal teams and customers a fast, searchable interface for ICON product data across three brands:

- **Vehicle Dynamics** — Full kit and component breakdown with BOM linkage, kit comparison tool, and image lightbox
- **Alloys** — Complete product listing with specs and images
- **Armor** — Complete product listing with specs and images

### Key Features

- **Smart search** — Finds products by part number (with or without hyphens), UPC, description keywords, year, make, model, or any combination. Multi-word searches use AND logic.
- **Kit comparison** — Select any two Vehicle Dynamics kits to see a side-by-side diff with status icons showing what's shared, what changed in quantity, and what's unique to each kit.
- **Image lightbox** — Click any product image to open a full-screen viewer with arrow navigation, thumbnail strip, and keyboard shortcuts (← → Esc).
- **BOM drill-down** — Click any component SKU to jump directly to its detail page.
- **No server required** — The portal is a single HTML file with all data embedded. It runs entirely in the browser from a local file or any web host.

---

## Files

| File | Description |
|------|-------------|
| `index.html` | The portal (rename of `RANDYS BOM Portal - ICON.html`) |
| `server.py` | Optional local Flask server — proxies PDM Automotive API for live product images and install docs |
| `Start BOM Portal.bat` | Windows launcher — starts `server.py` and opens the portal in your browser |
| `build_icon_portal.py` | Build script — compiles all data JSON files into `index.html` |
| `README.md` | This file |

---

## Viewing the Portal

### Option A — Open directly (no install needed)
Double-click `index.html` in File Explorer. It opens in your default browser. All search and comparison features work immediately.

### Option B — Run the local server (enables live PDM images)
Double-click `Start BOM Portal.bat`. This starts the Flask server and opens the portal at `http://localhost:8080`. Requires Python and the packages listed below.

### Option C — GitHub Pages (customer-facing link)
See the [Deployment](#deployment) section below.

---

## Updating Product Data

All product data lives in JSON files in the project folder. The build script reads these and compiles them into the single-file portal.

**To update and publish:**

1. Replace or update the relevant JSON data files:
   - `sd_icon_vd.json` — Vehicle Dynamics product specs
   - `bom_icon_vd.json` — Vehicle Dynamics kit BOMs
   - `img_icon_vd.json` — Vehicle Dynamics image URLs
   - `sd_icon_alloys.json` — Alloys product specs
   - `img_icon_alloys.json` — Alloys image URLs
   - `sd_icon_armor.json` — Armor product specs
   - `img_icon_armor.json` — Armor image URLs

2. Run the build script:
   ```
   python build_icon_portal.py
   ```
   This writes a new `RANDYS BOM Portal - ICON.html` (~8.8 MB).

3. Rename the output to `index.html` and push it to GitHub (see [Deployment](#deployment)).

---

## Deployment

The portal is hosted via **GitHub Pages**, giving customers a permanent link that always serves the latest version.

**Live URL:** `https://randysww.github.io/icon-bom-portal/`

### First-time setup
1. Create a public repository on GitHub named `icon-bom-portal`
2. Upload `index.html` to the repository root
3. Go to **Settings → Pages → Deploy from branch → main / root → Save**
4. The portal goes live within ~60 seconds

### Pushing an update
1. Rebuild the portal with `build_icon_portal.py`
2. Rename output to `index.html`
3. In the GitHub repo, click `index.html` → upload the new file → Commit
4. GitHub Pages redeploys automatically — customers see the new version on next open

---

## Local Server Setup (Optional)

The Flask server (`server.py`) proxies requests to the PDM Automotive API for live product images and install documentation. It also caches results in memory to avoid redundant API calls.

**Requirements:**
```
pip install flask requests
```

**Endpoints:**
| Endpoint | Description |
|----------|-------------|
| `http://localhost:8080/` | Portal index |
| `http://localhost:8080/api/pdm/{SKU}` | Fetch normalized PDM data for a SKU |
| `http://localhost:8080/api/auth-test` | Test all PDM auth methods |
| `http://localhost:8080/api/explore/{SKU}` | Debug all auth × endpoint combinations for a SKU |
| `http://localhost:8080/api/cache/clear` | Clear in-memory cache |

---

## Version History

| Version | Date | Notes |
|---------|------|-------|
| v1.0 | April 2026 | Initial release — VD, Alloys, Armor; kit comparison; lightbox; ICON brand guidelines |

---

## Maintained By

RANDYS Worldwide — [randysww.com](https://randysww.com)

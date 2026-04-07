# t.Setup

**Stereo Camera Sensor/Lens/Volume Calculator for DIC Systems**

t.Setup is a web-based tool for selecting optimal measuring volumes, lenses, and camera configurations for stereo Digital Image Correlation (DIC) systems. Built for applications engineers, sales teams, and customers working with ZEISS ARAMIS, Phantom, Photron, and other stereo imaging systems.

## Features

### Sensor Setup
- Forward calculator: select camera, base, and lens — see measurement volume, working distance, and displacement sensitivity
- Reverse calculator: enter desired measurement volume — get recommended lens and distance
- Bidirectionally linked sliders: MV, working distance, camera spacing, and angle all update together
- Depth of field estimation with interactive aperture slider
- Displacement sensitivity: X/Y (1/100 pixel in-plane) and Z (1/30 pixel out-of-plane)
- ZEISS calibration object recommendations (CP20/CP40/CC20 series) with marker diameters
- Speckle pattern size recommendations

### Frame Rate & Exposure
- Object velocity input with max exposure time calculation (per iDICs 2018: 0.1 px blur limit)
- High-speed camera frame rate tables with recording duration by buffer size
- Throughput (Gpx/s) and bandwidth (Gbps) calculations
- Resolution/FPS lookup for Phantom TMX, T3610, and more

### Camera & Lens Database
- 30 cameras: ZEISS ARAMIS (1, 12M, SRX), Phantom (TMX, T-series, KT-series), Photron (Nova, Orion, Mini W), Blackfly S, Pharsighted
- 28 lenses: Schneider Kreuznach (Opal, Tourmaline, Jade, Emerald), Titanar, Kowa, ARAMIS 1 dedicated
- In-app editors with search, filters, sorting, visibility toggle, and import/export (JSON)
- Drag-to-reorder lenses for custom dropdown ordering

### Configuration
- Camera and base selection with auto-filtering
- Camera filters: ZEISS-only mode, show/hide legacy cameras
- Adjustable calculation parameters (circle of confusion, blur limit)
- All settings and selections cached in browser localStorage

## Tech Stack

- React 18 + TypeScript + Vite
- Progressive Web App (PWA) — installable, works offline
- Client-side only — no backend, no data sent externally
- Light/dark theme

## Getting Started

```bash
npm install
npm run dev
```

Open http://localhost:5173 in Chrome. Use the hamburger menu to navigate between views.

## Install as App

In Chrome, click the install prompt at the bottom of the page, or go to Settings > Install t.Setup. The app works offline after installation.

## Deployment

Built for GitHub Pages deployment:

```bash
npm run build
```

Output in `dist/` — deploy to any static hosting.

## Calculation Engine

All optical calculations are ported from the ZEISS INSPECT `mvcalc.py` sensor setup module:

- **Beam length**: `BL = CD / (2 sin(alpha/2))`
- **Lens equation**: `g = BL0/2 + sqrt((BL0/2)^2 - BL0*f)`
- **MV projection**: stereo-angle-compensated field of view
- **DoF**: `2N * CoC * (m+1) / m^2` (pixel-based CoC per iDICs 2018)
- **Exposure**: `max_t = blur_limit / (velocity * magnification)`

See the in-app Help page for full formula documentation.

## Data Management

Camera and lens databases are JSON files in `public/data/`. Edit directly or use the in-app editors:

- `cameras.json` — 30 camera definitions
- `lenses.json` — 28 lens definitions with Schneider datasheet specs
- `bases.json` — 13 base/rig configurations
- `calibration-objects.json` — ZEISS CP20/CP40/CC20 panels
- `frame-rates.json` — Phantom high-speed camera resolution/FPS tables

## License

Internal use only. All calculations performed locally.

---

Built by [Trilion Quality Systems](https://trilion.com)

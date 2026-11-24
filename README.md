# FIELD-CART OS — QR Code Engineer

A 100% offline, zero-dependency civil & site engineering handheld calculator and scannable **QR Cartridge Studio**, packaged into a single air-gapped HTML application.

> **Copyright & License**: Copyright (c) 2026 **NazreenNasyuha**. Released under the [MIT License](LICENSE).

---

## Highlights

- **100% Self-Contained & Air-Gapped**: Runs directly from your local filesystem (`file://`) or GitHub Pages in Airplane Mode — zero external CDNs, zero web fonts, zero telemetry, enforced via a strict Content Security Policy (`connect-src 'none'`).
- **Dual Layout & Field Themes**:
  - **Studio Mode** (desktop workbench with live QR Cartridge Dock) & **Handheld Mode** (thumb-friendly field instrument layout).
  - **Dark Lab** & high-contrast **Daylight Site** themes for outdoor readability.
- **Built-In Pure-JS QR Engine (`PureQR`)**: Spec-compliant **ISO/IEC 18004** QR Code encoder (Versions 1–10, UTF-8 Byte Mode, Reed-Solomon GF(256), EC Levels M & L, all 8 mask patterns + 4 ISO penalty rules) — no third-party libraries.

---

## Engineering Tools Included

### 1. Gradient & Invert Level Calculator (`PIPE / DRAIN`)
- 4-way bidirectional solver: **Find Gradient**, **Find IL2 (Downstream)**, **Find IL1 (Upstream)**, and **Find Length (`L`)**.
- Supports `1 : X` ratio and `%` grade units, Fall / Rise direction toggles, quick engineering presets (`1:60` to `1:200`, `1%`, `2%`), and `IL1 <-> IL2` swap.
- Real-time **SVG Longitudinal Pipe Cross-Section** diagram and step-by-step formula breakdown (`Ratio`, `%`, `m/m`, `deg`, `Δh`, `Slope Length`).

### 2. Interpolation Studio (`SURVEY / LEVELS`)
- **Linear Interpolation (`X <-> Y`)**: Bidirectional interpolation with automatic out-of-range **Extrapolation Warning** and live **SVG Coordinate Plot**.
- **Chainage / Station Level Profile**: Generates regular setting-out station tables (`5m`, `10m`, `20m`, `25m` or custom intervals) plus custom extra chainages, with safe RFC-4180 CSV clipboard export.

### 3. Site Bench (`FIELD COMPANION`)
- **Leveling (HPC & Cut/Fill)**: Computes Height of Plane of Collimation (`HPC = TBM + BS`), Reduced RL (`HPC - Staff`), and Cut / Fill / On-Grade (`±2 mm`) tags with safe CSV export.
- **Linked 4-Way Slope Converter**: Instant synchronized conversion across `1:X`, `%`, `deg °`, and `mm/m`.
- **Excavation / Concrete Volume Estimator**: Net volume (`L × W × D × Qty`), `+10%` wastage allowance, plan area, cross-section area, and trench sidewall area.

### 4. QR Cartridge Bay & Printable Spec Cards
- Flash any calculation state into a compact **`FC1|...`** payload and render a crisp, scannable QR code.
- Export high-DPI **640×840 PNG QR Spec Cards** ready to print, laminate, or attach to site drawings.
- Reload cartridges via paste (`FC1|...` or JSON), native offline browser **`BarcodeDetector` camera scanner** (on supported browsers over HTTPS/localhost), or JSON library backup import/export.

---

## Quick Start

### Option A — Run Locally (Offline)
1. Download or clone this repository:
   ```bash
   git clone https://github.com/NazreenNasyuha/QR-Code-Engineer.git
   ```
2. Double-click **`QR Engineer.html`** (or **`index.html`**) to open it in any modern desktop or mobile browser. No build step or server is required.

### Option B — Deploy via GitHub Pages
1. Open your repository **Settings → Pages** on GitHub.
2. Under **Build and deployment**, select **Source: Deploy from a branch**, branch **`main`**, folder **`/ (root)`**, and click **Save**.
3. Once deployed, visit:
   `https://nazreennasyuha.github.io/QR-Code-Engineer/`
   (`index.html` automatically routes to `QR Engineer.html`.)

---

## Compact QR Wire Format (`FC1`)

Cartridges serialize into concise pipe-delimited UTF-8 strings designed to fit comfortably inside QR Versions 1–10 (`<= 216 bytes` EC-M / `<= 271 bytes` EC-L):

| Tool | Code | Example Structure |
| :--- | :---: | :--- |
| Gradient & Invert | `G` | `FC1\|G\|<Name>\|m=...&il1=...&il2=...&l=...&g=...&gu=...&d=...` |
| Linear Interpolation | `I` | `FC1\|I\|<Name>\|x1=...&y1=...&x2=...&y2=...&t=...&s=...` |
| Chainage Profile | `C` | `FC1\|C\|<Name>\|sc=...&sl=...&ec=...&el=...&iv=...&ex=...` |
| Leveling Log | `L` | `FC1\|L\|<Name>\|tbm=...&bs=...&r=label:staff:design;...` |

---

## Security & Privacy

- **Zero Network Calls**: Enforced by `<meta http-equiv="Content-Security-Policy">` with `connect-src 'none'`, `object-src 'none'`, `base-uri 'none'`, and `form-action 'none'`.
- **Untrusted Input Hardening**: All scanned QR strings, pasted codes, JSON backups, and `localStorage` entries pass through a strict schema sanitizer with type allowlisting, prototype-pollution guards, finite-number coercion, and import size/count limits.
- **XSS & CSV Safety**: Delegated DOM event listeners eliminate inline JS attribute injection; CSV clipboard exports use RFC-4180 quoting and spreadsheet formula neutralization.

---

## License

Copyright (c) 2026 **NazreenNasyuha**.  
This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

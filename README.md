# Ultra Rotary Generator MK-III Research Edition

A browser-based rotary generator and gear-train simulator with 2D schematic drawing, 3D visualization, live telemetry, diagnostics, export tools, an R&D lab for digital-twin style experiments, and an Analysis Lab with real FFT vibration spectra, gear stress calculation, lubrication-film modelling, efficiency maps, mission profiles, BOM costing, and a built-in self-test suite.

> **Important:** This project is an educational and conceptual simulation. It is not a certified engineering calculator, safety system, or manufacturing-ready design package. Validate all real-world mechanical, electrical, thermal, and safety decisions with qualified engineering analysis and testing.

---

## Features

### Interactive Generator Simulator

* Live rotary generator visualization
* 2D schematic canvas
* 3D Three.js scene
* Adjustable RPM, power, gear count, gear ratio, module, shaft diameter, clearance, and material
* Gear types including Spur, Helical, Planetary, Worm, and Rack & Pinion
* Camera controls, labels, axes, particles, thermal color mapping, and optional audio feedback

### Live Telemetry

* RPM
* Power output
* Torque
* Efficiency
* Temperature
* Vibration
* Health index
* Battery storage
* Load
* Remaining useful life estimate
* Risk index
* Live Chart.js telemetry graph

### Environment and Control

* Ambient temperature
* Throttle control
* Load control
* Cooling control
* Temperature and vibration warning limits
* Auto-safeguard mode
* AI Supervisor Control for simulated derating and protection actions

### Diagnostics

* Fault injection modes
* Overheat, vibration, wear, and resonance indicators
* System event log
* Anomaly scoring
* Lubrication index
* Bearing life estimate
* Resonance safety margin

### R&D Lab

* Bearing type and dynamic load rating inputs
* Lubricant viscosity model
* Electrical generator estimates including voltage, current, and power factor
* Digital-twin fidelity control
* Design optimizer
* Monte Carlo reliability testing
* Stress-test matrix
* Survival probability estimate
* Best-control optimizer
* Predictive maintenance plan export

### Analysis Lab (new in MK-III)

* **FFT vibration spectrum** — a real 2048-point radix-2 FFT (Hann-windowed, 8192 Hz sample rate) over a synthesized accelerometer signal containing shaft 1×/2× components, gear-mesh frequency (GMF) harmonics with sidebands, and rolling-element bearing defect tones (BPFO, BPFI, BSF, FTF). Fault injection changes the spectrum the way it would on a real machine, and a spectral diagnosis line identifies the dominant signature.
* **Gear tooth stress** — Lewis bending stress with the Barth dynamic factor and tabulated 20° full-depth form factors, plus Hertzian contact stress with per-material elastic coefficients. Live safety factors against material allowables feed the risk index.
* **Lubrication film model** — Vogel-type viscosity-temperature behaviour (ISO VG grades), simplified Hamrock–Dowson EHL film thickness, and the λ ratio classifying the regime as boundary, mixed, or full film.
* **Efficiency island map** — a 2D heatmap of efficiency across RPM × load with a live crosshair on the current operating point.
* **Mission profile editor** — define operating phases (duration, throttle, load, cooling), then simulate the whole mission with per-second thermal integration and Miner's-rule fatigue accumulation. Reports energy produced, peak temperature, damage per mission, and missions-to-failure.
* **BOM + cost estimator** — gears, shaft, bearings, magnet rotor, copper windings, housing, lubricant, and labour estimated from the current geometry and material, exportable as CSV.
* **Self-test suite** — 12 built-in validation tests covering the FFT, Lewis factors, viscosity model, λ monotonicity, bearing frequency ordering, unit conversion, and export formats.

### Quality of Life (new in MK-III)

* Metric / imperial unit switching (persisted)
* Design library — save, load, and delete named configurations in browser storage
* PNG snapshot export of the 3D view
* Keyboard shortcuts: **Space** pause, **G** regenerate, **R** reset camera, **1–6** switch tabs

### Export Tools

* CSV telemetry export (now including film λ and stress safety factors)
* JSON configuration export/import
* R&D report export
* Predictive maintenance plan export
* BOM cost estimate export
* SVG export
* DXF export
* STL export
* GLB export
* PNG snapshot export
* GIF animation export

---

## How to Run

### Recommended Method

1. Save the full app code as:

```text
index.html
```

2. Open the file in a modern browser such as Chrome, Edge, Firefox, or Safari.

3. For best results, use a local development server. In VS Code, install the **Live Server** extension, then right-click `index.html` and choose **Open with Live Server**.

### Avoid W3Schools TryIt for Full Testing

The app may run inside W3Schools TryIt, but that environment injects ads, sandbox iframes, trackers, and additional scripts. This can create console warnings that are not caused by the simulator.

Common W3Schools/browser noise includes:

```text
Attestation check for Topics failed
pubads_impl.js warnings
iframe sandbox warnings
This ad's html cannot be accessed
impressions.onelink failed
Grammarly-check.js errors
```

These messages are normally unrelated to the generator app.

---

## Required Browser Libraries

The app loads several browser libraries from CDNs:

* Three.js
* OrbitControls
* SVG.js
* Cannon.js
* Chart.js
* GIF.js
* GLTFExporter
* STLExporter

The physics engine should use the non-module browser build of Cannon.js:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/cannon.js/0.6.2/cannon.min.js"></script>
```

Do **not** load `cannon-es.js` with a normal `<script>` tag. `cannon-es` is an ES module and can cause this error:

```text
Unexpected token 'export'
```

---

## Basic Usage

1. Open the app.
2. Select a preset or adjust the design controls manually.
3. Press **Start** to begin simulation.
4. Use the tabs to switch between:

   * Design
   * Environment
   * Diagnostics
   * R&D Lab
   * Export
5. Monitor live telemetry and warnings.
6. Use export tools to save configurations, reports, models, or telemetry.

---

## Recommended Workflow

### 1. Create a Baseline

Start with a moderate RPM, load, and cooling setting. Confirm that temperature, vibration, and health remain stable.

### 2. Tune the Mechanical Design

Adjust:

* Gear ratio
* Tooth count
* Gear module
* Shaft diameter
* Clearance
* Material
* Gear type

Watch temperature, vibration, resonance margin, and efficiency.

### 3. Run Diagnostics

Use fault injection to simulate issues such as wear, imbalance, tooth damage, or cooling failure. Review the event log and anomaly score.

### 4. Use the R&D Lab

Run:

* Design optimizer
* Monte Carlo reliability test
* Stress test
* Apply Best Control

Then review survival probability, risk index, and remaining useful life estimate.

### 5. Export Results

Export a JSON configuration, CSV telemetry file, R&D report, or maintenance plan.

---

## Troubleshooting

### `openTab is not defined`

This usually means the JavaScript failed earlier before the tab function loaded. Check for syntax errors above this message in the console.

Most common cause:

```js
].join('
');
```

accidentally becoming a literal broken newline like:

```js
].join('
');
```

The correct form must be a single-line escaped newline:

```js
].join('\\n');
```

When written inside the actual app source, it should appear as:

```js
].join('\n');
```

### `Unexpected token 'export'`

You are loading an ES module file with a normal script tag. Replace `cannon-es.js` with the browser-safe Cannon.js build:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/cannon.js/0.6.2/cannon.min.js"></script>
```

### `AudioContext creation attempt blocked`

Browsers often block audio until the user interacts with the page. Click a button or enable audio after the page loads.

### `WebGL: INVALID_VALUE: texImage2D: no video`

This can happen in sandboxed preview environments or with blocked media resources. Try running the app from a local file or local server.

### Many Ad or Privacy Console Errors

If you see messages from `pubads_impl.js`, `googletag`, `onelink`, `quantcast`, `flashb`, or iframe sandbox warnings, those are likely from the hosting page, not from this app.

---

## Export File Types

### CSV

Exports telemetry data including time, RPM, temperature, power, torque, efficiency, vibration, health, anomaly score, lubrication index, bearing life, RUL, risk index, survival probability, voltage, current, power factor, and resonance margin.

### JSON

Exports the current configuration and simulation snapshot. This can be imported later to restore a design.

### SVG / DXF

Exports 2D drawing or schematic-style geometry.

### STL / GLB

Exports simple 3D model geometry for viewing or downstream prototyping workflows.

### GIF

Exports a short animation of the current visual state.

### Markdown Maintenance Plan

Exports a predictive maintenance plan based on current risk, lubrication, resonance, and remaining-life estimates.

---

## Simulation Notes

The simulator combines simplified models for:

* Gear friction
* Thermal rise
* Load effects
* Vibration (including synthesized spectra with shaft, gear-mesh, and bearing defect components)
* Efficiency
* Electrical output
* Lubrication degradation (Vogel viscosity-temperature + EHL film λ ratio)
* Gear tooth bending stress (Lewis equation with Barth dynamic factor)
* Gear contact stress (Hertzian, per-material elastic coefficients)
* Bearing L10-style life estimation
* Miner's-rule fatigue accumulation over mission profiles
* Resonance margin
* Fault severity
* Risk scoring
* Remaining useful life

The engineering formulas (Lewis, Hertz, L10, Miner, bearing defect frequencies) are textbook methods applied with assumed geometry factors. They are far better than arbitrary heuristics for exploring trends, but they are still not a substitute for a full ISO 6336 / AGMA rating or measured data.

These models are intentionally approximate and designed for interactive exploration, not for final engineering validation.

---

## Safety Disclaimer

Do not use this app alone to design, manufacture, certify, or operate real rotating machinery. Real generators, gear trains, shafts, bearings, and rotating assemblies can fail dangerously if improperly designed. Always perform proper mechanical analysis, electrical analysis, thermal testing, material validation, guarding, and safety review before building physical hardware.

---

## Suggested Improvements

Implemented in MK-III: real FFT vibration analysis, mission profile editor, efficiency island maps, BOM and cost estimator, improved bearing and lubricant models (Vogel viscosity + EHL λ ratio), gear tooth stress calculation (Lewis + Hertz), unit system switching, project save/load manager (design library), and a validation self-test suite.

Future upgrades could include:

* Thermal finite-difference model (multi-node gear/housing/oil network)
* Order-tracking and waterfall spectrum displays
* Offline library bundling
* ISO 6336 / AGMA 2101 full rating method
* Gearbox housing modal analysis for resonance modes
* WebGPU-accelerated particle and physics simulation

---

## License

Add your preferred license here. For personal experiments, a simple MIT License is usually suitable. For commercial or safety-related use, consult a legal professional and qualified engineers.

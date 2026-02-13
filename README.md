````markdown
# Rotary-Generator

**Rotary-Generator** is a lightweight, browser-first prototype/spec for an **interactive rotary generator + gearbox design environment**. It focuses on capturing the full parameter surface you’d expect in an engineering-oriented configurator (power/RPM/efficiency, gear topology, shaft sizing, environment variables), plus a pipeline for **visualization + export** (2D schematic, 3D model, CAD, telemetry).

At the moment, this repo contains **two UI/spec pages** (`index.html` and `beta.html`) that outline the intended controls, outputs, and export formats.

---

## What’s in this repo (current)

- **`index.html`** — *“Advanced Rotary Generator”* spec/UI: full parameter entry + visualization toggles + broad export menu.
- **`beta.html`** — *“Ultra Rotary Generator MK-II”* spec/UI: adds simulation throttle, cooling, audio toggles, particles, and physics-collision intent (Cannon.js mentioned), plus live KPI readouts.
- **`README.md`** — you’re reading it.

> This project is presently a **prototype/specification layer** (UI text + feature surface). The computational engine + rendering/export implementation can be layered in next.

---

## Feature surface (as specified)

### Core electrical + mechanical targets
- **Target / Output Power (W)**
- **Operating speed (RPM)**
- **Efficiency (%)**
- **Dimensions (L×W×H in mm)**

### Gear train configuration
- **Gear system type** (e.g., Spur / Bevel / Helical / Worm / Rack / Planetary)
- **Number of gears / stages**
- **Gear ratio**
- **Tooth count per gear**
- **Axial offset (mm)** (relevant to helical/bevel staging)
- **Shaft diameter (mm)**
- **Involute tooth profile toggle**

### Materials + appearance
- Structural/material selection (e.g., Aluminum/Steel/Titanium/Composite/Carbon Fiber)
- Color scheme presets (Default/Grayscale/Neon/Custom)
- Custom color picking

### Analysis + visualization toggles
- Mesh detail toggle (high-detail visual mesh)
- Stress analysis overlay (conceptual stress distribution view)
- CAD detail overlay (gear-by-gear computed parameters)
- Physics simulation toggle
- Camera + view controls (zoom, Euler angles)
- Motion trails (toggle + length)

### Environment + operating conditions
- Gravity (m/s²)
- Temperature (°C)
- Pressure (kPa)
- Vibration frequency (Hz)
- Cooling system efficiency (beta)

### Telemetry / live KPIs (beta intent)
- RPM
- Torque (Nm)
- Core temp (°C)
- Efficiency (%)
- Battery storage (%)

### Export surface (as specified)
- **2D**: PNG, SVG (schematic/blueprint)
- **3D**: STL, GLB (and animated GLB)
- **Media**: Animated GIF render
- **Data**: Specs JSON, Performance CSV / Telemetry CSV
- **CAD**: DXF export

---

## Quick start

### Option A — open directly
1. Download or clone the repo:
   ```bash
   git clone https://github.com/kai9987kai/Rotary-Generator.git
   cd Rotary-Generator
````

2. Open either file in your browser:

   * `index.html` (Advanced)
   * `beta.html` (MK-II)

### Option B — run a tiny local server (recommended for future export/runtime work)

Some browser features (file saving, module imports, fetch, workers) behave better over HTTP:

```bash
# Python 3
python -m http.server 8000
# then open:
# http://localhost:8000/index.html
# http://localhost:8000/beta.html
```

---

## Engineering model (recommended baseline for implementation)

If/when you wire the UI into calculations, the minimum viable physics typically looks like:

### Angular speed

[
\omega = \frac{2\pi \cdot RPM}{60}
]

### Mechanical ↔ electrical power relationship

If the generator efficiency is expressed as (\eta \in [0,1]):
[
P_{elec} = \eta \cdot P_{mech}
\quad\Rightarrow\quad
P_{mech} = \frac{P_{elec}}{\eta}
]

### Torque from power + RPM

[
\tau = \frac{P_{mech}}{\omega}
]

### Gear ratio propagation (common convention)

If gear ratio (G = \frac{\omega_{in}}{\omega_{out}}):
[
RPM_{out} = \frac{RPM_{in}}{G}
\quad,\quad
\tau_{out} \approx \tau_{in} \cdot G \cdot \eta_{gear}
]

Where (\eta_{gear}) is a per-stage efficiency (spur/helical typically higher than worm).

> This gives you enough to drive the live KPIs (RPM/Torque/Efficiency) and to generate plausible “performance CSV” output.

---

## Suggested Specs JSON shape (for `Export Specs JSON`)

A practical JSON payload that matches the repo’s parameter surface:

```json
{
  "design": {
    "target_power_w": 500,
    "rpm_in": 1800,
    "efficiency_pct": 92,
    "dimensions_mm": { "l": 120, "w": 80, "h": 90 },
    "material": "Steel"
  },
  "gear_train": {
    "type": "Helical",
    "stages": 3,
    "gear_ratio": 6.0,
    "teeth_per_gear": [18, 54, 20, 40, 16, 32],
    "axial_offset_mm": 2.5,
    "shaft_diameter_mm": 12,
    "involute_profile": true
  },
  "environment": {
    "gravity_mps2": 9.81,
    "temperature_c": 25,
    "pressure_kpa": 101.3,
    "vibration_hz": 0
  },
  "viz": {
    "color_scheme": "Default",
    "custom_color": "#2f6cff",
    "mesh_details": true,
    "stress_overlay": false,
    "cad_details": true,
    "physics_sim": false,
    "camera": { "zoom": 1.2, "rx": 15, "ry": 35, "rz": 0 },
    "trail": { "enabled": false, "length": 120 }
  },
  "exports": {
    "enabled": ["png2d", "svg2d", "stl3d", "dxf", "json", "csv", "gif", "glb"]
  }
}
```

---

## Roadmap (high-value next steps)

1. **Convert the spec pages into real HTML UI** (form inputs + state model).
2. **Computation core**:

   * power/RPM/torque math
   * staged gear propagation + per-stage efficiency
3. **2D schematic renderer**:

   * Canvas + SVG blueprint output
4. **3D renderer + exports**:

   * Three.js scene + STL/GLB export
5. **Telemetry recorder**:

   * sample loop → CSV download
6. **Optional “beta” extras**:

   * Web Audio API “engine sound”
   * particle heat/sparks
   * physics collisions (e.g., cannon-es)

---

## Contributing

PRs/issues are welcome—especially for:

* implementing the UI as functional controls
* adding a calculation engine + validation (units, ranges, gear constraints)
* exporters (SVG/DXF/STL/GLB)
* visualization improvements (stress map mock, CAD annotations)

---

## License

There is currently **no `LICENSE` file** in the repository.
If you want others to use/modify/distribute this project, add a license (MIT, Apache-2.0, GPL-3.0, etc.).

---

## Author

**Kai Piper** ([@kai9987kai](https://github.com/kai9987kai))

```

If you want, I can also generate a **README that matches GitHub Pages style** (with a feature GIF section, shields badges, and a tighter “product pitch”) while still staying accurate to what’s currently in the repo.
::contentReference[oaicite:0]{index=0}
```

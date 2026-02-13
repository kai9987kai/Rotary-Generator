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

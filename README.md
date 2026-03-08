# ShaderGradient Playground

![Three.js](https://img.shields.io/badge/Three.js-r128-black?style=flat-square&logo=threedotjs&logoColor=white)
![GLSL](https://img.shields.io/badge/GLSL-Shaders-5586A4?style=flat-square)
![Vanilla JS](https://img.shields.io/badge/Vanilla-JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![No Dependencies](https://img.shields.io/badge/Zero_Build-Single_HTML_File-22C55E?style=flat-square)
![Export](https://img.shields.io/badge/Export-GIF_%7C_WebM_%7C_MP4-6366F1?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-gray?style=flat-square)

**[🚀 Live Demo](https://julianhilgemann.github.io/shadergradient)**

A browser-based, real-time shader gradient simulator built on Three.js and custom GLSL. Dial in animated mesh gradient visuals — spheres, planes, water planes — and export them as looping GIFs or videos. No install, no build step: open the HTML file and go.

![ShaderGradient Playground screenshot](main_screenshot.png)

---

## What It Does

The playground renders a live, animating gradient mesh using a custom simplex-noise vertex shader. Three gradient colors are blended across the displaced geometry based on noise value. Every parameter is tweakable in real time via the control panel, and the current state can be exported as a looping animation or copied as a `<ShaderGradient />` JSX snippet for use in React projects.

---

## Features

### 🎨 Colors & Lighting
- **3 gradient color stops** — fully customizable via color pickers
- **Scene background color** — quick-access presets + custom picker
- **Brightness & reflection** controls for surface shading
- **Light type** — `3d` (directional with specular) or `env` (environment-based)
- **Environment presets** — `city`, `dawn`, `night`

### 🔷 Geometry & Noise
- **3 geometry types** — `sphere`, `plane`, `waterPlane`
- **Noise controls** — amplitude, density, frequency, strength
- **Mesh rotation** — X / Y / Z axes (–180° to 180°)
- **Display toggles** — wireframe mode, grain overlay, axes helper

### 📷 Camera
- **Spherical positioning** — distance, azimuth angle, polar angle
- **Lens controls** — zoom, field of view
- **Orbit controls** — drag the canvas to orbit freely
- **One-click camera reset**

### ⏱ Animation
- **Play / pause** toggle
- **Speed** (`uSpeed`) and **loop duration** controls
- **Pixel density** — up to 3× for sharper renders
- **uTime scrub** — manually seek through the animation cycle

### 🧊 Frosted Glass Overlay
Apply a glassmorphism layer over the canvas for compositional previews:
- **Blur intensity** (0–80px)
- **Saturation** multiplier
- **Tint color + fill opacity**
- **Border opacity**
- Quick-load glass presets: `Frosted Light`, `Frosted Dark`, `Heavy`, `Subtle`, `Tinted`

### 💾 Preset System
- **12 built-in presets** covering a range of moods and geometries
- **Save your own presets** — named, timestamped, stored in `localStorage`
- **Delete** individual user presets
- One-click load with visual color preview dots

### 📤 Export

#### GIF
- Resolution: `480p`, `720p`, `1080p`, `4K`
- Frame rate: `10`, `15`, `24 fps`
- Encoded entirely in-browser using [omggif](https://github.com/deanm/omggif) + a frequency-based median-cut palette quantiser
- Live progress bar + estimated file size

#### Video
| Format | Notes |
|---|---|
| WebM (VP9) | Via `MediaRecorder` API — broad browser support |
| MP4 (H.264) | Via `VideoEncoder` (WebCodecs) — Chrome 94+ |

- Resolution: `720p`, `1080p`, `2K`, `4K`
- Frame rate: `24`, `30`, `60 fps`
- Live progress + estimated file size

### 📋 JSX Code Output
Generates a ready-to-paste `<ShaderGradient />` component string reflecting the current state — all props included. Click the code block to copy to clipboard.

---

## Usage

```bash
# Just open it
open gradient_simulator.html
```

No server required. All rendering and encoding happens client-side. For video export at higher resolutions, a modern Chromium-based browser is recommended.

---

## Controls Reference

| Section | Parameter | Range |
|---|---|---|
| Colors | `color1–3` | Hex color |
| Colors | `brightness` | 0.1 – 3.0 |
| Colors | `reflection` | 0 – 1.0 |
| Shape | `uAmplitude` | 0 – 5 |
| Shape | `uDensity` | 0.1 – 5 |
| Shape | `uFrequency` | 0 – 20 |
| Shape | `uStrength` | 0 – 3 |
| Camera | `cDistance` | 1 – 30 |
| Camera | `cAzimuthAngle` | 0° – 360° |
| Camera | `cPolarAngle` | 0° – 180° |
| Camera | `cameraZoom` | 1 – 50 |
| Camera | `fov` | 10° – 120° |
| Animation | `uSpeed` | 0 – 2 |
| Animation | `loopDuration` | 2 – 60s |
| Animation | `pixelDensity` | 0.5 – 3× |

---

## Tech Stack

| Layer | Technology |
|---|---|
| 3D Rendering | [Three.js r128](https://threejs.org/) |
| Shaders | Custom GLSL (simplex noise, per-vertex displacement) |
| Orbit Controls | `THREE.OrbitControls` |
| GIF Encoding | [omggif](https://github.com/deanm/omggif) |
| MP4 Encoding | WebCodecs API + [mp4-muxer](https://github.com/Vanilagy/mp4-muxer) |
| Video Capture | `MediaRecorder` + Canvas `captureStream` |
| Persistence | `localStorage` (user presets) |

---

## Export Tips

- For the cleanest loop, set **uTime = 0** before exporting and keep `uSpeed` low
- GIF palette quality improves at lower resolutions — `720p` at `10fps` is a good default
- WebM export requires the renderer canvas to be at least 1px visible; the exporter handles this automatically
- 4K GIF exports can exceed 150MB — a warning is shown in the size estimate

---

## License

MIT

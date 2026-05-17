# Range WebAR Exporter

**Export your Blender scenes to Augmented Reality on any mobile browser — no app required.**

Range WebAR Exporter is a Blender 2.79 addon that takes your 3D models and turns them into a self-contained WebAR experience: a folder with an `index.html` you can upload to any web host and open on a phone.

Under the hood it uses **Three.js** and **WebXR**, following an 8thWall-style workflow — a static GLB model plus a JavaScript animation layer.

---

## What you can do with it

- Place 3D models on real-world surfaces with **Surface Placement** (hit-test)
- Anchor models to printed images with **Image Tracking**
- Preview models in a plain 3D viewer with no AR
- Add **JS-driven animations** (rotation, float, pulse, spin) without baking keyframes
- Make objects **interactive** — tap to trigger actions
- Add **hotspot annotations** with text, image, audio, and links
- Configure **materials** with Classic (Phong) or PBR shading
- Wire up behaviors visually with the **WebAR Node Tree**

---

## Requirements

| Requirement | Details |
|---|---|
| Blender | 2.79 |
| Browser | Chrome or Safari on iOS/Android with WebXR support |
| HTTPS | Required for real AR (Surface Placement, Image Tracking). Not needed for Viewer mode. |

---

## How it works

```
Blender Scene  ──►  Range WebAR Exporter  ──►  webar_output/
                                                 ├── index.html
                                                 ├── scene.glb
                                                 ├── scene.json
                                                 ├── styles.css
                                                 ├── runtime/
                                                 └── textures/
```

The exporter produces a ready-to-deploy folder. Upload it to any static web host (GitHub Pages, Netlify, your own server) and share the URL.

---

## Quick navigation

<div class="grid cards" markdown>

- :material-download: **[Installation](getting-started/installation.md)**  
  Install the addon in Blender 2.79

- :material-rocket-launch: **[Quick Start](getting-started/quickstart.md)**  
  Export your first scene in 5 minutes

- :material-tune: **[Main Panel](panels/main-panel.md)**  
  All scene-level export settings

- :material-cube: **[Object Panel](panels/object-panel.md)**  
  Per-object behavior, materials, hotspots

- :material-graph: **[Node Tree](nodes/introduction.md)**  
  Visual wiring of animations and events

- :material-file-code: **[scene.json Reference](reference/scene-schema.md)**  
  Full schema for the exported scene file

</div>

---

## License

GPL v3 — see [license details](https://www.gnu.org/licenses/gpl-3.0.html).

# Output Files

After clicking **Export WebAR Scene**, the addon generates a self-contained folder ready for deployment.

---

## Folder structure

```
webar_output/
├── index.html          ← Entry point — open this in a browser
├── scene.glb           ← 3D model (or scene.gltf + scene.bin)
├── scene.json          ← Scene configuration and behavior data
├── styles.css          ← UI overlay styles
├── textures/           ← All texture and asset files
│   ├── diffuse.png
│   ├── normal.png
│   └── marker.jpg
└── runtime/            ← WebAR JavaScript runtime modules
    ├── runtime.js          ← Entry: config + initialization
    ├── runtime-loader.js   ← Three.js + WebXR scene setup
    ├── animation-system.js ← JS animations (rotate, float, pulse, spin)
    ├── interaction-system.js ← Gesture handling (drag, pinch)
    ├── hotspot-system.js   ← Hotspot rendering and popups
    ├── event-system.js     ← Event dispatch (tap, timer, update)
    ├── component-system.js ← Component runtime (node tree behaviors)
    ├── action-system.js    ← Action executor (toggle, set, play)
    ├── debug-overlay.js    ← FPS / stats overlay
    └── utils/
        ├── object-utils.js     ← Object helpers
        └── scene-validator.js  ← Runtime scene validation
```

---

## File descriptions

### index.html

The browser entry point. Loads the runtime and the UI overlay. This file references the other assets by relative path — the folder structure must be kept intact when deploying.

### scene.glb / scene.gltf

The 3D model exported from Blender. Contains geometry, UV maps, materials, and (if not in Static mode) animations.

GLB is a single binary file. glTF + Bin splits the JSON description and binary data into separate files — useful for inspecting or manually editing the scene graph.

### scene.json

The scene configuration. The runtime reads this on load to configure AR mode, interactions, object behaviors, components, events, and hotspots. See [scene.json Schema](scene-schema.md).

### textures/

All external texture files (normal maps, specular maps, ORM maps, reflection textures, hotspot images, hotspot audio, and the Image Tracking marker image) are copied here during export.

### runtime/

The JavaScript runtime. These files are copied from the addon's own `templates/runtime/` folder — you should not edit them manually. Re-exporting from Blender will overwrite any manual changes.

---

## Deploying

Upload the entire output folder contents to a static web host. The folder structure and relative paths must be preserved.

**Recommended hosts:**

| Host | Free plan | HTTPS | Notes |
|---|---|---|---|
| GitHub Pages | ✓ | ✓ (automatic) | Good for open projects |
| Netlify | ✓ | ✓ (automatic) | Drag-and-drop deploy |
| Vercel | ✓ | ✓ (automatic) | Similar to Netlify |
| Your own server | — | Needs SSL cert | Full control |

!!! warning "HTTPS is required for AR"
    Surface Placement and Image Tracking use WebXR APIs that only work on HTTPS. Viewer Mode works on HTTP.

---

## What you can safely customize

- `index.html` — you can add your own meta tags, analytics, or branding, but avoid removing the script tags that load the runtime
- `styles.css` — safe to edit for custom branding
- `textures/` — you can add more asset files; the runtime only loads what is referenced in `scene.json`

Do not rename or restructure the `runtime/` folder or `scene.json` — the runtime expects them at those paths.

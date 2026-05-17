# Main Panel

**Location:** View3D → Sidebar (`N` key) → **WebAR** tab

The main panel controls all scene-level settings. It is divided into sections.

---

## Export Settings

Controls what gets exported and how.

| Property | Type | Default | Description |
|---|---|---|---|
| **Output Path** | Directory | `//webar_output` | Folder where the exported files are written. `//` means relative to the `.blend` file. |
| **Format** | Enum | GLB | `GLB (Binary)` — single self-contained file. `glTF + Bin` — separate `.gltf` + `.bin` files (useful for inspecting the JSON). |
| **Export Materials** | Bool | ✓ | Include materials and textures in the exported GLB. |
| **Material Mode** | Enum | Classic | Shading model used by the WebAR runtime. See [Materials](../materials/classic.md). |
| **Double Sided** | Bool | ✓ | Render both faces of polygons (disables backface culling). |
| **Normal Map Scale** | Float 0–3 | `1.0` | PBR mode only. Intensity of the normal map. `1.0` = normal strength, `0` = flat, `2` = double. |
| **Export Lights** | Bool | ✓ | Include Blender lights in the GLB. |
| **Debug Overlay** | Bool | ✗ | Show a runtime stats overlay (FPS, draw calls). For development only. |

---

## Animation

Controls how animations are included in the export.

See [Animation Modes](animation-modes.md) for full details.

| Mode | Description |
|---|---|
| **Static (8thWall Style)** | Exports a GLB snapshot at the current frame. Animations are driven by JavaScript at runtime — lightweight and fast. **Recommended for most cases.** |
| **Skeletal (Bones)** | Exports armature skinning and animation clips. Use when your model has rigged character animations. |
| **Object Animation** | Exports baked object-level keyframes. Heavy — not recommended unless necessary. |

---

## AR Settings

Controls the augmented reality mode and placement behavior.

| Property | Type | Default | Description |
|---|---|---|---|
| **AR Mode** | Enum | Surface Placement | See [AR Modes](ar-modes.md). |
| **Reference Size** | Float | `1.0` | Target bounding-box size in meters after scaling. Set this to the real-world size of your object. |
| **Background Color** | Color | Dark gray | Scene background color. **Viewer Mode only.** |
| **Auto Rotate Speed** | Float 0–10 | `0.5` | Continuous Y-axis rotation speed. **Viewer Mode only.** `0` = disabled. |
| **Marker Image** | File | — | Marker image for **Image Tracking** mode (JPG or PNG). |
| **Marker Width (m)** | Float | `0.2` | Real-world width of the printed marker in meters. **Image Tracking only.** |
| **Shadow Plane** | Bool | ✓ | Project a shadow below the model onto the AR surface. **Surface Placement and Image Tracking only.** |
| **Shadow Opacity** | Float 0–1 | `0.5` | Transparency of the shadow plane. `0` = invisible, `1` = solid black. |

---

## UI Overlay

An optional overlay panel shown on top of the AR view.

| Property | Type | Default | Description |
|---|---|---|---|
| **UI Overlay** | Bool | ✓ | Show the title/instructions panel. |
| **UI Title** | String | `WebAR Experience` | Title text shown in the overlay header. |
| **Instructions** | String | `Tap to place...` | Instructional text shown below the title. |

The overlay also includes a **Reset** button that re-triggers the placement flow.

---

## Interactions

Global gesture settings applied after the model is placed.

| Property | Type | Default | Description |
|---|---|---|---|
| **Enable Tap** | Bool | ✓ | Allow tap/click events on objects. Required for interactive objects and hotspots. |
| **Gesture Rotate** | Bool | ✓ | Drag with one finger to rotate the model around the Y axis. |
| **Gesture Scale** | Bool | ✓ | Pinch with two fingers to scale the model up or down. |

---

## Auto Regenerate

| Property | Type | Default | Description |
|---|---|---|---|
| **Auto Regenerate** | Bool | ✗ | Watch the Node Tree for changes and flag when a re-export is needed. A "Changes detected!" warning appears when the scene has been modified since the last export. |

---

## Action Buttons

| Button | Description |
|---|---|
| **Export WebAR Scene** | Runs the full export pipeline. Shows a validation dialog if there are warnings. |
| **Preview in Browser** | Starts a local HTTP server and opens the exported scene in your default browser. Also shows the LAN URL for testing on a mobile device. |
| **Open Output Folder** | Opens the output folder in your file manager. |

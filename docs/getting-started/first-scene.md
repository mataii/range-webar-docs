# Your First AR Scene

A step-by-step walkthrough building a minimal but complete AR experience: a product model that the user can place on a surface, rotate with a finger swipe, and tap to trigger an animation.

---

## What we'll build

- A mesh object placed on a real surface (hit-test)
- The model auto-scales to a realistic size
- The user can rotate and scale it with gestures
- A shadow appears beneath the model
- A hotspot annotation with a description

---

## 1. Prepare the model

Open your `.blend` file with the model you want to export.

**Before exporting, make sure:**

- [ ] Apply all transforms: select all objects → `Ctrl+A` → **Scale** (unapplied scale causes glitches in the browser)
- [ ] The model has a UV map
- [ ] Textures are images (not procedural materials)
- [ ] Textures are power-of-2 dimensions: 256, 512, 1024, 2048 px (non-power-of-2 textures show a warning on export)

!!! tip "Origin at the base"
    Set the object origin to the bottom center of the model. That way the model sits on the AR surface instead of floating or sinking into it.

---

## 2. Configure the scene

Open the **WebAR** sidebar panel.

### Export Settings

| Setting | Value |
|---|---|
| Output Path | `//webar_output` (or your preferred folder) |
| Format | GLB (Binary) |
| Export Materials | ✓ |
| Material Mode | Classic |
| Export Lights | ✓ |

### Animation

Set **Animation Mode** to **Static (8thWall Style)**. This exports a clean GLB snapshot at the current frame — no heavy keyframe data, fast to load.

### AR Settings

| Setting | Value |
|---|---|
| AR Mode | Surface Placement |
| Reference Size | `0.3` (30 cm — adjust to match your model's real-world size) |
| Shadow Plane | ✓ |
| Shadow Opacity | `0.5` |

### UI Overlay

| Setting | Value |
|---|---|
| UI Overlay | ✓ |
| Title | Your product or experience name |
| Instructions | `Point at a flat surface and tap to place` |

### Interactions

| Setting | Value |
|---|---|
| Enable Tap | ✓ |
| Gesture Rotate | ✓ |
| Gesture Scale | ✓ |

---

## 3. Configure the object

Select your mesh in the 3D View. Go to **Properties → Object → WebAR Object**.

| Setting | Value |
|---|---|
| Export to WebAR | ✓ |
| AR Behavior | Static |

Under **Material (Classic)**:

| Setting | Value |
|---|---|
| Normal Map | (your normal map file, if you have one) |
| Shininess | `30` |

---

## 4. Add a hotspot (optional)

A hotspot is an annotation that floats in 3D space and shows a popup with text and images.

1. Press `Shift+A` → **Empty** → **Plain Axes**
2. Position it on part of the model where you want the annotation (e.g. on a button or feature)
3. In **Properties → Object → WebAR Object**, enable **Hotspot**
4. Fill in Title, Description, and optionally an Image or URL

---

## 5. Export and preview

1. Click **Export WebAR Scene**
2. Click **Preview in Browser**
3. On your phone, navigate to the LAN URL shown in Blender (e.g. `http://192.168.1.x:PORT/index.html`)

In Viewer Mode (no HTTPS needed), you'll see the 3D model. For full AR with surface detection, deploy to an HTTPS host.

---

## Troubleshooting quick checks

| Problem | Fix |
|---|---|
| Model is too big / too small | Adjust **Reference Size** to match the real-world size |
| Model sinks into the surface | Move the object origin to the base of the model |
| Textures missing | Make sure texture files are saved to disk (not packed) before exporting |
| AR button missing | Browser needs HTTPS — use a proper host, not the local preview |

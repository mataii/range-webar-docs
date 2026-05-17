# Quick Start

This guide gets you from a Blender scene to a working WebAR experience in about 5 minutes.

---

## Step 1 — Open the WebAR panel

In the **3D View**, press `N` to open the sidebar and click the **WebAR** tab.

---

## Step 2 — Set an output path

Under **Export Settings**, click the folder icon next to **Output Path** and choose where the exported files will go. The default is `//webar_output` (a folder next to your `.blend` file).

---

## Step 3 — Choose an AR Mode

Under **AR Settings**, select the AR mode that fits your use case:

| Mode | When to use |
|---|---|
| **Surface Placement** | The model appears on a flat surface (floor, table) when the user taps |
| **Viewer Mode** | Plain 3D viewer, no AR. Good for desktop testing. |
| **Image Tracking** | The model anchors to a printed image marker |

For a first test, **Viewer Mode** is easiest because it works over plain HTTP (no HTTPS needed).

---

## Step 4 — Mark your objects for export

Select an object and go to **Properties → Object** (the orange square icon). You will see a **WebAR Object** panel. Make sure **Export to WebAR** is checked.

By default all objects in the scene are marked for export.

---

## Step 5 — Export

Click **Export WebAR Scene** in the WebAR panel. The addon will:

1. Export the selected objects as a GLB or glTF file
2. Copy all required textures to a `textures/` subfolder
3. Generate `index.html`, `scene.json`, `styles.css`, and the `runtime/` JS modules

---

## Step 6 — Preview

Click **Preview in Browser**. The addon starts a local HTTP server and opens your browser. You'll see a URL like:

```
http://192.168.1.x:XXXXX/index.html
```

Type that URL on your phone (connected to the same Wi-Fi) to test on mobile.

!!! warning "HTTPS for real AR"
    Surface Placement and Image Tracking require HTTPS. The local preview server uses plain HTTP, so AR features will not activate during local preview. Use Viewer Mode to test locally, then deploy to an HTTPS host for full AR.

---

## Step 7 — Deploy

Upload the entire contents of your output folder to any static web host:

- **GitHub Pages** (free, HTTPS automatic)
- **Netlify** (free tier, drag-and-drop deploy)
- Your own server with an SSL certificate

Share the URL and open it on a phone.

---

## What's next?

- [Configure per-object behaviors](../panels/object-panel.md) (animations, interactions)
- [Add hotspot annotations](../panels/hotspots.md)
- [Set up materials](../materials/classic.md)
- [Use the Node Tree](../nodes/introduction.md) for visual behavior wiring

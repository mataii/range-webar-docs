# FAQ

---

**Does this work with Blender 2.8 or later?**

No. The addon was built for **Blender 2.79** and uses its Python API. It is not compatible with Blender 2.8+ due to API changes in how properties, panels, and the glTF exporter work.

---

**Do users need to install an app?**

No. The exported experience runs entirely in the mobile browser using WebXR. Users just open a URL.

---

**Which browsers support it?**

- **Android:** Chrome (ARCore support required for Surface Placement)
- **iOS:** Safari 15.4+ (ARKit support required for Surface Placement)
- **Desktop:** Viewer Mode works in any modern browser. AR modes require a WebXR-capable browser with camera access.

---

**Does it work without HTTPS?**

Viewer Mode works over HTTP. Surface Placement and Image Tracking require HTTPS because WebXR camera access is a secure-context API.

---

**Can I use Blender 2.79 procedural textures?**

Not directly. The exporter uses the GLB format, which only supports image textures. You need to bake procedural textures to image files before exporting.

---

**Why is the model the wrong size in AR?**

Set **Reference Size** to the real-world size of the object in meters. For a 20 cm figurine, set `0.2`. The runtime scales the model's bounding box to match that size.

---

**Can I use this for commercial projects?**

The addon is licensed under GPL v3. The exported HTML/JS/JSON output is yours to use freely in any project.

---

**What is the recommended texture size?**

- **1024×1024** for most objects — good quality, fast load
- **2048×2048** for hero objects with fine detail
- Keep total texture memory under ~50 MB for smooth mobile performance

All textures should have power-of-2 dimensions (256, 512, 1024, 2048).

---

**Can I add my own JavaScript to the exported scene?**

Yes. You can edit `index.html` to add custom `<script>` tags. The `scene.json` and the runtime are just files — you can load them and extend the runtime freely.

For per-object interactions without custom JS, use the **On Click JS** field in the Object panel or the **Tap** event node.

---

**The AR Interaction node is deprecated — what do I use instead?**

Use the **Tap** node in the node tree. It does everything the AR Interaction node was meant to do and actually exports data (the AR Interaction node is present but does not compile to output).

---

**Can I deploy to multiple pages / embed in an existing site?**

Yes. Upload the output folder to your server and embed it in a WordPress page using an iframe:

```html
<iframe src="https://yoursite.com/webar_output/index.html"
        width="100%" height="600px" allow="camera; xr-spatial-tracking">
</iframe>
```

The `allow="camera; xr-spatial-tracking"` attribute is required for AR to work inside an iframe.

---

**Where is the node tree data stored?**

Node trees are stored inside the `.blend` file as a custom `WEBARNodeTree` data block. They are compiled and baked into `scene.json` at export time — the runtime does not read the `.blend` file.

# AR Modes

The **AR Mode** setting controls how the 3D model is placed in the real world.

**Location:** WebAR panel → AR Settings → **AR Mode**

---

## Surface Placement (Hit Test)

The user points their camera at a flat surface (floor, table, desk). When a surface is detected, a placement indicator appears. The user taps to drop the model there.

**Best for:** product visualization, furniture, architectural models, anything that should rest on a surface.

**Requirements:**
- HTTPS (WebXR hit-test requires a secure context)
- A device with ARCore (Android) or ARKit (iOS)

**Settings available with this mode:**

| Setting | Description |
|---|---|
| Reference Size | Controls how large the model appears relative to reality |
| Shadow Plane | Adds a shadow cast below the model |
| Gesture Rotate | Allow drag-to-rotate after placement |
| Gesture Scale | Allow pinch-to-scale after placement |

---

## Viewer Mode

Displays the model in a plain 3D scene — no AR, no camera feed. The model floats in front of the user and can be auto-rotated or manually rotated.

**Best for:** 3D product viewers, desktop previews, testing without HTTPS.

**Requirements:** Any modern browser. No HTTPS needed. No special device.

**Settings available with this mode:**

| Setting | Description |
|---|---|
| Background Color | Scene background (the camera feed is replaced by this color) |
| Auto Rotate Speed | Continuous Y-axis rotation (`0` = off) |
| Gesture Rotate | Manual rotation with drag |
| Gesture Scale | Pinch to scale |

!!! tip "Use Viewer Mode for local testing"
    The local preview server (`Preview in Browser`) uses plain HTTP, so Surface Placement and Image Tracking won't activate. Set the mode to Viewer for quick iteration, then switch and re-export before deploying.

---

## Image Tracking

The model anchors and tracks a specific printed image (a "marker"). The model appears on top of the image and moves with it if the image moves.

**Best for:** packaging AR, print media, business cards, product inserts.

**Requirements:**
- HTTPS
- A printed marker image (JPG or PNG)
- The marker must be flat and clearly visible to the camera

**Additional settings:**

| Setting | Description |
|---|---|
| Marker Image | Path to the JPG or PNG used as the tracking target |
| Marker Width (m) | Real-world width of the printed marker in meters. This sets the scale of the model relative to the marker. |

!!! warning "Marker image tips"
    Use images with high contrast and rich detail — solid colors and simple gradients track poorly. Avoid symmetrical images (the tracker can't determine orientation). A minimum print size of 10×10 cm is recommended.

---

## Comparison

| Feature | Surface Placement | Viewer Mode | Image Tracking |
|---|---|---|---|
| HTTPS required | ✓ | ✗ | ✓ |
| Works on desktop | ✗ | ✓ | ✗ |
| Needs printed marker | ✗ | ✗ | ✓ |
| Model tracks camera | ✗ | ✓ | ✓ |
| Shadow plane | ✓ | ✗ | ✓ |
| Auto-rotate | ✗ | ✓ | ✗ |

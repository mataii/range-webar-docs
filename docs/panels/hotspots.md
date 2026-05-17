# Hotspots

Hotspots are interactive annotation points anchored to positions in 3D space. In the AR scene they appear as floating icons — tap one to open a panel with a title, description, image, audio, or a link.

---

## Creating a hotspot

Hotspots are created from **Empty** objects.

1. Press `Shift+A` → **Empty** → **Plain Axes** (or any Empty type)
2. Position the Empty where you want the annotation to appear in AR space
3. In **Properties → Object → WebAR Object**, check **Hotspot**
4. Fill in the hotspot fields

!!! tip "Placement tip"
    Think in 3D: position the Empty at the feature you want to annotate — on a button, near a connector, above a component. The runtime converts Blender's Z-up coordinates to Three.js Y-up automatically.

---

## Hotspot properties

| Property | Type | Description |
|---|---|---|
| **Hotspot** | Bool | Enables this Empty as a hotspot. |
| **Icon** | Enum | The icon shown for the floating marker. |
| **Title** | String | Header text shown in the popup panel. |
| **Description** | String | Body text shown below the title. |
| **Image** | File (JPG/PNG) | Optional image shown in the panel. |
| **URL** | String | Optional external link opened in a new browser tab. |
| **Audio** | File (MP3/OGG) | Optional audio clip played when the hotspot is opened. |

---

## Icons

| Value | Appearance |
|---|---|
| `info` | ℹ️ Information circle |
| `star` | ⭐ Star |
| `camera` | 📷 Camera |
| `location` | 📍 Location pin |

---

## Multiple hotspots

You can have as many hotspots as needed. Add one Empty per annotation point. Each gets its own name and content.

A common pattern for a product model:

```
Empty "MotorInfo"    → position: top of the motor
Empty "ChargePort"   → position: USB port area
Empty "SerialLabel"  → position: bottom plate
```

---

## Coordinate system

Hotspot positions are stored in **Three.js Y-up** space. The exporter automatically converts from Blender's Z-up:

```
Blender (X, Y, Z) → Three.js (X, Z, −Y)
```

You don't need to do anything — just position the Empty normally in Blender.

---

## Asset files

Images and audio files are copied to the `textures/` subfolder of the output directory during export. Use relative paths in the hotspot fields (the file picker in Blender handles this automatically).

**Supported formats:**

| Asset | Formats |
|---|---|
| Image | `.png`, `.jpg`, `.jpeg`, `.webp`, `.gif` |
| Audio | `.mp3`, `.ogg` |

---

## Example output in scene.json

```json
{
  "id": "MotorInfo",
  "position": [0.0, 0.35, 0.12],
  "title": "Main Motor",
  "description": "500W motor with liquid cooling.",
  "image": "textures/motor_detail.jpg",
  "audio": "",
  "url": "https://example.com/product",
  "icon": "info"
}
```

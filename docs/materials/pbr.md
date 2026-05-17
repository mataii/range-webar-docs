# PBR Materials

PBR (Physically Based Rendering) mode uses **metallic/roughness** shading. It produces more realistic results than Classic mode, especially for metals, plastics, and surfaces with varied material properties.

**Enable it:** WebAR panel → Export Settings → Material Mode → **PBR**

---

## How it works

The runtime uses Three.js `MeshStandardMaterial`. The base color comes from the GLB's embedded material. Additional maps are specified per-object in the **WebAR Object** panel.

---

## Per-object material properties

These appear in **Properties → Object → WebAR Object → Material (PBR)** when Export Materials is enabled.

| Property | Type | Description |
|---|---|---|
| **Normal Map** | File (PNG/JPG) | Tangent-space normal map. Same as Classic mode. |
| **ORM Map** | File (PNG/JPG) | Combined texture: **R** = Occlusion, **G** = Roughness, **B** = Metalness. Preferred over separate maps. |
| **Roughness Map** | File (PNG/JPG) | Roughness (channel R). **Ignored if an ORM map is set.** |
| **Metalness Map** | File (PNG/JPG) | Metalness (channel R). **Ignored if an ORM map is set.** |

---

## ORM map explained

The ORM (or ARM) texture packs three maps into one file to save memory and texture slots:

| Channel | Data | Range |
|---|---|---|
| Red (R) | Ambient Occlusion | 0 = occluded (dark), 1 = fully lit |
| Green (G) | Roughness | 0 = mirror smooth, 1 = fully rough |
| Blue (B) | Metalness | 0 = non-metal, 1 = fully metallic |

Most 3D tools (Substance Painter, Marmoset, etc.) can export ORM directly. If yours doesn't, you can combine separate maps in Photoshop or any image editor by placing each map in the correct channel.

---

## Normal Map Scale

A global setting in the main panel (Export Settings → Normal Map Scale) that adjusts the strength of all normal maps in PBR mode.

| Value | Effect |
|---|---|
| `0.0` | No normal map effect (flat) |
| `1.0` | Full strength (default) |
| `2.0` | Doubled intensity |
| `3.0` | Maximum (may look exaggerated) |

---

## Transparency

Same as Classic mode. See [Classic Materials → Transparency](classic.md#transparency).

---

## PBR vs Classic — when to choose

| Situation | Recommendation |
|---|---|
| Low-end mobile devices or many objects | Classic |
| Metals, plastics, realistic surfaces | PBR |
| Stylized or cartoon look | Classic |
| You have Substance Painter textures | PBR |
| You have a diffuse + specular workflow | Classic |

---

## Tips for PBR mode

- Always use an **ORM map** if possible — it's more efficient than three separate textures
- Metalness should be close to `0` or `1` — avoid middle values on real materials (metal or not metal, rarely in between)
- Roughness `0.0–0.1` = mirror surface (polished chrome), `0.5` = plastic, `0.9–1.0` = chalk or rough concrete
- Keep normal maps in **linear** color space (not sRGB) when exporting from your texture tool

# Classic Materials (Phong)

Classic mode uses **Phong shading** — the traditional real-time shading model. It's simpler to set up than PBR and performs well on low-end mobile devices.

**Enable it:** WebAR panel → Export Settings → Material Mode → **Classic**

---

## How it works

The Blender material's diffuse texture (the base color image assigned in the material) is used as the main color. Additional maps are specified directly in the **WebAR Object** panel for each mesh.

The runtime combines them using Three.js `MeshPhongMaterial`.

---

## Per-object material properties

These appear in **Properties → Object → WebAR Object → Material (Classic)** when Export Materials is enabled.

| Property | Type | Description |
|---|---|---|
| **Normal Map** | File (PNG/JPG) | Tangent-space normal map. Adds surface detail without extra polygons. |
| **Specular Map** | File (PNG/JPG) | Controls which areas are shiny (white = shiny, black = matte). |
| **Shininess** | Float 0–1000 | Size of the specular highlight. `0` = matte, `30` = plastic-like, `500+` = very glossy. |
| **Reflection** | Float 0–1 | Intensity of the environment reflection. `0` = none, `1` = mirror-like. |
| **Reflection Map** | File (PNG/JPG) | Texture used as the environment reflection. Mapped using reflection coordinates (like Blender's Reflection mapping). Only visible if Reflection > 0. |

---

## Transparency

| Property | Type | Description |
|---|---|---|
| **Alpha Mode** | Enum | How transparency is handled for this object. |
| **Alpha Cutoff** | Float 0–1 | Threshold for Mask mode. Pixels below this alpha value are discarded. |

**Alpha Mode values:**

| Value | Use case |
|---|---|
| **Opaque** | No transparency. |
| **Mask (Cutout)** | Binary transparency — pixels are either fully visible or fully invisible. Good for foliage, fences, grids, fabric with holes. |
| **Blend** | Smooth transparency. Good for glass, smoke, particles, effects. |

!!! warning "Blender 2.79 transparency export"
    Blender 2.79's glTF exporter does not correctly export alpha modes. The **Alpha Mode** setting in the WebAR Object panel overrides this, applying the correct mode in the runtime. Always set it manually per object when transparency is needed.

---

## Texture format requirements

- Formats: `.png`, `.jpg`, `.jpeg`, `.webp`, `.gif`
- Dimensions: powers of 2 (256, 512, 1024, 2048 px) for best mobile GPU compatibility
- Color space: sRGB for color textures, linear for normal/specular maps

---

## Tips for Classic mode

- **Shininess 30** is a good starting point for plastic or painted surfaces
- **Shininess 200–500** for metal or polished surfaces
- Use a **Specular Map** to vary shininess across the surface (e.g. scratches = less shiny)
- **Reflection** + a spherical reflection texture gives a convincing chrome or glossy look on low-poly models
- Keep texture sizes at **1024×1024** for mobile performance; use **2048×2048** only for hero objects

---

## Double Sided

Enable **Double Sided** in the main panel (Export Settings) to render both sides of each polygon. This is equivalent to disabling backface culling in Range Engine. Useful for thin objects like leaves, cloth, or panels.

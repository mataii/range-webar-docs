# Troubleshooting

---

## Export errors

### "Output path not set!"

The **Output Path** field in the main panel is empty. Set it to a valid directory (e.g. `//webar_output`) before exporting.

### "No hay objetos marcados para exportar" (No objects marked for export)

All objects have **Export to WebAR** unchecked in their Object properties. Select each object, go to **Properties → Object → WebAR Object**, and enable **Export to WebAR**.

### "Export first!" when clicking Preview in Browser

The export has not been run yet, or the output folder is empty. Click **Export WebAR Scene** first.

---

## Scene validation warnings

The exporter runs a validation check before exporting and shows warnings if it finds potential issues. You can proceed anyway, but the issues may cause problems in the browser.

| Warning | Cause | Fix |
|---|---|---|
| `Object: sin mapa UV` | The mesh has no UV map | Add a UV unwrap in Edit Mode |
| `Object: sin materiales asignados` | Mesh has no material slot | Assign at least one material |
| `Material: sin imagen de textura` | Material has no image texture | Add an image texture to the material |
| `Image: no es potencia de 2` | Texture dimensions are not powers of 2 | Resize to 256/512/1024/2048 px |
| `Object: escala sin aplicar` | Object has unapplied scale | Select object → `Ctrl+A` → Scale |

---

## AR not working in browser

### "The page is not secure" / AR button missing

AR features require HTTPS. The local preview server uses plain HTTP.

**Fix:** Deploy to an HTTPS host (GitHub Pages, Netlify, etc.) to test full AR.

### Black screen or model not visible

- Check the browser console (F12) for JavaScript errors
- Make sure the GLB file exists in the output folder
- Check that texture files are present in the `textures/` folder

### Model is too large / too small

Adjust **Reference Size** in the AR Settings. Set it to the real-world size of the object in meters. For a 30 cm product, set `0.3`.

### Model floating above or sinking into the surface

The object's origin is not at the base. In Blender, select the object, go to **Object menu → Set Origin → Origin to Geometry**, then manually move the origin to the base of the model.

---

## Textures not appearing

### Textures missing in browser

- Make sure texture files are saved to disk (not packed inside the `.blend` file). **Image → Save As Image** for each texture.
- Non-browser-compatible formats (`.bmp`, `.tga`, `.exr`) are skipped. Convert to `.png` or `.jpg`.

### Wrong colors (too bright / too dark)

PBR textures (ORM, metalness, roughness) should be in **linear color space**, not sRGB. Color/diffuse textures should be sRGB. Check your texture export settings.

---

## Node Tree not compiling

### Behaviors not appearing in scene.json

- The node tree must contain a **Scene Output** node — without it the tree is ignored
- Nodes must be connected: an AR Object node must be linked to the animation or event node's **Target** input
- Check that the node tree is assigned to the scene in the **WebAR** panel

---

## Animations not playing

### GLB skeletal animations not playing

- Make sure **Animation Mode** is set to **Skeletal (Bones)**, not Static
- The animation action must be set on the armature object's active action or in NLA strips
- Check the `assets.animations` array in `scene.json` — the animation name must match exactly

### JS animations not visible

- Check that the object's **AR Behavior** is set to **Animated** in the Object panel
- In Static mode, the JS animation type must not be **None**
- Re-export after changing settings

---

## Performance issues on mobile

- Reduce texture sizes to 1024×1024 or smaller
- Reduce polygon count (aim for under 100k triangles total for smooth AR)
- Disable **Debug Overlay** in production
- Use **Static** animation mode instead of Object Animation
- Avoid too many simultaneous Blend-mode transparent objects

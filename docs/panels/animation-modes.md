# Animation Modes

The **Animation Mode** controls how movement is handled in the exported WebAR scene.

**Location:** WebAR panel → Animation → **Animation Mode**

---

## Static (8thWall Style) — Recommended

The GLB file is exported as a **snapshot at the current frame** — no keyframe data included. All motion is driven by **JavaScript at runtime** in the browser.

This approach mirrors the 8thWall workflow: a clean, lightweight model file plus a separate animation layer.

**Advantages:**
- Smallest file size
- Fastest load time
- Per-object JS animations configured directly in Blender (Rotate, Float, Pulse, Spin)
- No issues with armature or bone export compatibility

**When to use:** most product visualizations, decorative animations, interactive objects.

**JS Animation types available per object:**

| Type | Description |
|---|---|
| None | Object stays still |
| Rotate Y | Continuous rotation around the Y (vertical) axis |
| Rotate X | Continuous rotation around the X axis |
| Rotate Z | Continuous rotation around the Z axis |
| Float | Gentle up-and-down floating movement |
| Pulse Scale | Rhythmic scale in/out |
| Spin Fast | Fast spin — useful for loading indicators or highlights |

Speed for all types is set per-object in the **WebAR Object** panel.

---

## Skeletal (Bones)

Exports the armature with skinning weights and animation clips baked from the NLA or active action.

**Use when:** your model is a rigged character with walk cycles, gestures, or other bone-driven animations.

**Limitations:**
- Larger file size
- Browser compatibility depends on the rig complexity
- Object-level rotation animations (not bone-driven) may not export correctly — use Static mode for those

---

## Object Animation

Exports baked object-level keyframes (position, rotation, scale) by force-sampling the IPO curves.

**Use when:** you have non-bone animations — e.g. a mechanical assembly where parts move independently.

!!! warning "Heavy — not recommended"
    Object animation produces large files and can cause performance issues on mobile. Consider baking to a lower frame rate or replacing with JS animations (Static mode) where possible.

---

## Choosing the right mode

```
Has rigged character animations?
  └─ Yes → Skeletal (Bones)
  └─ No → Has complex mechanical keyframe animations?
              └─ Yes → Object Animation (use sparingly)
              └─ No → Static + JS animations (recommended)
```

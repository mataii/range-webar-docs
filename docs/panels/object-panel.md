# Object Panel

**Location:** Properties editor → Object tab (orange square) → **WebAR Object** section

Each object in the scene has its own WebAR settings. Select an object in the 3D View, then open the Properties editor to configure it.

---

## Export to WebAR

| Property | Type | Default |
|---|---|---|
| **Export to WebAR** | Bool | ✓ |

When unchecked, this object is completely ignored by the exporter — it will not appear in the GLB or in `scene.json`.

Supported object types: **Mesh**, **Armature**, **Empty**, **Light**.

---

## AR Behavior

| Value | Description |
|---|---|
| **Static** | Object does not move or respond to interaction. |
| **Animated** | Object has a continuous JS-driven animation (Rotate, Float, Pulse, Spin). Only available in **Static** animation mode. |
| **Interactive** | Object responds to tap/click events. |

---

## Animated behavior

When **AR Behavior** is set to **Animated**, two extra properties appear:

| Property | Type | Default | Description |
|---|---|---|---|
| **JS Animation** | Enum | None | The continuous animation type applied to this object. |
| **Speed** | Float 0–10 | `1.0` | Speed multiplier for the animation. `1.0` = default speed. |

**JS Animation types:**

| Type | Effect |
|---|---|
| None | No animation |
| Rotate Y | Spins around the vertical axis |
| Rotate X | Tilts forward/backward |
| Rotate Z | Rolls left/right |
| Float | Bobs gently up and down |
| Pulse Scale | Rhythmically grows and shrinks |
| Spin Fast | Fast spin (useful for spotlights or loading indicators) |

---

## Interactive behavior

When **AR Behavior** is set to **Interactive**, a custom JavaScript field appears:

| Property | Type | Description |
|---|---|---|
| **On Click JS** | String | JavaScript expression executed when the user taps this object. Example: `window.open('https://mysite.com')` |

!!! tip "Simple actions"
    For common actions like toggling visibility or playing an animation, use the **Node Tree** instead — it's easier and doesn't require writing JavaScript.

---

## Metadata

| Property | Type | Default |
|---|---|---|
| **Metadata JSON** | String | `{}` |

A free-form JSON string attached to this object in `scene.json`. Useful for integrating with external systems — for example, a product ID for an e-commerce backend.

```json
{"product_id": "SKU-001", "category": "electronics"}
```

---

## Material settings

The material section appears only for **Mesh** objects when **Export Materials** is enabled in the main panel.

The available fields depend on the **Material Mode** set in the main panel. See:

- [Classic Materials (Phong)](../materials/classic.md)
- [PBR Materials](../materials/pbr.md)

---

## Hotspot settings

Empty objects can be converted into **interactive AR annotations**. See [Hotspots](hotspots.md).

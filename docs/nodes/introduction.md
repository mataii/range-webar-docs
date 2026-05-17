# Node Tree — Introduction

The **WebAR Node Tree** is a visual editor for wiring animations and interaction events without writing JavaScript. It works similarly to Blender's shader or compositor nodes.

---

## Opening the Node Tree

1. In the **WebAR** sidebar panel, find the **Node Tree** property and click **New** to create a node tree, or select an existing one.
2. Switch any editor to the **Node Editor** and set the node tree type to **WebAR Node Tree** (the dropdown at the top left of the Node Editor).
3. Add nodes with `Shift+A` → **WebAR** menu.

!!! tip "Auto Regenerate"
    Enable **Auto Regenerate** in the WebAR panel to get a "Changes detected!" warning whenever you modify the node tree, reminding you to re-export.

---

## How it works

The node tree is **compiled** at export time. The exporter reads all connected nodes and converts them into the `components` and `events` arrays in `scene.json`. These are then executed by the runtime JavaScript in the browser.

Nodes that are not connected to a valid chain are ignored.

---

## Node types

| Category | Nodes |
|---|---|
| **Scene** | [Scene Output](object-nodes.md#scene-output) |
| **Objects** | [AR Object](object-nodes.md#ar-object) |
| **Animations** | [JS Animation](animation-nodes.md#js-animation), [Pulse](animation-nodes.md#pulse), [Spin](animation-nodes.md#spin) |
| **Events** | [Tap](event-nodes.md#tap), [Update](event-nodes.md#update), [Timer](event-nodes.md#timer) |
| **Experimental** | AR Light (WIP), AR Animation (WIP) |

---

## Basic workflow

A typical node setup connects:

```
AR Object → Animation node (Pulse / Spin / JS Animation)
AR Object → Event node (Tap / Timer)
```

The **Scene Output** node acts as the export root. Any node tree without a Scene Output node is ignored during export.

---

## Compiled output

The node tree produces two arrays in `scene.json`:

- **`components[]`** — continuous per-frame behaviors (Pulse, Spin, JS Animation)
- **`events[]`** — triggered behaviors (Tap, Update, Timer)

See the [scene.json Schema](../reference/scene-schema.md) for the full structure.

---

## Deprecated nodes

| Node | Status | Use instead |
|---|---|---|
| AR Interaction | Deprecated | **Tap** node |

The AR Interaction node is still available in the node menu but does not export any data.

# Event Nodes

Event nodes trigger **actions on objects** when a specific event occurs. They compile into the `events[]` array in `scene.json`.

All event nodes require an **AR Object** node connected to their **Target** input.

---

## Available actions

All event nodes share the same set of actions:

| Action | Description |
|---|---|
| **Toggle Visibility** | Show/hide the object each time the event fires |
| **Play Animation** | Play a named animation clip embedded in the GLB |
| **Set Rotation Y** | Set the object's Y rotation to a specific value (radians) |
| **Set Scale** | Set the object's uniform scale to a specific value |

---

## Tap

**Node ID:** `WEBARNodeTap`

Fires when the user taps or clicks on the target object.

**Requires:** Enable Tap must be on in the main panel (Interactions → Enable Tap).

**Inputs:**

| Socket | Type | Description |
|---|---|---|
| Target | Object | The object that receives tap events |

**Properties:**

| Property | Description |
|---|---|
| **Action** | What happens when the object is tapped |
| **Animation** | Animation clip name (Play Animation only) |
| **Rotation Y** | Target rotation value in radians (Set Rotation Y only) |
| **Scale** | Target scale value (Set Scale only) |

**Compiled output:**
```json
{
  "event": "tap",
  "target": "Button",
  "actions": [
    { "type": "toggle_visibility" }
  ]
}
```

---

## Update

**Node ID:** `WEBARNodeUpdate`

Fires every frame (the render loop update event). Use this for one-time setup actions or frame-by-frame state changes.

!!! warning "Use sparingly"
    Update fires every frame (~60 times per second). Expensive actions here can hurt performance. For continuous animations, use [Animation Nodes](animation-nodes.md) instead.

**Properties:** same action set as Tap.

**Compiled output:**
```json
{
  "event": "update",
  "target": "MyObject",
  "actions": [
    { "type": "play_animation", "name": "Idle" }
  ]
}
```

---

## Timer

**Node ID:** `WEBARNodeTimer`

Fires at a fixed interval, repeatedly.

**Inputs:**

| Socket | Type | Description |
|---|---|---|
| Target | Object | The object the action applies to |

**Properties:**

| Property | Range | Description |
|---|---|---|
| **Interval (s)** | 0.1–60 | Time in seconds between each trigger |
| **Action** | — | Same action set as Tap |

**Example use case:** Reset an object's rotation to zero every 3 seconds.

**Compiled output:**
```json
{
  "event": "timer",
  "target": "Wheel",
  "interval": 3.0,
  "actions": [
    { "type": "set_rotation", "value": 0.0 }
  ]
}
```

---

## Common patterns

**Tap to show/hide an object:**
```
AR Object (Button) ──► Tap → Toggle Visibility → AR Object (Panel)
```

**Auto-play animation on load:**
```
AR Object (Character) ──► Update → Play Animation → "Walk"
```

**Periodically reset rotation:**
```
AR Object (Spinner) ──► Timer (5s) → Set Rotation Y → 0
```

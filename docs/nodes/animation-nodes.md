# Animation Nodes

Animation nodes apply **continuous, per-frame behaviors** to objects. They compile into the `components[]` array in `scene.json`.

All animation nodes require an **AR Object** node connected to their **Target** input.

---

## JS Animation

**Node ID:** `WEBARNodeJSAnimation`

Applies a continuous JavaScript-driven animation to the target object.

**Inputs:**

| Socket | Type | Description |
|---|---|---|
| Target | Object | The AR Object to animate |

**Properties:**

| Property | Values | Description |
|---|---|---|
| **Type** | Rotate Y / Float | The animation type |
| **Speed** | 0–10 | Speed multiplier |

**Compiled output:**
```json
{
  "object": "MyObject",
  "type": "ROTATE",
  "speed": 1.5
}
```

---

## Pulse

**Node ID:** `WEBARNodePulse`

Makes the object rhythmically scale in and out — a breathing or heartbeat effect.

**Inputs:**

| Socket | Type | Description |
|---|---|---|
| Target | Object | The AR Object to pulse |

**Properties:**

| Property | Range | Description |
|---|---|---|
| **Speed** | 0–10 | Pulses per second |
| **Amplitude** | 0–5 | How much the scale changes. `0.1` = subtle, `0.5` = dramatic |

**Compiled output:**
```json
{
  "object": "MyObject",
  "type": "pulse",
  "speed": 1.0,
  "amplitude": 0.25
}
```

---

## Spin

**Node ID:** `WEBARNodeSpin`

Rotates the object continuously around a chosen axis.

**Inputs:**

| Socket | Type | Description |
|---|---|---|
| Target | Object | The AR Object to spin |

**Properties:**

| Property | Values | Description |
|---|---|---|
| **Axis** | X / Y / Z | Rotation axis |
| **Speed** | 0–20 | Rotation speed multiplier |

**Compiled output:**
```json
{
  "object": "MyObject",
  "type": "spin",
  "axis": [0, 1, 0],
  "speed": 2.0
}
```

Axis values: X = `[1,0,0]`, Y = `[0,1,0]`, Z = `[0,0,1]`.

---

## Combining animations

You can apply multiple animation nodes to the same object by connecting multiple nodes to the same AR Object output. For example: Pulse + Spin gives a spinning, pulsing object.

```
AR Object ──► Spin (Y, speed 1.0)
           └─► Pulse (speed 2.0, amplitude 0.1)
```

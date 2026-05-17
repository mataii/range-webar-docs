# Object Nodes

---

## AR Object

**Node ID:** `WEBARNodeObject`

Represents a Blender object in the node tree. Other nodes connect to this one to apply behaviors.

**Inputs:**

| Socket | Type | Description |
|---|---|---|
| Scale | Float | Scale multiplier (currently informational — does not affect runtime) |

**Outputs:**

| Socket | Type | Description |
|---|---|---|
| Object | Object | Passes the object reference to connected animation or event nodes |

**Properties:**

| Property | Description |
|---|---|
| **Object** | The Blender object this node represents. Pick it from the dropdown. |
| **Behavior** | Static / Animated / Interactive — mirrors the per-object setting in the Object panel |

!!! note
    The AR Object node is the **source** in every node chain. Animation and event nodes connect their inputs to the Object output of an AR Object node.

---

## Scene Output

**Node ID:** `WEBARNodeSceneOutput`

The export root marker. Every node tree must contain exactly one Scene Output node or the tree will not be compiled.

The node has no inputs or outputs — it simply signals to the exporter that this node tree should be processed.

**Usage:** Add it once to any node tree you want to compile. Its position doesn't matter.

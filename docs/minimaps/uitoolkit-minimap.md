# UI Toolkit Minimap

The `Minimap UIToolkit` prefab provides a minimap built on Unity's UI Toolkit system. 
---

## Prefab Structure

```
Minimap UIToolkit
├── Minimap Camera          ← orthographic camera, renders to Minimap RT
├── Camera Frustum Box      ← LineRenderer showing the main camera's view area
├── Minimap Document        ← UIDocument displaying Minimap RT
└── EventSystem
```

---

## Setup

### 1. Add the prefab

Drag the `Minimap UIToolkit` prefab into your scene.

### 2. Configure Rendering Layers

Assign the **Minimap Camera** and the **Camera Frustum Box** `LineRenderer` to a dedicated rendering layer (e.g. `Minimap`). Remove that layer from the main game camera's **Culling Mask** so the frustum box is only visible on the minimap.

### 3. Wire up Minimap Camera

On the **Minimap Camera** GameObject:

| Field | Value |
|---|---|
| **Target Texture** | The `Minimap RT` Render Texture asset |
| **Culling Mask** | The layers you want visible on the minimap |
| **Projection** | Orthographic |

Position and scale the camera's orthographic size to cover your map.

### 4. Wire up MinimapFrustumBox

On the **Camera Frustum Box** GameObject, the `MinimapFrustumBox` component needs:

| Field | Description |
|---|---|
| **Camera Frustum Box Renderer** | The `LineRenderer` on this GameObject |
| **Camera** | Your main game camera |
| **Ground Layer Mask** | Layer(s) used as the ground for frustum ray projection |
| **Camera View Display Vertical Offset** | Lifts the line slightly above the ground to prevent z-fighting |
| **Max Distance Fallback** | Fallback projection distance if the ground raycast misses |
| **Line Color / Width** | Visual style of the frustum outline |

### 5. Wire up MinimapCameraBinderUIToolkit

The `MinimapCameraBinderUIToolkit` component is on the **Minimap Document** GameObject. Set:

| Field | Value |
|---|---|
| **Bound Camera** | Your game camera controller |
| **Minimap Element Name** | Name of the child `VisualElement` to treat as the clickable minimap surface. Leave empty to use the root element |

### 6. Wire up UIToolkitCameraInputBlocker

The `UIToolkitCameraInputBlocker` component is also on the **Minimap Document** GameObject. Set:

| Field | Value |
|---|---|
| **Active Cursor State** | The `ActiveCursorStateSO` used by your camera controller |
| **Default Cursor State SO** | The cursor state to restore when the pointer leaves the minimap |
| **Over UI Cursor State** | Your `OverUICursorState` asset |

---

## Related

- [UGUI Minimap](ugui-minimap.md)
- [Cursor Over UI Detection](../advanced/cursor-over-ui-state.md)
- [Camera Bounds](../advanced/camera-bounds.md)

# UGUI Minimap

The `Minimap UGUI` prefab provides a minimap built with Unity's uGUI system.

---

## Prefab Structure

```
Minimap UGUI
├── Minimap Camera          ← orthographic camera, renders to Minimap RT
├── Camera Frustum Box      ← LineRenderer showing the main camera's view area
└── UI Canvas
│   └── Minimap Image       ← UGUI Image displaying Minimap RT
└── EventSystem
```

---

## Setup

1. Drag the `Minimap UGUI` prefab into your scene.
2. Adjust the **Minimap Camera's** orthographic size and distance to fully cover the game map.
3. Assign the **Minimap Camera** and the **Camera Frustum Box** `LineRenderer` to a dedicated rendering layer (e.g. `Minimap`). This is already done in the prefab, but you will be missing the layers in your project if you just imported this, or they might have overwritten yoru own layers, so double check to make sure.
4. Remove the minimap layer from the main game camera's **Culling Mask** so the frustum box is invisible in the main view.
5. Set the **Bound Camera** on `MinimapCameraBinderUGUI` to your game camera controller.
6. Set the **Camera** on `MinimapFrustumBox` to your main game camera.

---

## Configuration

### Minimap Camera


| Field | Value |
|---|---|
| **Target Texture** | The `Minimap RT` Render Texture asset |
| **Culling Mask** | The layers you want visible on the minimap |
| **Projection** | Orthographic |

You can adjust the Render Texture resolution to get the fidelity you need - larger textures give a sharper minimap but use more memory.

### MinimapFrustumBox

| Field | Description |
|---|---|
| **Camera Frustum Box Renderer** | The `LineRenderer` on this GameObject |
| **Camera** | Your main game camera |
| **Ground Layer Mask** | Layer(s) used as the ground for frustum ray projection. Leave empty if you don't need the box to follow terrain elevation |
| **Camera View Display Vertical Offset** | Lifts the line slightly above the ground to prevent clipping |
| **Max Distance Fallback** | Fallback projection distance if the ground raycast misses. Increase this for cameras that pitch steeply or use free look |
| **Line Color / Width** | Increase width to avoid aliasing if the rendered line appears too thin |

### MinimapCameraBinderUGUI

| Field | Description |
|---|---|
| **Minimap Rect** | The `RectTransform` of the Minimap Image |
| **Bound Camera** | Your game camera controller |
| **Input Button** | Mouse button used to interact with the minimap (default: Left) |

### UGUICameraInputBlocker

| Field | Description |
|---|---|
| **Active Cursor State** | The `ActiveCursorStateSO` used by your camera controller |
| **Default Cursor State SO** | The cursor state to restore when the pointer leaves the minimap |
| **Over UI Cursor State** | Your `OverUICursorState` asset |

Ensure **Raycast Target** is enabled on the `Image` component so pointer events are received.

---

## Related

- [UI Toolkit Minimap](uitoolkit-minimap.md)
- [Cursor Over UI Detection](../advanced/cursor-over-ui-state.md)
- [Camera Bounds](../advanced/camera-bounds.md)

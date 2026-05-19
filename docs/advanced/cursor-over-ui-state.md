# Cursor Over UI Detection

`OverUICursorState` is a special cursor state that signals to the camera controller that the cursor is currently over a UI element. When the active cursor state is an `OverUICursorState`, all camera input processing is skipped for that frame - pan, zoom, rotate, screen-edge scroll, everything stops.

This makes it possible to place interactive UI elements (like a minimap or HUD panel) on top of the game view without camera inputs leaking through. For example, dragging on the minimap won't also pan the camera.

---

## How It Works

`OverUICursorState` extends `SingleCursorStateSO`, so it behaves like a regular cursor state but is identifiable by type. The camera controllers use a type check internally:

```csharp
if (m_ignoreInput || m_activeCursorState.CurrentState is OverUICursorState)
{
    return;
}
```

The state is set and cleared by the `UGUICameraInputBlocker` component placed on the UGUI element. When the pointer enters the element, it sets the `OverUICursorState` on the shared `ActiveCursorStateSO`. When the pointer leaves, it restores the default cursor state.

---

## Setup

### 1. Create the asset

Right-click in the Project window and choose:

**Create > Parallel Cascades > Camera Controllers > Over UI Cursor State SO**

Optionally assign a cursor texture - you might want a normal arrow cursor here to override any custom camera cursor that was active just before the pointer moved over the UI. Leaving the texture field empty falls back to the system default cursor.

### 2. Add an input blocker component to the UI element

Two components are provided depending on your UI system:

| Component | Use with |
|---|---|
| `UGUICameraInputBlocker` | UGUI (`Canvas`-based) elements |
| `UIToolkitCameraInputBlocker` | UI Toolkit (`UIDocument`-based) elements |

Add the appropriate component to the root of the UI element that should block camera input (for example, the minimap image or panel).

Wire up the three fields in the inspector:

| Field | Value |
|---|---|
| **Active Cursor State** | The shared `ActiveCursorStateSO` asset used by your camera controller |
| **Default Cursor State SO** | The `CursorStateSO` to restore when the pointer leaves the element (typically your default `SingleCursorStateSO`) |
| **Over UI Cursor State** | The `OverUICursorState` asset created in step 1 |

For UGUI elements, the element must be able to receive pointer events. If the element is an `Image`, ensure **Raycast Target** is enabled on it.

---

## Difference from CameraControlStateSO

[`CameraControlStateSO`](ui-integration.md) fully pauses the camera - position, rotation, and zoom all freeze. Use it when the camera should be completely inert, such as during a pause menu.

`OverUICursorState` only stops gathering new input. The camera still applies its current movement state each frame, so any in-progress pan or rotation interpolates smoothly to a stop rather than cutting off abruptly. This also means you can still move the camera programmatically while the cursor is over UI - for example, binding the camera position to a minimap click without fighting the input system.

---

## Related

- [Cursor System](cursor-system.md)
- [UI Integration](ui-integration.md)
- [Minimaps](../minimaps/index.md)

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

### 2. Add UGUICameraInputBlocker to the UI element

Add the `UGUICameraInputBlocker` component to the root of the UGUI element that should block camera input (for example, the minimap image).

Wire up the three fields in the inspector:

| Field | Value |
|---|---|
| **Active Cursor State** | The shared `ActiveCursorStateSO` asset used by your camera controller |
| **Default Cursor State SO** | The `CursorStateSO` to restore when the pointer leaves the element (typically your default `SingleCursorStateSO`) |
| **Over UI Cursor State** | The `OverUICursorState` asset created in step 1 |

The UGUI element must be able to receive pointer events. If the element is an `Image`, ensure **Raycast Target** is enabled on it.

---

## Cursor Texture

Because `OverUICursorState` extends `SingleCursorStateSO` you can assign any cursor texture to it, or leave it empty to keep the system default. A few common choices:

- **Empty (system default)** - the OS arrow cursor appears while over UI.
- **Same texture as your default camera cursor** - no visible change when entering the UI area.
- **A distinct UI cursor** - a hand pointer or similar, to give extra visual feedback that camera controls are suspended.

---

## Difference from CameraControlStateSO

`OverUICursorState` and [`CameraControlStateSO`](ui-integration.md) both pause camera input, but they are designed for different scenarios:

| | `OverUICursorState` + `UGUICameraInputBlocker` | `CameraControlStateSO` |
|---|---|---|
| **Trigger** | Pointer hovering over a specific UGUI element | Explicit call from game logic (menu opened, scene transition, etc.) |
| **Scope** | Automatic, hover-based, per-element | Manual, applies globally |
| **Typical use** | Minimap, HUD panels that overlap the game view | Pause menus, inventory screens, cutscenes |

---

## Related

- [Cursor System](cursor-system.md)
- [UI Integration](ui-integration.md)

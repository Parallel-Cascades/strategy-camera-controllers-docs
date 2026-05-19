# Cursor System

The Cursor System lets you swap the cursor texture as the camera changes state - for example, showing a pan cursor when the player starts panning, or an edge-scroll arrow when the cursor reaches the screen edge.

All three controllers support the cursor system. The **Simulation Camera** demonstrates the widest range of cursor state changes and is the best reference for a fully configured setup.

If you don't want to use this, simply don't assign the cursors in the camera inspector.

---

## Architecture

The cursor system is built on a **ScriptableObject** architecture. Each cursor state is represented by a `CursorStateSO` ScriptableObject, which holds the cursor texture and other relevant data. The active cursor is set via a `ActiveCursorStateSO` singleton scriptable object.

---

## Creating Cursor Assets

Right-click in the Project window and choose:

```
Create > Parallel Cascades > Camera Controllers > ...
```

### Single Cursor State

`SingleCursorStateSO` is the default cursor state. It displays one fixed texture. Leaving the texture field empty will fall back to the system default cursor.

Create via: **Create > Parallel Cascades > Camera Controllers > Single Cursor State SO**

### Directional Cursor State

`DirectionalCursorStateSO` (created as **Edge Scroll Cursor State SO**) holds up to eight cursor textures - one for each cardinal and diagonal direction (S, N, E, W, SE, SW, NE, NW). The camera controller switches between them automatically as the cursor moves toward different screen edges during edge scrolling.

Create via: **Create > Parallel Cascades > Camera Controllers > Edge Scroll Cursor State SO**

### Hidden Cursor State

`HiddenCursorStateSO` hides the cursor and confines it to the window. When the camera exits this state the cursor is made visible again and warped back to the position it was at when the state was entered. This is used during mouse-drag panning, where the cursor should not be visible or able to leave the window.

Create via: **Create > Parallel Cascades > Camera Controllers > Hidden Cursor State SO**

### Over UI Cursor State

`OverUICursorState` is a special state that signals to the camera controller that the cursor is over a UI element, suspending all camera input for that frame. It extends `SingleCursorStateSO` so a cursor texture can optionally be assigned. See [Cursor Over UI Detection](cursor-over-ui-state.md) for full setup instructions.

Create via: **Create > Parallel Cascades > Camera Controllers > Over UI Cursor State SO**

---

## Cursor Color Variable

`CursorColorVariable` is a global ScriptableObject singleton that holds a single `Color` value. Any cursor state that references it will have its texture tinted by that color at runtime. This lets you change the tint of all cursors at once from a single asset - useful for theming or accessibility options.

Create via: **Create > Parallel Cascades > Camera Controllers > Cursor Color Variable**

Assign the same `CursorColorVariable` asset to every cursor state that should be affected by the global tint.

---

## Cursor Texture Guidelines

This uses Unity's [SetCursor()](https://docs.unity3d.com/6000.4/Documentation/ScriptReference/Cursor.SetCursor.html) hardware cursor API.

Cursor textures have to be 32x32 pixels, mipmaps disable, read/write enabled, alphaIsTransparency enabled and texture format RGBA32

In `SingleCursorStateSO` you can assign any cursor texture to it, or leave it empty to keep the system default.

---

## Related

- [Cursor Over UI Detection](cursor-over-ui-state.md)
- [Simulation Camera](../cameras/simulation-camera.md)
- [Quick Setup](../get-started.md)

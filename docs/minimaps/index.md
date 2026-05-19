# Minimaps

Two minimap prefabs are included - for uGUI or UIToolkit. You can drag and drop these into your scenes that use Strategy Camera Controllers, or use them as a template to build your own interactable minimaps.

| Prefab | UI System |
|---|---|
| `Minimap UGUI` | UGUI (`Canvas`-based) |
| `Minimap UIToolkit` | UI Toolkit (`UIDocument`-based) |

---

## How It Works

### Render Texture capture

An orthographic camera (`Minimap Camera`) sits above the scene and renders the map into a **Render Texture** (`Minimap RT`). That texture is then assigned to a UI element, giving you a live top-down view of the world.

You can adjust the minimap camera size and position and the render texture's resolution to customize the minimap look.

### Culling masks

Culling masks using layers let you control exactly what each camera sees. Typically:

Minimap only elements include the camera view frustum box, any building or unit textures or icons that only appear in the minimap.

- The **main game camera** renders everything except the minimap-only layer.
- The **minimap camera** renders the map geometry and any minimap-only overlays. It can omit certain objects like units or buildings that appear as textures instead.

This is how the camera frustum indicator stays visible on the minimap but is invisible in the main view.

For more information on culling masks, go to </br><https://docs.unity3d.com/6000.4/Documentation/ScriptReference/Camera-cullingMask.html>

### Camera frustum indicator

The `MinimapFrustumBox` component drives a `LineRenderer` that traces the four corners of the main camera's view frustum onto the ground plane each frame. Because the `LineRenderer` is on a minimap-only rendering layer, it appears on the minimap but not in the main scene view.

### UI display

The Render Texture is displayed inside a UI element - a UGUI `Image` or a UI Toolkit `VisualElement` with a background image. Check out the prefabs to see how this is set up.

### Camera interaction

Two components work together to let players click and drag the minimap to move the camera:

- **`MinimapCameraBinderUGUI` / `MinimapCameraBinderUIToolkit`** - converts a pointer position on the minimap element to a world position and calls `SetPanPosition` on the bound camera.
- **`UGUICameraInputBlocker` / `UIToolkitCameraInputBlocker`** - sets the `OverUICursorState` while the pointer is over the minimap, so the regular camera input (pan, rotate, zoom) is suspended. Because the camera still applies its current movement state, any in-progress motion completes smoothly rather than cutting off abruptly.

---

## Related

- [UGUI Minimap](ugui-minimap.md)
- [UI Toolkit Minimap](uitoolkit-minimap.md)
- [Cursor Over UI Detection](../advanced/cursor-over-ui-state.md)
- [Camera Bounds](../advanced/camera-bounds.md)

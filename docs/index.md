# Strategy Camera Controllers

Strategy Camera Controllers is a collection of Unity camera controllers built on Unity's Input System. Designed to be modular and extensible, these controllers are ready to drop into any project for rapid prototyping or to serve as a foundation for fully custom camera systems.

[Quick Setup](./get-started.md){ .md-button .md-button--primary } [Asset Store](https://assetstore.unity.com/packages/templates/systems/strategy-camera-controllers-370822){ .md-button .md-button--secondary }

---

## Camera Controllers

### Classic RTS Camera Controller


A fixed-angle overhead camera inspired by classic Blizzard-era RTS games. Maintains a consistent pitch that tilts downward as you zoom in for a more grounded feel at close range. Camera yaw can be temporarily rotated and snaps back to the default orientation when released.

[Learn More](./cameras/classic-rts-camera.md){ .md-button }

---

### Simulation Camera Controller

The most flexible of the three controllers. Supports full yaw, pitch, and pan control via both mouse drag and keyboard, including screen-edge panning. Automatic pan speed scaling based on zoom level keeps movement feeling consistent at any altitude.

[Learn More](./cameras/simulation-camera.md){ .md-button }

---

### Tactical War Camera Controller

A ground-level tactical camera inspired by the Total War series. Zooms by raising and lowering the camera's altitude rather than adjusting field of view. Free-look pitch and yaw is available via a held modifier key, making it ideal for surveying troops and terrain up close.

[Learn More](./cameras/tactical-war-camera.md){ .md-button }

---

## Advanced Features

| Feature | Description |
|---|---|
| [Camera Bounds](./advanced/camera-bounds.md) | Constrain camera movement to a defined play area |
| [Automatic Elevation Adjustment](./advanced/auto-elevation.md) | Lift the camera above terrain and obstacles automatically |
| [Cursor System](./advanced/cursor-system.md) | ScriptableObject-based cursor swapping as the camera changes state |
| [UI Pause Integration](./advanced/ui-integration.md) | Pause camera input from UI Toolkit or uGUI |
| [Input Remapping](./advanced/input-remapping.md) | Remap all controls via the Input System Actions editor |

---

## Support

If you encounter any issues or have questions, please reach out at [support@parallelcascades.com](mailto:support@parallelcascades.com) or through the [contact form](https://parallelcascades.com) on the website.

Consider leaving a review on the Asset Store!

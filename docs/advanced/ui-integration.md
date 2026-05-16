# UI Integration

Camera control can be paused when the player opens a menu or interacts with UI. This is handled through a **Scriptable Object** architecture, where a shared `CameraControlStateSO` asset acts as the single source of truth for whether camera control is currently active.

Any object that needs to enable or disable camera control - a menu, a pause screen, an inventory panel - holds a reference to the same `CameraControlStateSO` asset and calls `SetControlState()` on it. The camera controller itself also holds a reference to that same asset and subscribes to its `OnValueChanged` event to react immediately when the state changes.

---

## CameraControlStateSO

| Member | Description |
|---|---|
| **SetControlState(bool)** | Enables or disables camera control and fires `OnValueChanged` |
| **EnableCameraControl()** | Convenience method — calls `SetControlState(true)` |
| **DisableCameraControl()** | Convenience method — calls `SetControlState(false)` |
| **OnValueChanged** | Event fired whenever the state changes, passing the new `bool` value |

---

## Setup

1. Create a `CameraControlStateSO` asset via **Create > Parallel Cascades > Camera Controllers > Camera Control State SO**.
2. Assign the asset to the **Camera Control State** field on your camera controller component.
3. Assign the same asset to any UI component that should pause or resume camera control.
4. Call `EnableCameraControl()` or `DisableCameraControl()` on the asset from your UI logic (e.g. when a menu opens or closes).

---

## Demo Scenes

Two sample scenes demonstrate this pattern in practice, one for each Unity UI system:

| Scene | UI System |
|---|---|
| `Assets/ParallelCascades/StrategyCameraControllers/Samples/Unity UI Interface Demo.unity` | uGUI (Unity UI) |
| `Assets/ParallelCascades/StrategyCameraControllers/Samples/UIToolkit Menu Interface Demo.unity` | UI Toolkit |

Each scene contains a simple menu that disables camera control while it is open and re-enables it when it is closed. Open either scene and inspect the menu and camera controller objects to see the shared `CameraControlStateSO` asset wired up on both sides.

---

## Related

- [Quick Setup](../get-started.md)

# Quick Setup

## Requirements

- Unity Input System package (com.unity.inputsystem)


## Adding a Camera to Your Scene

The fastest way to get a camera into your scene is to use the ready-made **prefabs** found in:

```
Assets/ParallelCascades/StrategyCameraControllers/Prefabs/
```

Drag one of the camera prefabs into your scene Hierarchy.

!!! warning "Remove duplicate cameras"
    Delete or disable any existing **Main Camera** in your scene before adding a controller prefab to avoid conflicts.

### Available Prefabs

| Prefab | Description |
|---|---|
| `ClassicFantasyRTSCameraController` | Classic RTS camera tuned to feel like Warcraft 3 |
| `ClassicSciFiRTSCameraController` | Classic RTS camera tuned to feel like StarCraft 2 |
| `SimulationCameraController` | Full freedom(pitch+yaw+zoom) simulation camera |
| `TacticalWarCameraController` | Tactical camera with free-look in the vein of Total War games |

## Camera Rig Setup

The **Classic RTS** and **Simulation** cameras use a **rig** - the camera is a child of a rig GameObject that moves through the scene and is controlled by the controller script.

The **Tactical War** camera has no rig and controls the camera transform directly.

## Exploring the Sample Scenes

Sample scenes for all three controllers are included and are the best place to see how each camera is configured:

```
Assets/ParallelCascades/StrategyCameraControllers/Samples/
```

Open a sample scene and press Play to immediately try out the controls.

## Next Steps

- [Classic RTS Camera](./cameras/classic-rts-camera.md)
- [Simulation Camera](./cameras/simulation-camera.md)
- [Tactical War Camera](./cameras/tactical-war-camera.md)
- [Remapping Keybindings](./advanced/input-remapping.md)
- [Advanced Features](./advanced/index.md) - camera bounds, terrain elevation, cursor system, and more

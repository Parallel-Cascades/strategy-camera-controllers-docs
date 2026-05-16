# Automatic Elevation Adjustment

Automatic Elevation Adjustment lifts the camera upward when the terrain or an obstacle would otherwise intersect with it. This ensures the camera never clips through the ground or through buildings and other geometry.

All three controllers support this feature, and it is enabled in all sample scenes.

---

## How It Works

The controller casts a ray downward from the camera's current position. If the ray hits any collider within in the specified ground and obstacles layers within the configured minimum clearance distance, the camera's Y position is raised to maintain the desired clearance above the hit point.

The reason we differentiate between terrain and obstacles is that the camera should always lift above terrain, wherease it only lifts above
obstacles if they are within the specified min clearance range. So that you don't raise the camera unnecessarily if it's already zoomed out above the 
rooftops of buildings, for example.
---

## Setup

Automatic elevation requires two **Layer Masks** to be assigned on the controller component:

| Property | Description |
|---|---|
| **Enable Auto Elevation** | Toggle to enable or disable this feature |
| **Ground Layer Mask** | Layers to always lift above (e.g. your terrain layer) |
| **Obstacle Layer Mask** | Layers treated as obstacles the camera should lift above (e.g. buildings) |
| **Obstacle Clearance Distance** | Minimum distance to maintain between the camera and any obstacles below it |

!!! warning "Layer assignment"
    Make sure your terrain and obstacle GameObjects are assigned to the correct layers, and that those layers are included in the respective masks. The camera will not react to geometry on layers not included in the masks.

---

## Sample Scene Reference

All sample scenes demonstrate elevation. Open any sample scene and inspect the camera controller to see a working reference setup.

---

## Related

- [Camera Bounds](./camera-bounds.md)
- [Quick Setup](../get-started.md)

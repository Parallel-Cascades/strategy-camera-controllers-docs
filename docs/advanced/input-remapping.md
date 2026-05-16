# Input Remapping

All keybindings for every camera controller are defined as **Input Actions** and can be fully remapped through the Unity Input System editor without writing any code.

---

## Locating the InputActions Assets

Each controller has its own `InputActions` asset found in:

```
Assets/ParallelCascades/StrategyCameraControllers/Runtime/Input/
```

---

## Editing Bindings

Double-click an `InputActions` asset to open the **Input Actions editor**.

Here you can select existing bindings and add alternative keys or change the existing ones.

For a full walkthrough of the Input Actions editor, see the Unity documentation:

[Input Actions Editor — Unity Documentation](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.19/manual/ActionsEditor.html){ .md-button }

---

## Composite Bindings (Modifier Keys)

The **Tactical War Camera**'s free-look action uses a **one-modifier composite binding** (`Alt + Scroll Click`). Composite bindings combine multiple inputs into a single action.

To change the modifier key:

1. Expand the composite binding in the editor.
2. Click the **Modifier** part of the composite.
3. Click the binding field and press the new key.

For details on composite bindings, see:

[Action Bindings — Unity Documentation](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.19/manual/ActionBindings.html#one-modifier){ .md-button }

---

## Runtime Remapping

If you need to support player-configurable keybindings at runtime, the Unity Input System provides a **rebinding API**. This is outside the scope of this package, but the `InputActions` assets used here are fully compatible with it.

See the Unity documentation on [interactive rebinding](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.19/manual/ActionBindings.html#interactive-rebinding) for guidance.

---

## Related

- [Classic RTS Camera Controls](../cameras/classic-rts-camera.md#controls)
- [Simulation Camera Controls](../cameras/simulation-camera.md#controls)
- [Tactical War Camera Controls](../cameras/tactical-war-camera.md#controls)

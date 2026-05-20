# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.1] - 2026-05-20

### Fixed
- Isometric camera with minimap sample scene was missing the correct references.
- Orthographic camera now works with minimap binding.
- EventSystem removed from minimap prefab - documentation added to explain when you need to add it.
- Mousing over minimap and other UI elements now only prevents mouse drag input, while still allowing keyboard input.
- Tactical War Camera minimap binding adjusted to always contain the clicked point in view.

## [1.2.0] - 2026-05-19

### Added
- UGUI and UIToolkit minimaps that work with all camera controllers.

## [1.1.0] - 2026-05-18

### Added
- Orthographic Classic RTS Camera

### Fixed
- The menu for creating HiddenCursorState was named LockedCursorState

## [1.0.0] - 2026-05-14
Initial release

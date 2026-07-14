# GLB Crop Editor

A lightweight, single-file, browser-based editor for cropping and cleaning up GLB/glTF meshes — inspired by the [SuperSplat](https://superspl.at/editor) editing workflow, but for triangle meshes (e.g. photogrammetry / 3D-scan exports).

No install, no build step, no server. Open `index.html` in a browser, drop in a `.glb`, select what you want, crop, and export.

## Features

### Selection tools
- **Rect** — drag a screen-space rectangle (selects through the whole model)
- **Lasso** — freehand outline selection
- **Sphere volume** — click/drag to place a 3D sphere on the model, adjust radius, live yellow preview of what's inside, then apply
- **Box volume** — same, with independent X / Y / Z lengths
- **Set / Add / Remove** selection modes (`Shift` = add, `Ctrl` = remove while dragging)
- Invert / select all / deselect

### Editing
- **Delete selected** triangles
- **Crop** — keep only the selected region, delete everything else
- Multi-level **undo** (`Ctrl+Z`)
- Live triangle / selected / deleted counters

### Viewing
- Clickable **axis gizmo** — snap to orthographic front / back / top / bottom / left / right views
- **Perspective ⇄ orthographic** toggle (`O`)
- Orbit / pan / zoom (right-drag orbits even while a selection tool is active)

### Model transform
- Numeric position / rotation / uniform scale
- Quick ±90° rotations per axis
- **Center at origin** and **Set on ground (Y=0)** helpers
- The transform is baked into the exported GLB

### I/O
- Drag & drop or file-picker loading of `.glb` / `.gltf`
- Draco- and Meshopt-compressed files supported
- Original materials, textures, UVs and vertex colors preserved
- One-click export to `<name>_cropped.glb`

## Usage

1. Open `index.html` in any modern browser (Chrome/Edge/Firefox). Three.js is loaded from a CDN, so an internet connection is required.
   - If your browser blocks it, serve the folder instead: `npx serve .` and open the printed URL.
2. Drag a `.glb` onto the page.
3. Optionally fix the model's orientation and position (Model transform → rotate / Center at origin / Set on ground).
4. Select the region you want to keep with any tool — orthographic side/top views (axis gizmo) pair well with Rect select for clean straight cuts.
5. Click **Crop (keep selected only)** — or select junk and **Delete selected**.
6. **Export GLB**.

### Keyboard shortcuts

| Key | Action |
|---|---|
| `1`–`5` | Move / Rect / Lasso / Sphere / Box tools |
| `I` | Invert selection |
| `A` | Select all |
| `Esc` | Deselect |
| `Del` | Delete selected |
| `K` | Crop (keep selected only) |
| `Ctrl+Z` | Undo |
| `O` | Toggle orthographic / perspective |

## Notes & limitations

- Selection is per-triangle: a triangle is selected when its centroid falls inside the selection shape.
- Rect/Lasso select through the model (front and back). Use the sphere/box volumes for true 3D region selection, or orbit and use Remove mode to trim the far side.
- Triangle meshes only — point clouds and Gaussian-splat PLYs are not supported.
- Skinned/animated models are treated as static geometry; animations are not preserved on export.

## Tech

Plain HTML + [Three.js](https://threejs.org/) (r170) via CDN import map. Everything lives in a single `index.html`.

## License

[MIT](LICENSE)

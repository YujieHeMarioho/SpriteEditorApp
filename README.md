# ZFX Sprite Editor (ZFX 1.0)

A Qt-based 2D sprite editor for creating animated sprites using a pixel grid, including drawing tools, selection/movement, frame management, animated preview, and save/load to a custom `.ssp` file format.

## Features
- Frame-by-frame sprite editing (add/delete frames)
- Animated preview window with configurable FPS
- Tools:
  - Draw (pen)
  - Erase
  - Fill Bucket (flood fill)
  - Selection (click-drag to move painted pixels)
- Color picker
- Resizable grid (grid size slider)
- Theme menu (Dark / Rojo / Sky / Mocha)

## UI Overview
- Main editing area: a `QGraphicsView` grid (`drawingCanvas`)
- Left side: frame picker + add/delete frame buttons
- Right side: preview window that cycles through frames
- Top toolbar buttons:
  - Draw, Erase, Fill, Selection, Color button
- Sliders:
  - FPS slider (controls animation speed)
  - Grid size slider (controls number of cells per side)

## How to Use
1. Pick a color using the color button.
2. Select a tool:
   - `Draw`: paint cells by clicking/dragging on the grid.
   - `Erase`: erase cells (sets them back to transparent).
   - `Fill`: click to flood-fill a transparent region with the selected color.
   - `Selection`: click-drag to move the painted pixels on the grid.
3. Manage animation frames:
   - Click `+` to add a new frame.
   - Click `-` to delete the current frame (cannot delete the last frame).
   - Use the frame spinbox to jump to a frame.
4. Adjust:
   - FPS slider to control preview playback.
   - Grid size slider to change the grid resolution.
5. Use the menu:
   - `File -> Save` to export your animation as a `.ssp` file.
   - `File -> Load` to load a previously saved `.ssp` file.

## `.ssp` File Format
Saved files are JSON with the following structure:

- `gridDimension`: grid width/height (grid is `gridDimension x gridDimension`)
- `frames`: array of frames, where each frame contains `grid`

Each cell stores its color as a string in the form:
- `"R,G,B,A"` (0–255 integers), where `"0,0,0,0"` represents transparency.

Example:
```json
{
  "gridDimension": 10,
  "frames": [
    {
      "grid": [
        ["0,0,0,0", "255,0,0,255", "..."],
        ["...", "...", "..."]
      ]
    }
  ]
}

---
id: "002"
title: "Apply Handle Color to SVG Mug Previews"
stage: general
date: "2026-02-27"
surface: agent
model: claude-opus-4-6
feature: mug-preview
branch: main
user: Hassam Rauf
command: implement handle color tint
labels: ["canvas", "handle-color", "multiply-blend", "svg", "mug-designer"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - deploy/mug-preview-TEST.html
tests: []
---

## Prompt

Implement the following plan:

# Plan: Apply Handle Color to SVG Photo Mode Mug Previews

The handle color picker already exists in the UI (9 colors) and works for the procedural fallback mode, but has no effect in SVG photo mode (the current rendering). The user wants the selected handle color to visually tint the handle in the SVG mug photos.

Approach: After the SVG is drawn with multiply blend (step 5), add a new step 6 that applies the selected handle color as a tinted overlay on the handle region. Define handle region coordinates per zone, use multiply composite operation to tint, skip when white.

## Response

Added two changes to `deploy/mug-preview-TEST.html` in the `_drawPreviewMug` SVG photo mode path:

1. **Handle region coordinates** (after `mugFace` definition, ~line 1756):
   ```javascript
   const handleRegion = {
     front: { hx: 282, hy: 60, hw: 172, hh: 330 },
     rear:  { hx: 0,   hy: 50, hw: 50,  hh: 340 },
     back:  { hx: 0,   hy: 60, hw: 172, hh: 330 },
   };
   ```

2. **Handle color tint step** (after step 5 multiply draw, ~line 1858):
   - Reads `this.selectedHandleColor`
   - Skips if white (`#ffffff`) since multiply with white is a no-op
   - Applies `globalCompositeOperation = 'multiply'` with a `fillRect` over the handle region
   - Coordinates are zone-clip-relative, scaled and offset to match SVG positioning

The handle color picker at line 389 already calls `renderAllZoneCanvases()` on change, so tinting updates reactively.

## Outcome

- Handle color now visually tints the handle in SVG photo mode across all three zones (front, rear, back)
- White handle color correctly shows no tint (original SVG appearance)
- Multiply blend preserves the 3D shading/depth of the original SVG handle
- Design/print area is unaffected by the tint
- Handle region coordinates are approximate and may need visual tuning

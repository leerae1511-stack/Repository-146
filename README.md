# Tool Pocket Generator V146

## Provenance
Built directly from `Tool_Pocket_Generator_V139_FINAL(1).zip`, the explicitly requested starting point. No V140–V145 files or changes were used as the source.

## Exact change
Only the interpretation and drawing of Curve points was changed:
- A Curve point is now an on-outline point. The rendered curve passes through its centre.
- Segments touching a Curve point use Catmull-Rom interpolation through the existing point coordinates.
- Straight-to-Straight segments remain straight.
- The canvas profile and the sampled geometry use the same `sampled()` output, so Geometry Check and downstream geometry that consume `sampled()` see the same curve shape as the drawing.

## Why
In V139, Curve points were used as quadratic Bezier control handles. A Bezier control handle attracts the arc but the arc does not generally pass through it. The screenshot showed the blue C point off the black line. This rebuild changes Curve semantics so C is on the outline.

## Not changed
- Add Point placement logic
- Existing point coordinates, point numbering, and point Straight/Curve assignments
- Finger relief behaviour
- Dimensions, physical grid, workspace, Geometry Check rules, JSON workflow, STL construction, and controls/layout, except version strings/markers
- Saved-tools storage key remains the V139 key for continuity

## Retest
1. Open V146 and load the same profile.
2. Select a point and set it to Curve.
3. Confirm the black outline passes through the centre of the Curve point.
4. Check nearby Straight points remain at their same coordinates and the curve changes locally.
5. Run Geometry Check and confirm the visible curve still passes through the Curve point and is not displaced.
6. Confirm FR arcs and other parts of the outline are unchanged.
7. If correct, then separately test Add Point; Add Point logic was deliberately not changed in this build.

## Verification status
- ZIP integrity and JavaScript syntax checked.
- Source changes checked against V139.
- Not tested in iPad/Safari. The geometry behaviour requires your visual retest.

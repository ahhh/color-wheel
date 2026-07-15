# Color Wheel Studio

A single self-contained HTML page for exploring color-harmony relationships on
an interactive color wheel. Pick a wheel type, drag the nodes around the wheel,
and read off the resulting palette. New wheel types are added with a few lines
of YAML — no build step, no dependencies.

![Tetradic harmony on the wheel](docs/preview.png)

## Usage

Open `index.html` in any modern browser. That's it — everything (markup,
styles, logic, and the built-in wheel definitions) lives in that one file, so it
works offline and can be dropped onto any static host.

- **Drag** any node around the wheel to rotate the whole harmony.
- **Arrow keys** (with the wheel focused) nudge the harmony one segment at a time.
- **Wheel Types** in the right panel switch between harmonies.
- The **Palette** section shows the selected colors, plus six *variations* — the
  same constellation rotated in one-segment steps around the wheel.

## Adding wheel types

Edit the YAML in the **Definitions** panel and press **Load definitions**. Each
entry describes one wheel type:

```yaml
harmonies:
  - name: Split Complementary
    description: A base hue plus the two neighbours of its opposite.
    offsets: [0, 150, 210]
```

| Field         | Meaning                                                                 |
| ------------- | ----------------------------------------------------------------------- |
| `name`        | Label shown in the panel and header.                                    |
| `description` | One-line summary shown under the title.                                 |
| `offsets`     | Node positions in degrees, measured from the draggable base (`0`).      |

Offsets can be negative and are taken modulo 360. Two nodes render as a line;
three or more render as a closed polygon. To make a change permanent, paste the
YAML into the `DEFAULT_YAML` constant near the top of the `<script>` block in
`index.html`.

## How it works

- The wheel is a 24-segment HSL disc where hue maps directly to angle
  (0° = red at the top, increasing clockwise).
- A node's color is snapped to the segment beneath it, so the swatches always
  match exactly what you see on the wheel.
- Colors are named from a 24-entry hue table (Red, Vermilion, Orange, Amber, …).
- A small purpose-built YAML parser handles the definition subset (maps, block
  and flow sequences, scalars) so there are no external libraries.

## Project layout

```
index.html    The entire application
README.md     This file
LICENSE       MIT
```

## License

Released under the [MIT License](LICENSE).

# Nightreign-Overlay-Release

# Nightreign Overlay

**Currently this has only been tested in Solo Expeditions**

## Installation

The overlay requires these two files:

- `ignite_nightreign_overlay.dll`
- `ignite_nightreign_overlay.toml`

Keep them together in the same folder.

Add the DLL to the ME3 profile as a native DLL:

```toml
[[natives]]
enabled = true
path = "/dll/ignite_nightreign_overlay.dll"
load_early = false
```

## Overlay settings

The `[overlay]` section controls the appearance and operating mode:

```toml
[overlay]
mode = "standard"
header = "IGNITE Nightreign Overlay"
scale = 1.0
background_opacity = 0.38
border_opacity = 0.42
corner_radius = 10.0
anchor = "top_right"
horizontal_offset = 24.0
vertical_offset = 90.0
width = 320.0
padding = 12.0
label_column_width = 190.0
```

- `mode`: Use `"standard"` for run statistics only or `"tournament"` to add Score.
- `header`: Text displayed at the top of the overlay. An empty string hides the header.
- `scale`: Scales the font and panel. The DLL limits it to `0.5` through `3.0`.
- `background_opacity`: Background visibility from `0.0` (invisible) to `1.0` (opaque).
- `border_opacity`: Border visibility from `0.0` to `1.0`.
- `corner_radius`: Roundness of the panel corners in pixels.
- `anchor`: One of `"top_left"`, `"top_right"`, `"bottom_left"`, or `"bottom_right"`.
- `horizontal_offset`: Distance inward from the selected horizontal screen edge.
- `vertical_offset`: Distance inward from the selected vertical screen edge.
- `width`: Panel width before scaling.
- `padding`: Space between the panel border and its contents.
- `label_column_width`: Width reserved for labels; statistic values remain right-aligned.

## Tournament scoring

Tournament mode calculates Score from accumulated runes, enemies felled, great enemies felled, and
treasure found. Each statistic has a group size and points awarded for each completed group:

```toml
[tournament.runes]
units_per_group = 10000
points_per_group = 5

[tournament.enemies]
units_per_group = 10
points_per_group = 2

[tournament.great_enemies]
units_per_group = 1
points_per_group = 10

[tournament.treasure]
units_per_group = 1
points_per_group = 1
```

Only completed groups count. With the settings above:

- 25,000 accumulated runes award 10 points.
- 24 enemies award 4 points because they contain two complete groups of 10.
- 2 great enemies award 20 points.
- 3 treasures award 3 points.
- The displayed total is 37 points.

Set `points_per_group = 0` to disable scoring for a statistic. A `units_per_group` value of `0` also
disables that rule. Statistics and Score update approximately once per second.

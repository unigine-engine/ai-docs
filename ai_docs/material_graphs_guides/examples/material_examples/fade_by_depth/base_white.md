# base_white

This example demonstrates how to implement an effect of fading by depth.

- **Sample:** Fade By Depth Example
- **Source:** `art_samples/material_examples/fade_by_depth/materials/base_white.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 3 nodes, 2 links, 0 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 2 (Tangent) |
| `vertex_mode` | 0 (Position) |
| `two_sided` | False |
| `tessellation` | False |
| `depth_test` | True |

## What drives the Material node

- **Albedo** <- `float`

## Node inventory

`Final`, `Material`, `float`

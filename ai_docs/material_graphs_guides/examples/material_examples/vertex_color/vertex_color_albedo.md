# vertex_color_albedo

This example demonstrates how to use vertex color for texture blending when creating materials.

- **Sample:** Vertex Color Example
- **Source:** `art_samples/material_examples/vertex_color/materials/vertex_color_albedo.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 4 nodes, 3 links, 0 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 2 (Tangent) |
| `vertex_mode` | 1 (Offset) |
| `two_sided` | False |
| `tessellation` | False |
| `depth_test` | True |
| `blend_mode` | 0 |
| `depth_shadow` | True |
| `screen_projection` | False |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- `Vertex Color`

## Node inventory

`Expression`, `Final`, `Material`, `Vertex Color`

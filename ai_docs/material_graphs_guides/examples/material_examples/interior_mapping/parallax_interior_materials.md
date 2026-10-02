# parallax_interior_materials

This example demonstrates how to create the effect of parallax interior mapping when creating materials.

- **Sample:** Interior Mapping Example
- **Source:** `art_samples/material_examples/interior_mapping/interior_room/materials/parallax_interior_materials.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 5 nodes, 4 links, 2 parameters

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
| `blend_mode` | 0 |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo_color` | Color | `1 1 1 1` |  |
| `roughness` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- parameter `albedo_color`
- **Roughness** <- parameter `roughness`

## Node inventory

`Parameter` x2, `Expression`, `Final`, `Material`

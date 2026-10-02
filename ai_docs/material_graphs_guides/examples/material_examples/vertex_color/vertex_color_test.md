# vertex_color_test

This example demonstrates how to use vertex color for texture blending when creating materials.

- **Sample:** Vertex Color Example
- **Source:** `art_samples/material_examples/vertex_color/materials/vertex_color_test.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 4 nodes, 3 links, 8 parameters

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
| `Albedo A` | Texture2D |  | `factory_brick_alb.texture` |
| `Albedo B` | Texture2D |  | `jct_pavement_alb.texture` |
| `Albedo C` | Texture2D |  | `wood_2_alb.texture` |
| `Albedo D` | Texture2D |  | `stones_alb.texture` |
| `Normal A` | Texture2D |  | `factory_brick_n.texture` |
| `Normal B` | Texture2D |  | `jct_pavement_n.texture` |
| `Normal C` | Texture2D |  | `wood_2_n.texture` |
| `Normal D` | Texture2D |  | `rocks_n.texture` |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- `Vertex Color`

## Node inventory

`Expression`, `Final`, `Material`, `Vertex Color`

# normal_from_height_texture

This example demonstrates how to convert a height value from a height texture to normals.

- **Sample:** Normal From Height Texture Example
- **Source:** `art_samples/material_examples/normal_from_height_texture/materials/normal_from_height_texture.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 9 nodes, 8 links, 5 parameters

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

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `0` |  |
| `roughness` | Slider | `0.5` |  |
| `Height` | Texture2D |  | `jct_pavement_h.texture` |
| `Height Value` | Slider | `0.00999999977648265` |  |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- parameter `albedo_color`
- **Metalness** <- parameter `metalness`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- subgraph `normal from height texture.msubgraph`
  - **Heightmap Texture** <- parameter `Height`
  - **Height (Meters)** <- parameter `Height Value`

## Node inventory

`Parameter` x5, `Expression`, `Final`, `Material`, `SubGraph`

## Subgraphs used

- `normal from height texture.msubgraph`

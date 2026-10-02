# normal_map_tangent_space

This example demonstrates how to use tangent-space normal maps.

- **Sample:** Tangent-Space Normal Map Example
- **Source:** `art_samples/material_examples/normal_map_tangent_space/materials/normal_map_tangent_space.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 6 nodes, 5 links, 3 parameters

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
| `Normal` | Texture2D |  | `boxes_seams_on_hard_edges_n.texture` |
| `Color` | Color | `0.4901959896087648 0 0 1` |  |
| `a` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- parameter `Color`
- **Roughness** <- `float`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Normal`

## Node inventory

`Parameter` x2, `Final`, `Material`, `SampleTexture`, `float`

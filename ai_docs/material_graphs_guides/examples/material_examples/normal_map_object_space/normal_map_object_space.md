# normal_map_object_space

This example demonstrates how to use object-space normal maps.

- **Sample:** Object-Space Normal Map Example
- **Source:** `art_samples/material_examples/normal_map_object_space/materials/normal_map_object_space.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 6 nodes, 5 links, 2 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 1 (Object) |
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
| `Color` | Color | `0.4901959896087648 0 0 1` |  |
| `Normal` | Texture2D |  | `boxes_nrgb.png` |

## What drives the Material node

- **Albedo** <- parameter `Color`
- **Roughness** <- `float`
- **Normal Object Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Normal`

## Node inventory

`Parameter` x2, `Final`, `Material`, `SampleTexture`, `float`

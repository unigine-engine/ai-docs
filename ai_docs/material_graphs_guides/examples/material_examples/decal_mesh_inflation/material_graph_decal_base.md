# material_graph_decal_base

This example demonstrates how to implement Geometry Inflation based on camera distance for Mesh Decals. The technique helps preserve visibility for very thin elements when TAA is enabled. For 3D objects (e.g., lampposts, pipes, ropes, cables, antennas, etc.), it works by offsetting vertices along their normal vectors, making them appear slightly thicker as they move farther away from the camera. For meshes see the Geometry Inflation sample.

- **Sample:** Decal Mesh Inflation
- **Source:** `art_samples/material_examples/decal_mesh_inflation/materials/material_graph_decal_base.mgraph`
- **Graph type:** 4 (Decal PBR)
- **Size:** 11 nodes, 11 links, 5 parameters

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
| `cast_gi` | False |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `0` |  |
| `roughness` | Slider | `0.5` |  |

## What drives the Material node

- **Opacity** <- expression `w`
  - **in** <- `_multiply` (Multiply)
    - **A** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo`
    - **B** <- parameter `albedo_color`
- **Albedo** <- `_multiply` (Multiply)
  - **A** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `albedo`
  - **B** <- parameter `albedo_color`
- **Metalness** <- parameter `metalness`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`

## Node inventory

`Parameter` x5, `SampleTexture` x2, `Expression`, `Final`, `Material`, `_multiply`

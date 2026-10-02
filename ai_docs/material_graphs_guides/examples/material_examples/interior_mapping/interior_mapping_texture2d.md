# interior_mapping_texture2d

This example demonstrates how to create the effect of parallax interior mapping when creating materials.

- **Sample:** Interior Mapping Example
- **Source:** `art_samples/material_examples/interior_mapping/materials/interior_mapping_texture2d.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 12 nodes, 11 links, 7 parameters

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
| `texture2D` | Texture2D |  | `white.texture` |
| `parallax_multiplier` | Slider | `1` |  |
| `sides_correction` | Slider | `0.4199999868869783` |  |
| `perspective_correction` | Slider | `0` |  |
| `tiling` | Float2 | `1 1` |  |
| `offset` | Float2 | `1 1` |  |
| `roughness` | Slider | `0.5` |  |

## What drives the Material node

- **Albedo** <- `float`
- **Roughness** <- parameter `roughness`
- **Emission** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `texture2D`
  - **UV** <- subgraph `interior mapping texture2d.msubgraph`
    - **Parallax Multiplier** <- parameter `parallax_multiplier`
    - **Tiling** <- parameter `tiling`
    - **Offset** <- parameter `offset`
    - **Sides Correction** <- parameter `sides_correction`
    - **Perspective Correction** <- parameter `perspective_correction`

## Node inventory

`Parameter` x7, `Final`, `Material`, `SampleTexture`, `SubGraph`, `float`

## Subgraphs used

- `interior mapping texture2d.msubgraph`

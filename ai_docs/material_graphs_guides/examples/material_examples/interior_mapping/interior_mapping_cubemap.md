# interior_mapping_cubemap

This example demonstrates how to create the effect of parallax interior mapping when creating materials.

- **Sample:** Interior Mapping Example
- **Source:** `art_samples/material_examples/interior_mapping/materials/interior_mapping_cubemap.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 10 nodes, 9 links, 5 parameters

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
| `cubemap` | TextureCube |  | `environment_default.texture` |
| `parallax_multiplier` | Slider | `1` |  |
| `tiling` | Float2 | `1 1` |  |
| `offset` | Float2 | `0 0` |  |
| `roughness` | Slider | `0.5` |  |

## What drives the Material node

- **Albedo** <- `float`
- **Roughness** <- parameter `roughness`
- **Emission** <- `SampleTexture` (SampleTexture: Mip)
  - **Texture** <- parameter `cubemap`
  - **Direction** <- subgraph `interior mapping cubemap.msubgraph`
    - **Parallax Multiplier** <- parameter `parallax_multiplier`
    - **Tiling** <- parameter `tiling`
    - **Offset** <- parameter `offset`

## Node inventory

`Parameter` x5, `Final`, `Material`, `SampleTexture`, `SubGraph`, `float`

## Subgraphs used

- `interior mapping cubemap.msubgraph`

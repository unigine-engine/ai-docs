# chameleon_paint_by_ramp

This example illustrates imitation of the chameleon paint and curve-based color correction using the Texture Ramp RGB node.

- **Sample:** Ramp RGB-Texture Example
- **Source:** `art_samples/material_examples/ramp_rgb_texture/materials/chameleon_paint_by_ramp.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 8 nodes, 7 links, 3 parameters

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
| `ramp` | TextureRamp RGB |  |  |
| `metalness` | Slider | `0` |  |
| `roughness` | Slider | `0.5` |  |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- `SampleTexture` (SampleTexture: Mip)
    - **Texture** <- parameter `ramp`
    - **U** <- subgraph `fresnel.msubgraph`
- **Metalness** <- parameter `metalness`
- **Roughness** <- parameter `roughness`

## Node inventory

`Parameter` x3, `Expression`, `Final`, `Material`, `SampleTexture`, `SubGraph`

## Subgraphs used

- `fresnel.msubgraph`

# color_correction_by_ramp

This example illustrates imitation of the chameleon paint and curve-based color correction using the Texture Ramp RGB node.

- **Sample:** Ramp RGB-Texture Example
- **Source:** `art_samples/material_examples/ramp_rgb_texture/materials/color_correction_by_ramp.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 7 nodes, 6 links, 2 parameters

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
| `albedo` | Texture2D |  | `white.texture` |

## What drives the Material node

- **Albedo** <- subgraph `color_correction_by_ramp.msubgraph`
  - **Source Color** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo`
  - **Texture Ramp RGB** <- parameter `ramp`

## Node inventory

`Parameter` x2, `Expression`, `Final`, `Material`, `SampleTexture`, `SubGraph`

## Subgraphs used

- `color_correction_by_ramp.msubgraph`

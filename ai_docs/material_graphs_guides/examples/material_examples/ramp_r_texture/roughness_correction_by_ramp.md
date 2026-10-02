# roughness_correction_by_ramp

This example illustrates imitation of scratches and curve-based intensity adjustment for a single-channel texture using the Texture Ramp R node.

- **Sample:** Ramp R-Texture Example
- **Source:** `art_samples/material_examples/ramp_r_texture/materials/roughness_correction_by_ramp.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 14 nodes, 13 links, 4 parameters

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
| `albedo_color` | Color | `0.47058799862861656 0.47058799862861656 0.47058799862861656 1` |  |
| `ramp` | TextureRamp R |  |  |
| `metalness` | Slider | `0` |  |
| `roughness` | Texture2D |  | `white.texture` |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- parameter `albedo_color`
- **Metalness** <- parameter `metalness`
- **Roughness** <- expression `x`
  - **in** <- `SampleTexture` (SampleTexture: Mip)
    - **Texture** <- parameter `ramp`
    - **U** <- expression `y`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `roughness`
        - **UV** <- `_multiply` (Multiply)
          - **A** <- `Vertex UV 0`
          - **B** <- `float`

## Node inventory

`Parameter` x4, `Expression` x3, `SampleTexture` x2, `Final`, `Material`, `Vertex UV 0`, `_multiply`, `float`

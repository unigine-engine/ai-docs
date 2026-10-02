# hair_temporal_filter

This sample illustrates how to create hair or fur.

- **Sample:** Hair Shading Example
- **Source:** `art_samples/material_examples/hair_shading/materials/hair_temporal_filter.mgraph`
- **Graph type:** 3 (Mesh Transparent Unlit)
- **Size:** 34 nodes, 34 links, 5 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 2 (View) |
| `vertex_offset_space` | 3 (View) |
| `vertex_mode` | 0 (Position) |
| `two_sided` | True |
| `tessellation` | False |
| `depth_test` | True |
| `blend_mode` | 3 |
| `cast_gi` | False |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `opacity_texture` | Texture2D |  | `white.texture` |
| `opacity` | Slider | `10` |  |
| `polygon_view_direction_offset` | Slider | `0.10000000149011612` |  |
| `temporal_filtering_intensity` | Slider | `1` |  |
| `velocity_clamping` | Slider | `200` |  |

## What drives the Material node

- **Opacity** <- `saturate` (Saturate)
  - **Value** <- `_multiply` (Multiply)
    - **A** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `opacity_texture`
    - **B** <- parameter `opacity`
- **Color** <- expression `x,y,z`
  - **in** <- `lerp` (Lerp)
    - **A** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- `Screen Color Old` (Texture Buffer Screen Color Old)
      - **UV** <- `_add` (Add)
        - **A** <- `Screen UV`
        - **B** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- `GBuffer Velocity` (Texture Buffer GBuffer Velocity)
          - **UV** <- `Screen UV`
    - **B** <- `SampleTexture` (SampleTexture: Catmull)
      - **Texture** <- `Screen Color Opacity` (Texture Buffer Screen Color Opacity)
      - **UV** <- `Screen UV`
    - **Coefficient** <- `lerp` (Lerp)
      - **A** <- expression `1-x`
        - **in** <- parameter `temporal_filtering_intensity`
      - **B** <- `float`
      - **Coefficient** <- `saturate` (Saturate)
        - **Value** <- `_multiply` (Multiply)
          - **A** <- `length` (Length)
            - ...
          - **B** <- parameter `velocity_clamping`
- **Vertex Position View Space** <- `_add` (Add)
  - **A** <- `Vertex Position`
  - **B** <- `_multiply` (Multiply)
    - **A** <- `View Direction`
    - **B** <- parameter `polygon_view_direction_offset`
- **PostEffects Clip Threshold** <- `float`

## Node inventory

`Parameter` x5, `SampleTexture` x4, `Expression` x3, `Screen UV` x3, `_multiply` x3, `_add` x2, `float` x2, `lerp` x2, `saturate` x2, `Final`, `GBuffer Velocity`, `Material`, `Screen Color Old`, `Screen Color Opacity`, `Vertex Position`, `View Direction`, `length`

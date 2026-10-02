# ui_transparent_base

- **Source:** `showcase_content/materials/base_materials/ui_transparent_base.mgraph`
- **Graph type:** 3 (Mesh Transparent Unlit)
- **Size:** 21 nodes, 22 links, 6 parameters

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
| `opacity_texture` | Texture2D |  | `white.texture` |
| `emission` | Texture2D |  | `white.texture` |
| `opacity` | Slider | `1` |  |
| `emission_color` | Color | `1 1 1 1` |  |
| `emission_scale` | Slider | `1` |  |
| `uv_transform` | Float4 | `1 1 0 0` |  |

## What drives the Material node

- **Opacity** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `opacity_texture`
      - **UV** <- subgraph `tiling and offset.msubgraph`
        - **UV** <- `Vertex UV 0`
        - **Tiling** <- expression `x,y`
          - **in** <- parameter `uv_transform`
        - **Offset** <- expression `z,w`
          - **in** <- parameter `uv_transform`
  - **B** <- parameter `opacity`
- **Color** <- `_multiply` (Multiply)
  - **A** <- `srgbInv` (Srgb Inverse)
    - **Color** <- `_multiply` (Multiply)
      - **A** <- expression `x,y,z`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `emission`
          - **UV** <- subgraph `tiling and offset.msubgraph`
            - ...
      - **B** <- expression `x,y,z`
        - **in** <- parameter `emission_color`
  - **B** <- parameter `emission_scale`

## Node inventory

`Parameter` x6, `Expression` x5, `_multiply` x3, `SampleTexture` x2, `Final`, `Material`, `SubGraph`, `Vertex UV 0`, `srgbInv`

## Subgraphs used

- `tiling and offset.msubgraph`

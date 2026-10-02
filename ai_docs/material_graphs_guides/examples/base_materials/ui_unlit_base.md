# ui_unlit_base

- **Source:** `showcase_content/materials/base_materials/ui_unlit_base.mgraph`
- **Graph type:** 3 (Mesh Transparent Unlit)
- **Size:** 22 nodes, 25 links, 5 parameters

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
| `emission` | Texture2D |  | `white.texture` |
| `emission_color` | Color | `1 1 1 1` |  |
| `emission_scale` | Slider | `1` |  |
| `uv_transform` | Float4 | `1 1 0 0` |  |
| `use_alpha_channel` | Int | `0` |  |

## What drives the Material node

- **Opacity** <- `Branch`
  - **Condition** <- parameter `use_alpha_channel`
  - **True** <- `_multiply` (Multiply)
    - **A** <- expression `w`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `emission`
        - **UV** <- subgraph `tiling and offset.msubgraph`
          - **UV** <- `Vertex UV 0`
          - **Tiling** <- expression `x,y`
            - ...
          - **Offset** <- expression `z,w`
            - ...
    - **B** <- expression `w`
      - **in** <- parameter `emission_color`
  - **False** <- expression `w`
    - **in** <- parameter `emission_color`
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

`Expression` x7, `Parameter` x5, `_multiply` x3, `Branch`, `Final`, `Material`, `SampleTexture`, `SubGraph`, `Vertex UV 0`, `srgbInv`

## Subgraphs used

- `tiling and offset.msubgraph`

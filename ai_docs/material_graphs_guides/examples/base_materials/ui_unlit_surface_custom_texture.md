# ui_unlit_surface_custom_texture

- **Source:** `showcase_content/materials/base_materials/ui_unlit_surface_custom_texture.mgraph`
- **Graph type:** 3 (Mesh Transparent Unlit)
- **Size:** 14 nodes, 14 links, 3 parameters

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
| `uv_transform` | Float4 | `1 1 0 0` |  |
| `use_alpha_channel` | Int | `0` |  |
| `uv_channel` | Int | `0` |  |

## What drives the Material node

- **Color** <- expression `x,x,x`
  - **in** <- `srgbInv` (Srgb Inverse)
    - **Color** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- `Surface Custom Texture`
      - **UV** <- subgraph `tiling and offset.msubgraph`
        - **UV** <- `Branch`
          - **Condition** <- parameter `uv_channel`
          - **True** <- `Vertex UV 1`
          - **False** <- `Vertex UV 0`
        - **Tiling** <- expression `x,y`
          - **in** <- parameter `uv_transform`
        - **Offset** <- expression `z,w`
          - **in** <- parameter `uv_transform`

## Node inventory

`Expression` x3, `Parameter` x2, `Branch`, `Final`, `Material`, `SampleTexture`, `SubGraph`, `Surface Custom Texture`, `Vertex UV 0`, `Vertex UV 1`, `srgbInv`

## Subgraphs used

- `tiling and offset.msubgraph`

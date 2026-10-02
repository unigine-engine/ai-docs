# pbr_detail_multiply_base

- **Source:** `showcase_content/materials/base_materials/pbr_detail_multiply_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 113 nodes, 113 links, 27 parameters

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
| `albedo` | Texture2D |  | `white.texture` |
| `shading` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `uv_transform` | Float4 | `1 1 1 1` |  |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `1` |  |
| `roughness` | Slider | `1` |  |
| `normal_scale` | Slider | `1` |  |
| `specular` | Slider | `0.5` |  |
| `microfiber` | Slider | `0` |  |
| `translucent` | Slider | `0` |  |
| `detail_albedo` | Texture2D |  | `white.texture` |
| `detail_shading` | Texture2D |  | `white.texture` |
| `detail_normal` | Texture2D |  | `normal.texture` |
| `detail_mask` | Texture2D |  | `white.texture` |
| `detail_uv_transform` | Float4 | `1 1 1 1` |  |
| `detail_mask_uv_transform` | Float4 | `1 1 1 1` |  |
| `detail_albedo_color` | Color | `1 1 1 1` |  |
| `detail_metalness` | Slider | `1` |  |
| `detail_roughness` | Slider | `1` |  |
| `detail_normal_visible` | Slider | `1` |  |
| `detail_albedo_color_visible` | Slider | `1` |  |
| `detail_metalness_visible` | Slider | `1` |  |
| `detail_roughness_visible` | Slider | `1` |  |
| `base_uv_channel` | Int | `0` |  |
| `detail_uv_channel` | Int | `0` |  |
| `detail_mask_uv_channel` | Int | `0` |  |

## What drives the Material node

- **Albedo** <- `_multiply` (Multiply)
  - **A** <- portal Portal Out
  - **B** <- expression `x,y,z`
    - **in** <- `lerp` (Lerp)
      - **A** <- `float4`
      - **B** <- portal Portal Out
      - **Coefficient** <- `_multiply` (Multiply)
        - **A** <- `_multiply` (Multiply)
          - **A** <- parameter `detail_albedo_color_visible`
          - **B** <- portal Portal Out
        - **B** <- expression `w`
          - **in** <- portal Portal Out
- **Metalness** <- `_multiply` (Multiply)
  - **A** <- portal Portal Out
  - **B** <- `lerp` (Lerp)
    - **A** <- `float`
    - **B** <- portal Portal Out
    - **Coefficient** <- `_multiply` (Multiply)
      - **A** <- `_multiply` (Multiply)
        - **A** <- parameter `detail_metalness_visible`
        - **B** <- portal Portal Out
      - **B** <- expression `w`
        - **in** <- portal Portal Out
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- portal Portal Out
  - **B** <- `lerp` (Lerp)
    - **A** <- `float`
    - **B** <- portal Portal Out
    - **Coefficient** <- `_multiply` (Multiply)
      - **A** <- `_multiply` (Multiply)
        - **A** <- parameter `detail_roughness_visible`
        - **B** <- portal Portal Out
      - **B** <- expression `w`
        - **in** <- portal Portal Out
- **Specular** <- parameter `specular`
- **Microfiber** <- parameter `microfiber`
- **Normal Tangent Space** <- `reorientNormalBlend` (Reorient Normal Blend)
  - **Base Normal** <- portal Portal Out
  - **Detail Normal** <- portal Portal Out
- **Translucent** <- parameter `translucent`

## Node inventory

`Parameter` x27, `Expression` x19, `_multiply` x16, `PortalOut` x14, `PortalIn` x9, `SampleTexture` x7, `Branch` x3, `SubGraph` x3, `Vertex UV 0` x3, `Vertex UV 1` x3, `lerp` x3, `float` x2, `Final`, `Material`, `float4`, `reorientNormalBlend`

## Subgraphs used

- `tiling and offset.msubgraph`

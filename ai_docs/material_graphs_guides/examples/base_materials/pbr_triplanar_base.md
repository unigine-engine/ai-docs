# pbr_triplanar_base

- **Source:** `showcase_content/materials/base_materials/pbr_triplanar_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 34 nodes, 37 links, 14 parameters

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
| `ambient_occlusion` | Texture2D |  | `white.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `1` |  |
| `roughness` | Slider | `1` |  |
| `normal_scale` | Slider | `1` |  |
| `specular` | Slider | `0.5` |  |
| `microfiber` | Slider | `0` |  |
| `translucent` | Slider | `0` |  |
| `uv_transform` | Float3 | `1 1 1` |  |
| `ao_uv_transform` | Float4 | `1 1 0 0` |  |
| `triplanar_blend` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- subgraph `triplanar color.msubgraph`
      - **Texture2D** <- parameter `albedo`
      - **Blend** <- parameter `triplanar_blend`
      - **Tiling** <- parameter `uv_transform`
  - **B** <- expression `x,y,z`
    - **in** <- parameter `albedo_color`
- **Metalness** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- subgraph `triplanar color.msubgraph`
      - **Texture2D** <- parameter `shading`
      - **Blend** <- parameter `triplanar_blend`
      - **Tiling** <- parameter `uv_transform`
  - **B** <- parameter `metalness`
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- expression `y`
    - **in** <- subgraph `triplanar color.msubgraph`
      - **Texture2D** <- parameter `shading`
      - **Blend** <- parameter `triplanar_blend`
      - **Tiling** <- parameter `uv_transform`
  - **B** <- parameter `roughness`
- **Specular** <- parameter `specular`
- **Microfiber** <- parameter `microfiber`
- **Normal Tangent Space** <- `RotateSpace` (Rotate Space)
  - **Object** <- subgraph `triplanar normal.msubgraph`
    - **NormalMap Texture** <- parameter `normal`
    - **Blend** <- parameter `triplanar_blend`
    - **Tiling** <- parameter `uv_transform`
- **Translucent** <- parameter `translucent`
- **Ambient Occlusion** <- expression `x`
  - **in** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `ambient_occlusion`
    - **UV** <- subgraph `tiling and offset.msubgraph`
      - **UV** <- `Vertex UV 0`
      - **Tiling** <- expression `x,y`
        - **in** <- parameter `ao_uv_transform`
      - **Offset** <- expression `z,w`
        - **in** <- parameter `ao_uv_transform`

## Node inventory

`Parameter` x15, `Expression` x7, `SubGraph` x4, `_multiply` x3, `Final`, `Material`, `RotateSpace`, `SampleTexture`, `Vertex UV 0`

## Subgraphs used

- `triplanar color.msubgraph`
- `tiling and offset.msubgraph`
- `triplanar normal.msubgraph`

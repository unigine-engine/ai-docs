# pbr_triplanar(os)_tessellation_base

- **Source:** `showcase_content/materials/base_materials/pbr_triplanar(os)_tessellation_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 54 nodes, 53 links, 17 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 2 (Tangent) |
| `vertex_mode` | 0 (Position) |
| `two_sided` | False |
| `tessellation` | True |
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
| `displacement` | Texture2D |  | `white.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `1` |  |
| `roughness` | Slider | `1` |  |
| `specular` | Slider | `0.5` |  |
| `microfiber` | Slider | `0` |  |
| `translucent` | Slider | `0` |  |
| `uv_transform` | Float3 | `1 1 1` |  |
| `ao_uv_transform` | Float4 | `1 1 0 0` |  |
| `triplanar_blend` | Slider | `1` |  |
| `tessellation_factor` | Slider | `1` |  |
| `displacement_scale` | Slider | `0.5` |  |
| `heightmap_mid_point` | Slider | `0.5` |  |

## What drives the Material node

- **Albedo** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- subgraph `triplanar color.msubgraph`
      - **Texture2D** <- parameter `albedo`
      - **Blend** <- parameter `triplanar_blend`
      - **Tiling** <- portal Portal Out
  - **B** <- expression `x,y,z`
    - **in** <- parameter `albedo_color`
- **Metalness** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- subgraph `triplanar color.msubgraph`
      - **Texture2D** <- parameter `shading`
      - **Blend** <- parameter `triplanar_blend`
      - **Tiling** <- portal Portal Out
  - **B** <- parameter `metalness`
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- expression `y`
    - **in** <- subgraph `triplanar color.msubgraph`
      - **Texture2D** <- parameter `shading`
      - **Blend** <- parameter `triplanar_blend`
      - **Tiling** <- portal Portal Out
  - **B** <- parameter `roughness`
- **Specular** <- parameter `specular`
- **Microfiber** <- parameter `microfiber`
- **Normal Tangent Space** <- `RotateSpace` (Rotate Space)
  - **Object** <- subgraph `triplanar normal.msubgraph`
    - **NormalMap Texture** <- parameter `normal`
    - **Blend** <- parameter `triplanar_blend`
    - **Tiling** <- portal Portal Out
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
- **Tessellation Factor** <- parameter `tessellation_factor`
- **Tessellation Vertex Object Position** <- portal Portal Out

## Node inventory

`Parameter` x20, `Expression` x8, `PortalOut` x5, `SubGraph` x5, `_multiply` x5, `PortalIn` x2, `Final`, `Material`, `RotateSpace`, `SampleTexture`, `Vertex Normal`, `Vertex Position`, `Vertex UV 0`, `_add`, `_subtract`

## Subgraphs used

- `triplanar color.msubgraph`
- `tiling and offset.msubgraph`
- `triplanar normal.msubgraph`

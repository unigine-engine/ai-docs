# pbr_tessellation_base

- **Source:** `showcase_content/materials/base_materials/pbr_tessellation_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 61 nodes, 60 links, 18 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 1 (Object) |
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
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `1` |  |
| `roughness` | Slider | `1` |  |
| `normal_scale` | Slider | `1` |  |
| `specular` | Slider | `0.5` |  |
| `microfiber` | Slider | `0` |  |
| `translucent` | Slider | `0` |  |
| `uv_transform` | Float4 | `1 1 0 0` |  |
| `ao_uv_transform` | Float4 | `1 1 0 0` |  |
| `displacement` | Texture2D |  | `white.texture` |
| `tessellation density map` | Texture2D |  | `white.texture` |
| `displacement scale` | Slider | `1` |  |
| `tessellation factor` | Slider | `0.5` |  |
| `heightmap_mid_point` | Slider | `0.5` |  |

## What drives the Material node

- **Albedo** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo`
      - **UV** <- portal Portal Out
  - **B** <- expression `x,y,z`
    - **in** <- parameter `albedo_color`
- **Metalness** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
      - **UV** <- portal Portal Out
  - **B** <- parameter `metalness`
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- expression `y`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
      - **UV** <- portal Portal Out
  - **B** <- parameter `roughness`
- **Specular** <- parameter `specular`
- **Microfiber** <- parameter `microfiber`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
  - **UV** <- portal Portal Out
  - **Normal Intensity** <- parameter `normal_scale`
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
- **Tessellation Factor** <- portal Portal Out
- **Tessellation Vertex Object Position** <- portal Portal Out

## Node inventory

`Parameter` x18, `Expression` x11, `PortalOut` x7, `SampleTexture` x6, `_multiply` x6, `PortalIn` x3, `SubGraph` x2, `Vertex UV 0` x2, `Final`, `Material`, `Vertex Normal`, `Vertex Position`, `_add`, `_subtract`

## Subgraphs used

- `tiling and offset.msubgraph`

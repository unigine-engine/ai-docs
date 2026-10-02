# pbr_geometry_inflation_base

- **Source:** `showcase_content/materials/base_materials/pbr_geometry_inflation_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 42 nodes, 46 links, 18 parameters

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
| `geometry_inflation` | Bool | `0` |  |
| `albedo` | Texture2D |  | `white.texture` |
| `shading` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `ambient_occlusion` | Texture2D |  | `white.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `0` |  |
| `roughness` | Slider | `1` |  |
| `normal_scale` | Slider | `1` |  |
| `specular` | Slider | `0.5` |  |
| `microfiber` | Slider | `0` |  |
| `translucent` | Slider | `0` |  |
| `uv_transform` | Float4 | `1 1 0 0` |  |
| `ao_uv_transform` | Float4 | `1 1 0 0` |  |
| `inflation` | Group |  |  |
| `inflation_min_threshold` | Slider | `0` |  |
| `inflation_scale` | Slider | `0.025000000372529037` |  |
| `inflation_max_threshold` | Slider | `1000` |  |

## What drives the Material node

- **Albedo** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo`
      - **UV** <- subgraph `tiling and offset.msubgraph`
        - **UV** <- `Vertex UV 0`
        - **Tiling** <- expression `x,y`
          - **in** <- parameter `uv_transform`
        - **Offset** <- expression `z,w`
          - **in** <- parameter `uv_transform`
  - **B** <- expression `x,y,z`
    - **in** <- parameter `albedo_color`
- **Metalness** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
      - **UV** <- subgraph `tiling and offset.msubgraph`
        - **UV** <- `Vertex UV 0`
        - **Tiling** <- expression `x,y`
          - **in** <- parameter `uv_transform`
        - **Offset** <- expression `z,w`
          - **in** <- parameter `uv_transform`
  - **B** <- parameter `metalness`
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- expression `y`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
      - **UV** <- subgraph `tiling and offset.msubgraph`
        - **UV** <- `Vertex UV 0`
        - **Tiling** <- expression `x,y`
          - **in** <- parameter `uv_transform`
        - **Offset** <- expression `z,w`
          - **in** <- parameter `uv_transform`
  - **B** <- parameter `roughness`
- **Specular** <- parameter `specular`
- **Microfiber** <- parameter `microfiber`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
  - **UV** <- subgraph `tiling and offset.msubgraph`
    - **UV** <- `Vertex UV 0`
    - **Tiling** <- expression `x,y`
      - **in** <- parameter `uv_transform`
    - **Offset** <- expression `z,w`
      - **in** <- parameter `uv_transform`
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
- **Vertex Offset Tangent Space** <- `Branch`
  - **Condition** <- parameter `geometry_inflation`
  - **True** <- subgraph `geometry_inflation.msubgraph`
    - **Inflation Min Threshold** <- parameter `inflation_min_threshold`
    - **Inflation Scale** <- parameter `inflation_scale`
    - **Inflation Max Threshold** <- parameter `inflation_max_threshold`
  - **False** <- `float3`

## Node inventory

`Parameter` x17, `Expression` x9, `SampleTexture` x4, `SubGraph` x3, `_multiply` x3, `Vertex UV 0` x2, `Branch`, `Final`, `Material`, `float3`

## Subgraphs used

- `tiling and offset.msubgraph`
- `geometry_inflation.msubgraph`

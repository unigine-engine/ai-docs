# pbr_alphatest_two_sided_base

- **Source:** `showcase_content/materials/base_materials/pbr_alphatest_two_sided_base.mgraph`
- **Graph type:** 1 (Mesh Alpha Test PBR)
- **Size:** 28 nodes, 32 links, 11 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 2 (Tangent) |
| `vertex_mode` | 1 (Offset) |
| `two_sided` | True |
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
| `albedo` | Texture2D |  | `white.texture` |
| `shading` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `0` |  |
| `roughness` | Slider | `1` |  |
| `normal_scale` | Slider | `1` |  |
| `specular` | Slider | `0.5` |  |
| `microfiber` | Slider | `0` |  |
| `translucent` | Slider | `0` |  |
| `uv_transform` | Float4 | `1 1 0 0` |  |

## What drives the Material node

- **Opacity** <- expression `w`
  - **in** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `albedo`
    - **UV** <- subgraph `tiling and offset.msubgraph`
      - **UV** <- `Vertex UV 0`
      - **Tiling** <- expression `x,y`
        - **in** <- parameter `uv_transform`
      - **Offset** <- expression `z,w`
        - **in** <- parameter `uv_transform`
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

## Node inventory

`Parameter` x11, `Expression` x7, `SampleTexture` x3, `_multiply` x3, `Final`, `Material`, `SubGraph`, `Vertex UV 0`

## Subgraphs used

- `tiling and offset.msubgraph`

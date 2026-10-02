# pbr_alphatest_spherelized_normals_base

- **Source:** `showcase_content/materials/base_materials/pbr_alphatest_spherelized_normals_base.mgraph`
- **Graph type:** 1 (Mesh Alpha Test PBR)
- **Size:** 37 nodes, 42 links, 15 parameters

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
| `albedo` | Texture2D |  | `white.texture` |
| `shading` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `alpha_clip_threshold` | Slider | `0.5` |  |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `1` |  |
| `roughness` | Slider | `1` |  |
| `normal_scale` | Slider | `1` |  |
| `specular` | Slider | `1` |  |
| `microfiber` | Slider | `1` |  |
| `translucent` | Slider | `1` |  |
| `uv_transform` | Float4 | `1 1 0 0` |  |
| `spherelized_normals` | Group |  |  |
| `pivot` | Float3 | `0 0 1` |  |
| `spherelize_intensity` | Slider | `1` |  |

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
- **Opacity Clip Threshold** <- parameter `alpha_clip_threshold`
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
- **Normal Tangent Space** <- `lerp` (Lerp)
  - **A** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `normal`
    - **UV** <- subgraph `tiling and offset.msubgraph`
      - **UV** <- `Vertex UV 0`
      - **Tiling** <- expression `x,y`
        - **in** <- parameter `uv_transform`
      - **Offset** <- expression `z,w`
        - **in** <- parameter `uv_transform`
    - **Normal Intensity** <- parameter `normal_scale`
  - **B** <- `reorientNormalBlend` (Reorient Normal Blend)
    - **Base Normal** <- `RotateSpace` (Rotate Space)
      - **Object** <- `normalize` (Normalize)
        - **Vector** <- `_subtract` (Subtract)
          - **A** <- `Vertex Position`
          - **B** <- parameter `pivot`
    - **Detail Normal** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `normal`
      - **UV** <- subgraph `tiling and offset.msubgraph`
        - **UV** <- `Vertex UV 0`
        - **Tiling** <- expression `x,y`
          - **in** <- parameter `uv_transform`
        - **Offset** <- expression `z,w`
          - **in** <- parameter `uv_transform`
      - **Normal Intensity** <- parameter `normal_scale`
  - **Coefficient** <- parameter `spherelize_intensity`
- **Translucent** <- parameter `translucent`

## Node inventory

`Parameter` x14, `Expression` x7, `SampleTexture` x3, `_multiply` x3, `Final`, `Material`, `RotateSpace`, `SubGraph`, `Vertex Position`, `Vertex UV 0`, `_subtract`, `lerp`, `normalize`, `reorientNormalBlend`

## Subgraphs used

- `tiling and offset.msubgraph`

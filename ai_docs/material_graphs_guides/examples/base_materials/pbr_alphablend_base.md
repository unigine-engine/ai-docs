# pbr_alphablend_base

- **Source:** `showcase_content/materials/base_materials/pbr_alphablend_base.mgraph`
- **Graph type:** 2 (Mesh Transparent PBR)
- **Size:** 41 nodes, 48 links, 15 parameters

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
| `uv_transform` | Float4 | `1 1 0 0` |  |
| `ao_uv_transform` | Float4 | `1 1 0 0` |  |
| `opacity_fresnel` | Slider | `1` |  |
| `opacity_fresnel_pow` | Slider | `2` |  |

## What drives the Material node

- **Opacity** <- `lerp` (Lerp)
  - **A** <- expression `w`
    - **in** <- `_multiply` (Multiply)
      - **A** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `albedo`
        - **UV** <- subgraph `tiling and offset.msubgraph`
          - **UV** <- `Vertex UV 0`
          - **Tiling** <- expression `x,y`
            - ...
          - **Offset** <- expression `z,w`
            - ...
      - **B** <- parameter `albedo_color`
  - **B** <- `lerp` (Lerp)
    - **A** <- expression `w`
      - **in** <- `_multiply` (Multiply)
        - **A** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `albedo`
          - **UV** <- subgraph `tiling and offset.msubgraph`
            - ...
        - **B** <- parameter `albedo_color`
    - **B** <- `float`
    - **Coefficient** <- subgraph `fresnel.msubgraph`
      - **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `normal`
        - **UV** <- subgraph `tiling and offset.msubgraph`
          - **UV** <- `Vertex UV 0`
          - **Tiling** <- expression `x,y`
            - ...
          - **Offset** <- expression `z,w`
            - ...
        - **Normal Intensity** <- parameter `normal_scale`
      - **Power** <- parameter `opacity_fresnel_pow`
  - **Coefficient** <- parameter `opacity_fresnel`
- **Albedo** <- `_multiply` (Multiply)
  - **A** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `albedo`
    - **UV** <- subgraph `tiling and offset.msubgraph`
      - **UV** <- `Vertex UV 0`
      - **Tiling** <- expression `x,y`
        - **in** <- parameter `uv_transform`
      - **Offset** <- expression `z,w`
        - **in** <- parameter `uv_transform`
  - **B** <- parameter `albedo_color`
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

## Node inventory

`Parameter` x15, `Expression` x9, `SampleTexture` x4, `SubGraph` x3, `_multiply` x3, `Vertex UV 0` x2, `lerp` x2, `Final`, `Material`, `float`

## Subgraphs used

- `tiling and offset.msubgraph`
- `fresnel.msubgraph`

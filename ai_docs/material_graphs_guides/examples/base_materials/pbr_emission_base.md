# pbr_emission_base

- **Source:** `showcase_content/materials/base_materials/pbr_emission_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 36 nodes, 40 links, 14 parameters

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
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `1` |  |
| `roughness` | Slider | `1` |  |
| `normal_scale` | Slider | `1` |  |
| `specular` | Slider | `0.5` |  |
| `microfiber` | Slider | `0` |  |
| `translucent` | Slider | `0` |  |
| `emission` | Texture2D |  | `white.texture` |
| `emission_color` | Color | `1 1 1 1` |  |
| `emission_scale` | Slider | `1` |  |
| `uv_transform` | Float4 | `1 1 0 0` |  |

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
- **Emission** <- `_multiply` (Multiply)
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

`Parameter` x14, `Expression` x8, `_multiply` x5, `SampleTexture` x4, `Final`, `Material`, `SubGraph`, `Vertex UV 0`, `srgbInv`

## Subgraphs used

- `tiling and offset.msubgraph`

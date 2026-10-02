# pbr_parallax_depth_offset_base

- **Source:** `showcase_content/materials/base_materials/pbr_parallax_depth_offset_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 34 nodes, 37 links, 15 parameters

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
| `displacement` | Texture2D |  | `checker_d.texture` |
| `parallax_scale` | Slider | `1` |  |
| `parallax_min_layers` | Slider | `4` |  |
| `parallax_max_layers` | Slider | `16` |  |
| `shadow_normal_offset` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo`
      - **UV** <- subgraph `parallax occlusion mapping.msubgraph`
        - **Heightmap Texture 2D** <- parameter `displacement`
        - **Parallax Intensity (In Meters)** <- parameter `parallax_scale`
        - **Max Layers** <- parameter `parallax_max_layers`
        - **Min Layers** <- parameter `parallax_min_layers`
  - **B** <- expression `x,y,z`
    - **in** <- parameter `albedo_color`
- **Metalness** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
      - **UV** <- subgraph `parallax occlusion mapping.msubgraph`
        - **Heightmap Texture 2D** <- parameter `displacement`
        - **Parallax Intensity (In Meters)** <- parameter `parallax_scale`
        - **Max Layers** <- parameter `parallax_max_layers`
        - **Min Layers** <- parameter `parallax_min_layers`
  - **B** <- parameter `metalness`
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- expression `y`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
      - **UV** <- subgraph `parallax occlusion mapping.msubgraph`
        - **Heightmap Texture 2D** <- parameter `displacement`
        - **Parallax Intensity (In Meters)** <- parameter `parallax_scale`
        - **Max Layers** <- parameter `parallax_max_layers`
        - **Min Layers** <- parameter `parallax_min_layers`
  - **B** <- parameter `roughness`
- **Specular** <- parameter `specular`
- **Microfiber** <- parameter `microfiber`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
  - **UV** <- subgraph `parallax occlusion mapping.msubgraph`
    - **Heightmap Texture 2D** <- parameter `displacement`
    - **Parallax Intensity (In Meters)** <- parameter `parallax_scale`
    - **Max Layers** <- parameter `parallax_max_layers`
    - **Min Layers** <- parameter `parallax_min_layers`
  - **Normal Intensity** <- parameter `normal_scale`
- **Translucent** <- parameter `translucent`
- **Depth Offset** <- subgraph `parallax occlusion mapping.msubgraph`
  - **Heightmap Texture 2D** <- parameter `displacement`
  - **Parallax Intensity (In Meters)** <- parameter `parallax_scale`
  - **Max Layers** <- parameter `parallax_max_layers`
  - **Min Layers** <- parameter `parallax_min_layers`
- **Vertex Offset Tangent Space** <- `Branch`
  - **Condition** <- `Is Shadow Pass`
  - **True** <- `_multiply` (Multiply)
    - **A** <- `Vertex Normal`
    - **B** <- expression `-x,-x,-x`
      - **in** <- parameter `shadow_normal_offset`
  - **False** <- `float`

## Node inventory

`Parameter` x15, `Expression` x5, `_multiply` x4, `SampleTexture` x3, `Branch`, `Final`, `Is Shadow Pass`, `Material`, `SubGraph`, `Vertex Normal`, `float`

## Subgraphs used

- `parallax occlusion mapping.msubgraph`

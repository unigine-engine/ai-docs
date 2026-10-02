# tree_animation_base

- **Source:** `showcase_content/materials/base_materials/tree_animation_base.mgraph`
- **Graph type:** 1 (Mesh Alpha Test PBR)
- **Size:** 30 nodes, 32 links, 15 parameters

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
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `roughness` | Slider | `0.5` |  |
| `translucent` | Texture2D |  | `white.texture` |
| `translucent_intensity` | Slider | `1` |  |
| `Animation` | Group |  |  |
| `stem_speed` | Slider | `1` |  |
| `stem_wind_offset` | Slider | `0.5` |  |
| `branches_speed` | Slider | `1` |  |
| `branches_offset` | Slider | `0.5` |  |
| `leaves tiling` | Slider | `1` |  |
| `leaves speed` | Slider | `1` |  |
| `leaves offset` | Slider | `1` |  |
| `wind direction` | Float2 | `1 0` |  |
| `object height` | Slider | `5` |  |

## What drives the Material node

- **Opacity** <- expression `w`
  - **in** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `albedo`
- **Albedo** <- expression `x,y,z`
  - **in** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `albedo`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
- **Translucent** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `translucent`
  - **B** <- parameter `translucent_intensity`
- **Vertex Offset Tangent Space** <- subgraph `tree animation.msubgraph`
  - **Stem Speed** <- parameter `stem_speed`
  - **Stem Wind Offset** <- parameter `stem_wind_offset`
  - **Branches Speed** <- parameter `branches_speed`
  - **Branches Offset** <- `_multiply` (Multiply)
    - **A** <- expression `z`
      - **in** <- `Vertex Color`
    - **B** <- parameter `branches_offset`
  - **Leaves Tiling** <- parameter `leaves tiling`
  - **Leaves Speed** <- parameter `leaves speed`
  - **Leaves Offset** <- `_multiply` (Multiply)
    - **A** <- expression `x`
      - **in** <- `Vertex Color`
    - **B** <- parameter `leaves offset`
  - **Wind Direction** <- parameter `wind direction`
  - **Object Height** <- parameter `object height`
  - **Branches Time Offset (Sec)** <- expression `y`
    - **in** <- `Vertex Color`

## Node inventory

`Parameter` x14, `Expression` x6, `SampleTexture` x3, `_multiply` x3, `Final`, `Material`, `SubGraph`, `Vertex Color`

## Subgraphs used

- `tree animation.msubgraph`

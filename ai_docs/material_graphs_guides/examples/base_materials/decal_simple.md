# decal_simple

- **Source:** `showcase_content/materials/base_materials/decal_simple.mgraph`
- **Graph type:** 4 (Decal PBR)
- **Size:** 32 nodes, 34 links, 9 parameters

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
| `normal` | Texture2D |  | `normal.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `roughness` | Slider | `0.5` |  |
| `metalness` | Slider | `1` |  |
| `angle_fade_min` | Slider | `0` |  |
| `angle_fade_max` | Slider | `0.10000000149011612` |  |
| `shading` | Texture2D |  | `white.texture` |
| `normal_opacity` | Slider | `1` |  |

## What drives the Material node

- **Opacity** <- `_multiply` (Multiply)
  - **A** <- `saturate` (Saturate)
    - **Value** <- `rerange` (Rerange)
      - **In** <- `_dot_product` (Dot Product)
        - **A** <- `float3`
        - **B** <- `Decal Scene Normal`
      - **In Range Minimum** <- parameter `angle_fade_min`
      - **In Range Maximum** <- parameter `angle_fade_max`
      - **Out Range Minimum** <- `float`
      - **Out Range Maximum** <- `float`
  - **B** <- `_multiply` (Multiply)
    - **A** <- expression `w`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `albedo`
    - **B** <- expression `w`
      - **in** <- parameter `albedo_color`
- **Albedo** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo`
  - **B** <- expression `x,y,z`
    - **in** <- parameter `albedo_color`
- **Metalness** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
  - **B** <- parameter `metalness`
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- expression `y`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
  - **B** <- parameter `roughness`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
- **Opacity (Normal)** <- parameter `normal_opacity`

## Node inventory

`Parameter` x9, `Expression` x6, `_multiply` x5, `SampleTexture` x3, `float` x2, `Decal Scene Normal`, `Final`, `Material`, `_dot_product`, `float3`, `rerange`, `saturate`

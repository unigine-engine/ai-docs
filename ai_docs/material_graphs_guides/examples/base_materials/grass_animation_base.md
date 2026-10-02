# grass_animation_base

- **Source:** `showcase_content/materials/base_materials/grass_animation_base.mgraph`
- **Graph type:** 1 (Mesh Alpha Test PBR)
- **Size:** 63 nodes, 66 links, 21 parameters

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
| `albedo_2` | Texture2D |  | `white.texture` |
| `specular_normal` | Texture2D |  | `normal.texture` |
| `albedo_mask` | Texture2D |  | `white.texture` |
| `albedo_mask_tiling` | Slider | `1` |  |
| `albedo_color` | Color | `1 1 1 1` |  |
| `albedo_2_color` | Color | `1 1 1 1` |  |
| `specular` | Slider | `1` |  |
| `specular_normal_intensity` | Slider | `1` |  |
| `roughness` | Slider | `0.800000011920929` |  |
| `translucent` | Slider | `0.05000000074505829` |  |
| `Animation` | Group |  |  |
| `Wind Animation Tiling` | Slider | `2` |  |
| `Wind Animation Speed` | Slider | `1.5` |  |
| `Wind Animation Intensity` | Slider | `1` |  |
| `Wind DIrection` | Float2 | `1 0` |  |
| `Wind Bend Intensity` | Slider | `1` |  |
| `Object Height` | Slider | `0.10000000149011612` |  |
| `specular_by_distance` | Group |  |  |
| `distance_for_roughness` | Slider | `1` |  |
| `distance_for_specular` | Slider | `1` |  |

## What drives the Material node

- **Opacity** <- expression `w`
  - **in** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `albedo`
- **Albedo** <- `lerp` (Lerp)
  - **A** <- `_multiply` (Multiply)
    - **A** <- expression `x,y,z`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `albedo`
    - **B** <- expression `x,y,z`
      - **in** <- parameter `albedo_color`
  - **B** <- `_multiply` (Multiply)
    - **A** <- expression `x,y,z`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `albedo_2`
    - **B** <- expression `x,y,z`
      - **in** <- parameter `albedo_2_color`
  - **Coefficient** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo_mask`
      - **UV** <- `_multiply` (Multiply)
        - **A** <- expression `x,y`
          - **in** <- `Vertex Position`
        - **B** <- parameter `albedo_mask_tiling`
- **Roughness** <- `lerp` (Lerp)
  - **A** <- `lerp` (Lerp)
    - **A** <- `float`
    - **B** <- parameter `roughness`
    - **Coefficient** <- `rerange` (Rerange)
      - **In** <- `_dot_product` (Dot Product)
        - **A** <- expression `-x,-y,-z`
          - **in** <- `Sun Direction`
        - **B** <- `RotateSpace` (Rotate Space)
          - **Tangent** <- `SampleTexture` (SampleTexture: Default)
            - ...
      - **In Range Minimum** <- `float`
      - **In Range Maximum** <- `float`
      - **Out Range Minimum** <- `float`
      - **Out Range Maximum** <- `float`
  - **B** <- `float`
  - **Coefficient** <- `saturate` (Saturate)
    - **Value** <- `_divide` (Divide)
      - **A** <- subgraph `vertex depth.msubgraph`
      - **B** <- parameter `distance_for_specular`
- **Specular** <- `lerp` (Lerp)
  - **A** <- parameter `specular`
  - **B** <- `float`
  - **Coefficient** <- `saturate` (Saturate)
    - **Value** <- `_divide` (Divide)
      - **A** <- subgraph `vertex depth.msubgraph`
      - **B** <- parameter `distance_for_specular`
- **Normal Tangent Space** <- `lerp` (Lerp)
  - **A** <- subgraph `grass animation.msubgraph`
    - **Wind Animation Tiling** <- parameter `Wind Animation Tiling`
    - **Wind Animation Speed** <- parameter `Wind Animation Speed`
    - **Wind Animation Intensity** <- parameter `Wind Animation Intensity`
    - **Wind Direction** <- parameter `Wind DIrection`
    - **Wind Bend Intensity** <- parameter `Wind Bend Intensity`
    - **Normal Tangent Space** <- `RotateSpace` (Rotate Space)
      - **Object** <- `float3`
    - **Object Height (In Meters)** <- parameter `Object Height`
  - **B** <- `RotateSpace` (Rotate Space)
    - **Object** <- `float3`
  - **Coefficient** <- `saturate` (Saturate)
    - **Value** <- `_divide` (Divide)
      - **A** <- subgraph `vertex depth.msubgraph`
      - **B** <- parameter `distance_for_specular`
- **Translucent** <- parameter `translucent`
- **Vertex Offset Tangent Space** <- subgraph `grass animation.msubgraph`
  - **Wind Animation Tiling** <- parameter `Wind Animation Tiling`
  - **Wind Animation Speed** <- parameter `Wind Animation Speed`
  - **Wind Animation Intensity** <- parameter `Wind Animation Intensity`
  - **Wind Direction** <- parameter `Wind DIrection`
  - **Wind Bend Intensity** <- parameter `Wind Bend Intensity`
  - **Normal Tangent Space** <- `RotateSpace` (Rotate Space)
    - **Object** <- `float3`
  - **Object Height (In Meters)** <- parameter `Object Height`

## Node inventory

`Parameter` x19, `Expression` x8, `float` x8, `lerp` x6, `SampleTexture` x4, `RotateSpace` x3, `_multiply` x3, `SubGraph` x2, `float3` x2, `Final`, `Material`, `Sun Direction`, `Vertex Position`, `_divide`, `_dot_product`, `rerange`, `saturate`

## Subgraphs used

- `grass animation.msubgraph`
- `vertex depth.msubgraph`

# hair_base

This sample illustrates how to create hair or fur.

- **Sample:** Hair Shading Example
- **Source:** `art_samples/material_examples/hair_shading/materials/hair_base.mgraph`
- **Graph type:** 1 (Mesh Alpha Test PBR)
- **Size:** 53 nodes, 50 links, 14 parameters

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
| `depth_shadow` | False |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `opacity` | Texture2D |  | `white.texture` |
| `albedo` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `opacity_ramp` | TextureRamp R |  |  |
| `albedo_color` | Color | `1 1 1 1` |  |
| `translucent` | Slider | `1` |  |
| `anisotropy` | Slider | `1` |  |
| `specular` | Slider | `1` |  |
| `roughness_texture` | Texture2D |  | `white.texture` |
| `roughness_ramp` | TextureRamp R |  |  |
| `ambient_occlusion_texture` | Texture2D |  | `white.texture` |
| `depth_offset_parameters` | Group |  |  |
| `depth_offset` | Texture2D |  | `white.texture` |
| `depth_offset_intensity` | Slider | `1` |  |

## What drives the Material node

- **Opacity** <- subgraph `float_correction_by_ramp.msubgraph`
  - **Source Float** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `opacity`
  - **Texture Ramp R** <- parameter `opacity_ramp`
- **Opacity Clip Threshold** <- `frac` (Frac)
  - **Value** <- `_add` (Add)
    - **A** <- expression `x`
      - **in** <- subgraph `blue noise 256x256 animated.msubgraph`
        - **Number Of Frames** <- `int`
    - **B** <- `_multiply` (Multiply)
      - **A** <- `Golden Ratio`
      - **B** <- subgraph `vertex depth.msubgraph`
- **Albedo** <- `float`
- **Specular** <- `float`
- **Normal Tangent Space** <- portal Portal Out
- **Translucent** <- parameter `translucent`
- **Ambient Occlusion** <- `float`
- **Emission** <- subgraph `hair shading.msubgraph`
  - **Albedo** <- expression `x,y,z`
    - **in** <- `_multiply` (Multiply)
      - **A** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `albedo`
      - **B** <- parameter `albedo_color`
  - **Normal (Tangent Space)** <- portal Portal Out
  - **Diffuse Ambient Occlusion** <- portal Portal Out
  - **Specular Roughness** <- subgraph `float_correction_by_ramp.msubgraph`
    - **Source Float** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `roughness_texture`
    - **Texture Ramp R** <- parameter `roughness_ramp`
  - **Specular Intensity** <- parameter `specular`
  - **Specular Ambient Occlusion** <- portal Portal Out
  - **Anisotropy** <- parameter `anisotropy`
- **Depth Offset** <- `_multiply` (Multiply)
  - **A** <- `rerange` (Rerange)
    - **In** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `depth_offset`
    - **In Range Minimum** <- `float`
    - **In Range Maximum** <- `float`
    - **Out Range Minimum** <- `float`
    - **Out Range Maximum** <- `float`
  - **B** <- parameter `depth_offset_intensity`

## Node inventory

`Parameter` x13, `float` x7, `Expression` x6, `SampleTexture` x6, `SubGraph` x5, `PortalOut` x4, `_multiply` x3, `PortalIn` x2, `Final`, `Golden Ratio`, `Material`, `_add`, `frac`, `int`, `rerange`

## Subgraphs used

- `blue noise 256x256 animated.msubgraph`
- `hair shading.msubgraph`
- `vertex depth.msubgraph`
- `float_correction_by_ramp.msubgraph`

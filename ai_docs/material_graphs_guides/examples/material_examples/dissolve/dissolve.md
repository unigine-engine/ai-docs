# dissolve

This example demonstrates how to create an Alpha Test material with a dissolve effect.

- **Sample:** Dissolve Example
- **Source:** `art_samples/material_examples/dissolve/materials/dissolve.mgraph`
- **Graph type:** 1 (Mesh Alpha Test PBR)
- **Size:** 56 nodes, 54 links, 9 parameters

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
| `Albedo Color` | Color | `1 1 1 1` |  |
| `Dissolve` | Slider | `1` |  |
| `Border Color` | Color | `0.01568629965186119 1 0 1` |  |
| `Border Width` | Slider | `0.05000000074505832` |  |
| `Noise Scale` | Slider | `2` |  |
| `Emission Intensity` | Slider | `5` |  |
| `Albedo` | Texture2D |  | `white.texture` |
| `Normal` | Texture2D |  | `normal.texture` |
| `Shading` | Texture2D |  | `white.texture` |

## What drives the Material node

- **Opacity** <- `step` (Step)
  - **A** <- `rerange` (Rerange)
    - **In** <- portal Portal Out
    - **In Range Minimum** <- `float`
    - **In Range Maximum** <- `float`
    - **Out Range Minimum** <- `float`
    - **Out Range Maximum** <- expression `1+x`
      - **in** <- portal Portal Out
  - **B** <- `_add` (Add)
    - **A** <- portal Portal Out
    - **B** <- portal Portal Out
- **Opacity Clip Threshold** <- `float`
- **Albedo** <- `lerp` (Lerp)
  - **A** <- `float`
  - **B** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `Albedo`
      - **UV** <- `Vertex UV 0`
  - **Coefficient** <- portal Portal Out
- **Metalness** <- expression `x`
  - **in** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `Shading`
    - **UV** <- `Vertex UV 0`
- **Roughness** <- expression `y`
  - **in** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `Shading`
    - **UV** <- `Vertex UV 0`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Normal`
  - **UV** <- `Vertex UV 0`
- **Emission** <- `_multiply` (Multiply)
  - **A** <- `_multiply` (Multiply)
    - **A** <- `srgbInv` (Srgb Inverse)
      - **Color** <- expression `x,y,z`
        - **in** <- parameter `Border Color`
    - **B** <- expression `1-x`
      - **in** <- portal Portal Out
  - **B** <- parameter `Emission Intensity`

## Node inventory

`Expression` x8, `Parameter` x8, `float` x8, `PortalOut` x7, `PortalIn` x4, `SampleTexture` x4, `Vertex UV 0` x4, `_multiply` x3, `rerange` x2, `step` x2, `Final`, `Material`, `Texture2D`, `_add`, `lerp`, `srgbInv`

# melting_base

This example demonstrates how to create an effect of a melting geometry.

- **Sample:** Melting Example
- **Source:** `art_samples/material_examples/melting/materials/melting_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 93 nodes, 92 links, 15 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 2 (Tangent) |
| `vertex_mode` | 0 (Position) |
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
| `roughness_map` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `1` |  |
| `roughness_intensity` | Slider | `1` |  |
| `Melting` | Group |  |  |
| `melting_level` | Slider | `0.5` |  |
| `3D_noise` | Texture3D |  | `noise_smooth_vector_128_3d.texture` |
| `3D_noise_tiling` | Slider | `0.15000000596046498` |  |
| `temperature_color` | Slider | `3000` |  |
| `emission_intensity` | Slider | `4` |  |
| `melting_gradient_length` | Slider | `0.40000000596046575` |  |
| `noise_displacement` | Slider | `0.6999999880790748` |  |
| `extrude_by_normals` | Slider | `0.20000000298023224` |  |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- `_multiply` (Multiply)
    - **A** <- expression `x,y,z`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `albedo`
    - **B** <- expression `x,y,z`
      - **in** <- parameter `albedo_color`
  - **B** <- `float`
  - **Coefficient** <- portal Portal Out
- **Metalness** <- parameter `metalness`
- **Roughness** <- `lerp` (Lerp)
  - **A** <- `_multiply` (Multiply)
    - **A** <- subgraph `contrast.msubgraph`
      - **Value** <- expression `x`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `roughness_map`
          - **UV** <- `_multiply` (Multiply)
            - ...
      - **Contrast (From -1 to 1)** <- `float`
    - **B** <- parameter `roughness_intensity`
  - **B** <- `float`
  - **Coefficient** <- portal Portal Out
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
  - **Normal Intensity** <- `float`
- **Emission** <- `_multiply` (Multiply)
  - **A** <- `srgbInv` (Srgb Inverse)
    - **Color** <- `_multiply` (Multiply)
      - **A** <- subgraph `blackbody.msubgraph`
        - **Temperature** <- `_multiply` (Multiply)
          - **A** <- portal Portal Out
          - **B** <- parameter `temperature_color`
      - **B** <- portal Portal Out
  - **B** <- parameter `emission_intensity`
- **Vertex Position Object Space** <- `_add` (Add)
  - **A** <- `_compose_float3` (Compose Float3)
    - **X** <- expression `x`
      - **in** <- portal Portal Out
    - **Y** <- expression `y`
      - **in** <- portal Portal Out
    - **Z** <- `clamp` (Clamp)
      - **Value** <- expression `z`
        - **in** <- portal Portal Out
      - **Minimum** <- `float`
      - **Maximum** <- portal Portal Out
  - **B** <- `_multiply` (Multiply)
    - **A** <- `Vertex Normal`
    - **B** <- `lerp` (Lerp)
      - **A** <- `_multiply` (Multiply)
        - **A** <- portal Portal Out
        - **B** <- parameter `extrude_by_normals`
      - **B** <- `float`
      - **Coefficient** <- `saturate` (Saturate)
        - **Value** <- expression `z`
          - **in** <- portal Portal Out

## Node inventory

`Parameter` x16, `float` x15, `PortalOut` x11, `Expression` x10, `_multiply` x10, `SampleTexture` x4, `lerp` x4, `PortalIn` x3, `_add` x3, `saturate` x3, `SubGraph` x2, `rerange` x2, `Final`, `Material`, `Vertex Normal`, `Vertex Position`, `Vertex UV 0`, `_compose_float3`, `_subtract`, `clamp`, `pow`, `srgbInv`

## Subgraphs used

- `contrast.msubgraph`
- `blackbody.msubgraph`

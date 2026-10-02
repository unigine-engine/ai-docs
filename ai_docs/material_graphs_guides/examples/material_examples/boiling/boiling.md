# boiling

This example demonstrates creation of a complex effect of boiling liquid featuring tessellation and vertex offset control.

- **Sample:** Boiling Example
- **Source:** `art_samples/material_examples/boiling/materials/boiling.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 117 nodes, 116 links, 15 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 1 (Object) |
| `vertex_mode` | 1 (Offset) |
| `two_sided` | False |
| `tessellation` | True |
| `depth_test` | True |
| `blend_mode` | 0 |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo_color_0` | Color | `1 1 1 1` |  |
| `albedo_color_2` | Color | `0.29803898930549777 0.4392159879207628 0.239215999841691 1` |  |
| `roughness` | Slider | `0.5` |  |
| `3d_noise_tiling` | Slider | `0.40000000596046575` |  |
| `Bubbles` | Group |  |  |
| `bubbles_cones` | Texture2D |  | `white.texture` |
| `bubbles_offset` | Texture2D |  | `white.texture` |
| `bubbles_mask` | Texture2D |  | `white.texture` |
| `bubbles_emission_color` | Color | `1 1 1 1` |  |
| `bubbles_height` | Slider | `0.05999999865889568` |  |
| `bubbles_tiling` | Slider | `1` |  |
| `animation_speed` | Slider | `1` |  |
| `tessellation` | Group |  |  |
| `tessellation_factor_map` | Texture2D |  | `white.texture` |
| `tessellation_factor` | Slider | `0.25` |  |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- expression `x,y,z`
    - **in** <- `lerp` (Lerp)
      - **A** <- parameter `albedo_color_2`
      - **B** <- parameter `albedo_color_0`
      - **Coefficient** <- `lerp` (Lerp)
        - **A** <- `float`
        - **B** <- `float`
        - **Coefficient** <- subgraph `fresnel.msubgraph`
          - **Normal Tangent Space** <- portal Portal Out
          - **Power** <- `float`
  - **B** <- expression `x,y,z`
    - **in** <- parameter `albedo_color_2`
  - **Coefficient** <- `saturate` (Saturate)
    - **Value** <- `_add` (Add)
      - **A** <- `_multiply` (Multiply)
        - **A** <- `length` (Length)
          - **Vector** <- expression `x,y,z`
            - ...
        - **B** <- `float`
      - **B** <- portal Portal Out
- **Roughness** <- parameter `roughness`
- **Specular** <- `float`
- **Normal Tangent Space** <- portal Portal Out
- **Translucent** <- `float`
- **Emission** <- `_multiply` (Multiply)
  - **A** <- `pow` (Power)
    - **Value** <- portal Portal Out
    - **Power** <- `float`
  - **B** <- `srgbInv` (Srgb Inverse)
    - **Color** <- parameter `bubbles_emission_color`
- **Tessellation Factor** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `tessellation_factor_map`
      - **UV** <- portal Portal Out
  - **B** <- parameter `tessellation_factor`
- **Tessellation Vertex Offset Object Space** <- portal Portal Out

## Node inventory

`float` x18, `PortalOut` x15, `Parameter` x14, `Expression` x13, `_multiply` x13, `PortalIn` x5, `SampleTexture` x5, `_add` x4, `lerp` x4, `SubGraph` x3, `_subtract` x3, `RotateSpace` x2, `Time` x2, `saturate` x2, `Final`, `Material`, `Texture3D`, `Vertex Position`, `Vertex UV 0`, `_divide`, `_greater`, `frac`, `length`, `normalReconstructZ`, `pow`, `rerange`, `smoothstep`, `srgbInv`

## Subgraphs used

- `normal from height value.msubgraph`
- `fresnel.msubgraph`

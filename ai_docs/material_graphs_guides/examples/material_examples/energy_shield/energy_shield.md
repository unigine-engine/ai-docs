# energy_shield

This example demonstrates how to implement an effect of an animated energy shield.

- **Sample:** Energy Shield Example
- **Source:** `art_samples/material_examples/energy_shield/materials/energy_shield.mgraph`
- **Graph type:** 3 (Mesh Transparent Unlit)
- **Size:** 143 nodes, 142 links, 7 parameters

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
| `Intersection Power` | Slider | `8` |  |
| `Fresnel Power` | Slider | `3` |  |
| `Emission Color 1` | Color | `0.21960799396038094 0.49411800503730885 1 1` |  |
| `Emission Color 2` | Color | `0.784313976764679 0.34509798884391873 1 1` |  |
| `Emission Intensity` | Slider | `8` |  |
| `Time Speed` | Slider | `0.3000000119209299` |  |
| `Opacity` | Slider | `1` |  |

## What drives the Material node

- **Opacity** <- `saturate` (Saturate)
  - **Value** <- `_multiply` (Multiply)
    - **A** <- portal Portal Out
    - **B** <- parameter `Opacity`
- **Color** <- `_multiply` (Multiply)
  - **A** <- `_multiply` (Multiply)
    - **A** <- portal Portal Out
    - **B** <- `lerp` (Lerp)
      - **A** <- expression `x,y,z`
        - **in** <- `srgbInv` (Srgb Inverse)
          - **Color** <- parameter `Emission Color 1`
      - **B** <- expression `x,y,z`
        - **in** <- `srgbInv` (Srgb Inverse)
          - **Color** <- parameter `Emission Color 2`
      - **Coefficient** <- portal Portal Out
  - **B** <- parameter `Emission Intensity`
- **Vertex Offset Tangent Space** <- `_multiply` (Multiply)
  - **A** <- `Vertex Normal`
  - **B** <- `rerange` (Rerange)
    - **In** <- portal Portal Out
    - **In Range Minimum** <- `float`
    - **In Range Maximum** <- `float`
    - **Out Range Minimum** <- `float`
    - **Out Range Maximum** <- `float`

## Node inventory

`float` x25, `_multiply` x21, `Expression` x15, `PortalOut` x12, `pow` x9, `PortalIn` x8, `Parameter` x7, `saturate` x7, `SampleTexture` x4, `_add` x4, `_subtract` x4, `Texture2D` x3, `Vertex UV 0` x3, `Vertex Normal` x2, `_compose_float2` x2, `length` x2, `lerp` x2, `srgbInv` x2, `Depth Opacity`, `Final`, `Material`, `Screen UV`, `Time`, `Vertex Position`, `View Direction`, `_dot_product`, `max`, `rerange`, `sin`

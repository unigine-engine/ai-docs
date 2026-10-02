# glass_blend_mode_refraction_thin

This example demonstrates different implementations of glass materials for different needs.

- **Sample:** Glass Example
- **Source:** `art_samples/material_examples/glass/materials/glass_blend_mode_refraction_thin.mgraph`
- **Graph type:** 3 (Mesh Transparent Unlit)
- **Size:** 21 nodes, 18 links, 11 parameters

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
| `blend_mode` | 2 |
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
| `normal_intensity` | Slider | `1` |  |
| `translucent_roughness` | Slider | `1` |  |
| `translucent_fresnel_power` | Slider | `1` |  |
| `fake_refraction` | Slider | `1` |  |
| `opacity` | Slider | `1` |  |
| `ior` | Slider | `1` |  |
| `step_size` | Slider | `0.10000000149011612` |  |

## What drives the Material node

- **Color** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- parameter `albedo_color`
  - **B** <- expression `1-x`
    - **in** <- subgraph `fresnel.msubgraph`
      - **Normal Tangent Space** <- portal Portal Out
      - **Power** <- parameter `translucent_fresnel_power`
- **Refraction Screen UV Offset** <- subgraph `refraction screen uv offset for thin objects.msubgraph`
  - **Fake Refraction Intensity** <- parameter `fake_refraction`
  - **Normal Tangent Space** <- portal Portal Out

## Node inventory

`Parameter` x7, `PortalOut` x3, `SubGraph` x3, `Expression` x2, `Final`, `Material`, `PortalIn`, `SampleTexture`, `_multiply`, `float`

## Subgraphs used

- `fresnel.msubgraph`
- `refraction screen uv offset for thin objects.msubgraph`
- `refraction raymarched.msubgraph`

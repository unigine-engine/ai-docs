# glass_blend_mode_refraction_thick

This example demonstrates different implementations of glass materials for different needs.

- **Sample:** Glass Example
- **Source:** `art_samples/material_examples/glass/materials/glass_blend_mode_refraction_thick.mgraph`
- **Graph type:** 3 (Mesh Transparent Unlit)
- **Size:** 19 nodes, 17 links, 10 parameters

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
| `blend_mode` | 2 |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `translucent_color` | Color | `1 1 1 1` |  |
| `roughness` | Slider | `0.5` |  |
| `normal_intensity` | Slider | `1` |  |
| `translucent_roughness` | Slider | `0` |  |
| `translucent_fresnel_power` | Slider | `1` |  |
| `index_of_refraction` | Slider | `1.5499999523162846` |  |
| `last_step` | Slider | `0.10000000149011612` |  |
| `last_step_size` | Slider | `100000` |  |

## What drives the Material node

- **Color** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- parameter `translucent_color`
  - **B** <- expression `1-x`
    - **in** <- subgraph `fresnel.msubgraph`
      - **Normal Tangent Space** <- portal Portal Out
      - **Power** <- parameter `translucent_fresnel_power`
- **Refraction Screen UV Offset** <- subgraph `refraction raymarched.msubgraph`
  - **Step Size** <- parameter `last_step`
  - **Translucence Roughness** <- parameter `translucent_roughness`
  - **Last Step Size** <- parameter `last_step_size`
  - **IOR** <- parameter `index_of_refraction`
  - **Normal Tangent Space** <- portal Portal Out

## Node inventory

`Parameter` x8, `Expression` x2, `PortalOut` x2, `SubGraph` x2, `Final`, `Material`, `PortalIn`, `SampleTexture`, `_multiply`

## Subgraphs used

- `fresnel.msubgraph`
- `refraction raymarched.msubgraph`

# glass_thick_colored_low_quality

This example demonstrates different implementations of glass materials for different needs.

- **Sample:** Glass Example
- **Source:** `art_samples/material_examples/glass/materials/glass_thick_colored_low_quality.mgraph`
- **Graph type:** 2 (Mesh Transparent PBR)
- **Size:** 21 nodes, 19 links, 8 parameters

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
| `normal` | Texture2D |  | `normal.texture` |
| `translucence_color` | Color | `1 1 1 1` |  |
| `translucence_fresnel_power` | Slider | `1` |  |
| `roughness` | Slider | `0` |  |
| `normal_intensity` | Slider | `1` |  |
| `index_of_refraction` | Slider | `1.5499999523162846` |  |
| `ray_length_refraction` | Slider | `10` |  |
| `translucence_roughness` | Slider | `0` |  |

## What drives the Material node

- **Albedo** <- `float`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- portal Portal Out
- **Emission** <- `_multiply` (Multiply)
  - **A** <- subgraph `refraction simple for thick objects.msubgraph`
    - **Translucence Color** <- expression `x,y,z`
      - **in** <- parameter `translucence_color`
    - **IOR** <- parameter `index_of_refraction`
    - **Translucence Roughness** <- parameter `translucence_roughness`
    - **Ray Length** <- parameter `ray_length_refraction`
    - **Normal Tangent Space** <- portal Portal Out
  - **B** <- expression `1-x`
    - **in** <- subgraph `fresnel.msubgraph`
      - **Normal Tangent Space** <- portal Portal Out
      - **Power** <- parameter `translucence_fresnel_power`

## Node inventory

`Parameter` x8, `PortalOut` x3, `Expression` x2, `SubGraph` x2, `Final`, `Material`, `PortalIn`, `SampleTexture`, `_multiply`, `float`

## Subgraphs used

- `refraction simple for thick objects.msubgraph`
- `fresnel.msubgraph`

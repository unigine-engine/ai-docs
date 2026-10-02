# glass_blend_mode_add

This example demonstrates different implementations of glass materials for different needs.

- **Sample:** Glass Example
- **Source:** `art_samples/material_examples/glass/materials/glass_blend_mode_add.mgraph`
- **Graph type:** 2 (Mesh Transparent PBR)
- **Size:** 22 nodes, 22 links, 11 parameters

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
| `blend_mode` | 1 |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `roughness` | Slider | `0` |  |
| `normal_intensity` | Slider | `1` |  |
| `translucent_roughness` | Slider | `1` |  |
| `Fake Refraction` | Slider | `1` |  |
| `opacity` | Slider | `1` |  |
| `step_size` | Slider | `0.05000000074505832` |  |
| `threshold` | Slider | `0.20000000298023224` |  |
| `last_step_size` | Slider | `100000` |  |

## What drives the Material node

- **Albedo** <- `float`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- portal Portal Out
- **Ambient Occlusion** <- expression `1-x`
  - **in** <- subgraph `reflection raymarched.msubgraph`
    - **Step Size** <- parameter `step_size`
    - **Last Step Size** <- parameter `last_step_size`
    - **Threshold** <- parameter `threshold`
    - **Roughness** <- parameter `roughness`
    - **Normal Tangent Space** <- portal Portal Out
- **Emission** <- expression `x,y,z`
  - **in** <- `_multiply` (Multiply)
    - **A** <- `_multiply` (Multiply)
      - **A** <- subgraph `reflection raymarched.msubgraph`
        - **Step Size** <- parameter `step_size`
        - **Last Step Size** <- parameter `last_step_size`
        - **Threshold** <- parameter `threshold`
        - **Roughness** <- parameter `roughness`
        - **Normal Tangent Space** <- portal Portal Out
      - **B** <- subgraph `reflection raymarched.msubgraph`
        - **Step Size** <- parameter `step_size`
        - **Last Step Size** <- parameter `last_step_size`
        - **Threshold** <- parameter `threshold`
        - **Roughness** <- parameter `roughness`
        - **Normal Tangent Space** <- portal Portal Out
    - **B** <- subgraph `fresnel pbr.msubgraph`
      - **Roughness** <- parameter `roughness`
      - **Normal Tangent Space** <- portal Portal Out

## Node inventory

`Parameter` x8, `PortalOut` x3, `Expression` x2, `SubGraph` x2, `_multiply` x2, `Final`, `Material`, `PortalIn`, `SampleTexture`, `float`

## Subgraphs used

- `reflection raymarched.msubgraph`
- `fresnel pbr.msubgraph`

# clear_coat_base

This example illustrates how to create materials having two physical layers such as car paint, carbon, metal, or wood covered with varnish.

- **Sample:** Clear Coat Example
- **Source:** `art_samples/material_examples/clear_coat/materials/clear_coat_base.mgraph`
- **Graph type:** 2 (Mesh Transparent PBR)
- **Size:** 30 nodes, 29 links, 10 parameters

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
| `blend_mode` | 0 |
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
| `step_size` | Slider | `0.10000000149011612` |  |
| `last_step_size` | Slider | `0` |  |
| `geometry_inflation` | Slider | `0.0010000000474974576` |  |
| `threshold` | Slider | `1` |  |
| `screen_perimeter_softness` | Slider | `0.25` |  |

## What drives the Material node

- **Albedo** <- `float`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- portal Portal Out
- **Ambient Occlusion** <- expression `1-x`
  - **in** <- subgraph `reflection raymarched.msubgraph`
    - **Step Size** <- parameter `step_size`
    - **Last Step Size** <- parameter `last_step_size`
    - **Threshold** <- parameter `threshold`
    - **Screen Perimeter Softness** <- parameter `screen_perimeter_softness`
    - **Roughness** <- parameter `roughness`
    - **Normal Tangent Space** <- portal Portal Out
- **Emission** <- `lerp` (Lerp)
  - **A** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- `Screen Color Opacity` (Texture Buffer Screen Color Opacity)
      - **UV** <- `Screen UV`
  - **B** <- subgraph `reflection raymarched.msubgraph`
    - **Step Size** <- parameter `step_size`
    - **Last Step Size** <- parameter `last_step_size`
    - **Threshold** <- parameter `threshold`
    - **Screen Perimeter Softness** <- parameter `screen_perimeter_softness`
    - **Roughness** <- parameter `roughness`
    - **Normal Tangent Space** <- portal Portal Out
  - **Coefficient** <- `lerp` (Lerp)
    - **A** <- `float`
    - **B** <- `float`
    - **Coefficient** <- subgraph `fresnel.msubgraph`
      - **Normal Tangent Space** <- portal Portal Out
      - **Power** <- `float`
- **Vertex Offset Tangent Space** <- expression `0,0,x`
  - **in** <- parameter `geometry_inflation`

## Node inventory

`Parameter` x9, `float` x4, `Expression` x3, `PortalOut` x3, `SampleTexture` x2, `SubGraph` x2, `lerp` x2, `Final`, `Material`, `PortalIn`, `Screen Color Opacity`, `Screen UV`

## Subgraphs used

- `fresnel.msubgraph`
- `reflection raymarched.msubgraph`

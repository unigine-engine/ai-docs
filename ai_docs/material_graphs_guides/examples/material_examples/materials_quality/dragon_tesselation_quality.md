# dragon_tesselation_quality

This example illustrates the Materials Quality feature enabling you to apply a certain set of features inside graph-based materials connected to the corresponding input of a Material Quality Switch node depending on the quality level selected globally.

- **Sample:** Materials Quality Example
- **Source:** `art_samples/material_examples/materials_quality/materials/dragon_tesselation_quality.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 27 nodes, 26 links, 3 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 2 (Tangent) |
| `vertex_mode` | 1 (Offset) |
| `two_sided` | False |
| `tessellation` | True |
| `depth_test` | True |
| `blend_mode` | 0 |
| `cast_gi` | False |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `height` | Texture2D |  | `black.texture` |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `albedo`
- **Metalness** <- `float`
- **Roughness** <- `float`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
- **Tessellation Factor** <- `MaterialQualitySwitch` (Material Quality Switch)
  - **Low** <- `float`
  - **Medium** <- `float`
  - **High** <- `float`
- **Tessellation Vertex Offset Tangent Space** <- expression `0,0,x`
  - **in** <- `_multiply` (Multiply)
    - **A** <- `rerange` (Rerange)
      - **In** <- expression `x`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `height`
      - **In Range Minimum** <- `float`
      - **In Range Maximum** <- `float`
      - **Out Range Minimum** <- `float`
      - **Out Range Maximum** <- `float`
    - **B** <- `MaterialQualitySwitch` (Material Quality Switch)
      - **Low** <- `float`
      - **Medium** <- `float`
      - **High** <- `float`

## Node inventory

`float` x12, `Expression` x3, `Parameter` x3, `SampleTexture` x3, `MaterialQualitySwitch` x2, `Final`, `Material`, `_multiply`, `rerange`

# normal_from_height_value

This example demonstrates how to convert height values to normal vectors.

- **Sample:** Normal From Height Value Example
- **Source:** `art_samples/material_examples/normal_from_height_value/materials/normal_from_height_value.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 34 nodes, 34 links, 4 parameters

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
| `albedo color` | Color | `1 1 1 1` |  |
| `normal` | Texture2D |  | `normal.texture` |
| `Coverage` | Slider | `0.15000000596046498` |  |
| `Contrast` | Slider | `0.8999999761581469` |  |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- parameter `albedo color`
- **Normal Tangent Space** <- `reorientNormalBlend` (Reorient Normal Blend)
  - **Base Normal** <- subgraph `normal from height value.msubgraph`
    - **Height Value** <- portal Portal Out
  - **Detail Normal** <- `lerp` (Lerp)
    - **A** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- `Texture2D`
      - **UV** <- `Vertex UV 0`
    - **B** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- `Texture2D`
      - **UV** <- `Vertex UV 0`
      - **Normal Intensity** <- `float`
    - **Coefficient** <- portal Portal Out

## Node inventory

`float` x6, `Expression` x3, `Parameter` x3, `SampleTexture` x3, `Texture2D` x3, `Vertex UV 0` x3, `PortalOut` x2, `SubGraph` x2, `Final`, `Material`, `PortalIn`, `_add`, `_multiply`, `lerp`, `reorientNormalBlend`, `rerange`, `smoothstep`

## Subgraphs used

- `normal from height value.msubgraph`
- `contrast.msubgraph`

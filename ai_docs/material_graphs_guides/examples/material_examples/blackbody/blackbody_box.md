# blackbody_box

This example demonstrates how to implement simulation of blackbody radiation for physically accurate emissive materials.

- **Sample:** Blackbody Example
- **Source:** `art_samples/material_examples/blackbody/materials/blackbody_box.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 19 nodes, 20 links, 1 parameters

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
| `Temperature` | Slider | `20000` |  |

## What drives the Material node

- **Albedo** <- `float`
- **Specular** <- `float`
- **Emission** <- `srgbInv` (Srgb Inverse)
  - **Color** <- `_multiply` (Multiply)
    - **A** <- subgraph `blackbody.msubgraph`
      - **Temperature** <- `_multiply` (Multiply)
        - **A** <- expression `x`
          - **in** <- `Vertex UV 0`
        - **B** <- parameter `Temperature`
    - **B** <- `saturate` (Saturate)
      - **Value** <- `_multiply` (Multiply)
        - **A** <- expression `x`
          - **in** <- `Vertex UV 0`
        - **B** <- `rerange` (Rerange)
          - **In** <- parameter `Temperature`
          - **In Range Minimum** <- `float`
          - **In Range Maximum** <- `float`
          - **Out Range Minimum** <- `float`
          - **Out Range Maximum** <- `float`

## Node inventory

`float` x6, `_multiply` x3, `Expression` x2, `Final`, `Material`, `Parameter`, `SubGraph`, `Vertex UV 0`, `rerange`, `saturate`, `srgbInv`

## Subgraphs used

- `blackbody.msubgraph`

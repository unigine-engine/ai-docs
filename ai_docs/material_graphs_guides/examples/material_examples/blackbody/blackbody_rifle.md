# blackbody_rifle

This example demonstrates how to implement simulation of blackbody radiation for physically accurate emissive materials.

- **Sample:** Blackbody Example
- **Source:** `art_samples/material_examples/blackbody/materials/blackbody_rifle.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 33 nodes, 35 links, 8 parameters

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
| `albedo` | Texture2D |  | `white.texture` |
| `shading` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `white.texture` |
| `albedo color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `1` |  |
| `roughness` | Slider | `1` |  |
| `contrast` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- `_multiply` (Multiply)
  - **A** <- expression `x,y,z`
    - **in** <- parameter `albedo color`
  - **B** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo`
- **Metalness** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
  - **B** <- parameter `metalness`
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- expression `y`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `shading`
  - **B** <- parameter `roughness`
- **Specular** <- `float`
- **Emission** <- `srgbInv` (Srgb Inverse)
  - **Color** <- `_multiply` (Multiply)
    - **A** <- subgraph `blackbody.msubgraph`
      - **Temperature** <- `_multiply` (Multiply)
        - **A** <- subgraph `contrast.msubgraph`
          - **Value** <- expression `y`
            - ...
          - **Contrast (From -1 to 1)** <- parameter `contrast`
        - **B** <- parameter `Temperature`
    - **B** <- `saturate` (Saturate)
      - **Value** <- `_multiply` (Multiply)
        - **A** <- subgraph `contrast.msubgraph`
          - **Value** <- expression `y`
            - ...
          - **Contrast (From -1 to 1)** <- parameter `contrast`
        - **B** <- `rerange` (Rerange)
          - **In** <- parameter `Temperature`
          - **In Range Minimum** <- `float`
          - **In Range Maximum** <- `float`
          - **Out Range Minimum** <- `float`
          - **Out Range Maximum** <- `float`

## Node inventory

`Parameter` x7, `_multiply` x6, `Expression` x5, `float` x5, `SampleTexture` x2, `SubGraph` x2, `Final`, `Material`, `Vertex Position`, `rerange`, `saturate`, `srgbInv`

## Subgraphs used

- `blackbody.msubgraph`
- `contrast.msubgraph`

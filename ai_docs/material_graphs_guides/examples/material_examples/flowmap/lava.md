# lava

Using the Flowmap Panner node to create a lava flow.

- **Sample:** Flowmap
- **Source:** `art_samples/material_examples/flowmap/materials/lava.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 88 nodes, 86 links, 18 parameters

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
| `emission_mask` | Texture2D |  | `white.texture` |
| `roughness` | Slider | `0.5` |  |
| `tiling` | Float2 | `1 1` |  |
| `temperature` | Slider | `1` |  |
| `temperature_spread` | Slider | `1` |  |
| `speed` | Slider | `0.7500000000000014` |  |
| `height` | Texture2D |  | `black.texture` |
| `height_scale` | Slider | `1` |  |
| `coast_displacement` | Slider | `1` |  |
| `flowmap_strength` | Slider | `0.5` |  |
| `normal_intensity` | Slider | `1` |  |
| `transition` | Slider | `1` |  |
| `refraction` | Slider | `1` |  |
| `depth_border` | Slider | `1` |  |
| `depth_border_intensity` | Slider | `1` |  |
| `phase_2_offset` | Float2 | `1 1` |  |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- subgraph `flowmap_panner.msubgraph`
    - **Source Texture** <- parameter `albedo`
    - **FlowMap Texture (0-1)** <- `Surface Custom Texture`
    - **Source Tiling** <- parameter `tiling`
    - **FlowMap UV** <- `Vertex UV 1`
    - **Phase 2 UV Offset** <- parameter `phase_2_offset`
    - **Speed** <- parameter `speed`
    - **Strength** <- parameter `flowmap_strength`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- portal Portal Out
- **Emission** <- `srgbInv` (Srgb Inverse)
  - **Color** <- `_multiply` (Multiply)
    - **A** <- subgraph `blackbody.msubgraph`
      - **Temperature** <- `_multiply` (Multiply)
        - **A** <- `saturate` (Saturate)
          - **Value** <- `_multiply` (Multiply)
            - ...
        - **B** <- parameter `temperature`
    - **B** <- `saturate` (Saturate)
      - **Value** <- `_multiply` (Multiply)
        - **A** <- `saturate` (Saturate)
          - **Value** <- `_multiply` (Multiply)
            - ...
        - **B** <- `rerange` (Rerange)
          - **In** <- parameter `temperature`
          - **In Range Minimum** <- `float`
          - **In Range Maximum** <- `float`
          - **Out Range Minimum** <- `float`
          - **Out Range Maximum** <- `float`
- **Tessellation Vertex Offset Tangent Space** <- expression `0,0,x`
  - **in** <- `_multiply` (Multiply)
    - **A** <- `_multiply` (Multiply)
      - **A** <- expression `x`
        - **in** <- subgraph `flowmap_panner.msubgraph`
          - **Source Texture** <- parameter `height`
          - **FlowMap Texture (0-1)** <- `Surface Custom Texture`
          - **Source Tiling** <- parameter `tiling`
          - **FlowMap UV** <- `Vertex UV 1`
          - **Phase 2 UV Offset** <- parameter `phase_2_offset`
          - **Speed** <- parameter `speed`
          - **Strength** <- parameter `flowmap_strength`
      - **B** <- parameter `height_scale`
    - **B** <- `_multiply` (Multiply)
      - **A** <- `saturate` (Saturate)
        - **Value** <- `_multiply` (Multiply)
          - **A** <- expression `z`
            - ...
          - **B** <- parameter (float)
      - **B** <- parameter `coast_displacement`

## Node inventory

`Parameter` x29, `_multiply` x10, `Expression` x8, `float` x8, `Surface Custom Texture` x6, `Vertex UV 1` x6, `SubGraph` x5, `saturate` x4, `SampleTexture` x3, `PortalOut` x2, `rerange` x2, `Final`, `Material`, `PortalIn`, `length`, `srgbInv`

## Subgraphs used

- `flowmap_panner.msubgraph`
- `blackbody.msubgraph`

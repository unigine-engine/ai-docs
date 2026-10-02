# river_water

Using the Flowmap Panner node to create rivers, and vortexes.

- **Sample:** Flowmap River and Vortex Example
- **Source:** `art_samples/material_examples/flowmap_river_and_vortex/materials/river_water.mgraph`
- **Graph type:** 2 (Mesh Transparent PBR)
- **Size:** 120 nodes, 126 links, 16 parameters

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
| `shallow_color` | Color | `1 1 1 1` |  |
| `deep_color` | Color | `1 1 1 1` |  |
| `roughness` | Slider | `0.5` |  |
| `tiling` | Float2 | `1 1` |  |
| `speed` | Slider | `0.7500000000000014` |  |
| `height` | Texture2D |  | `black.texture` |
| `height_scale` | Slider | `1` |  |
| `flowmap_strength` | Slider | `0.5` |  |
| `normal_intensity` | Slider | `1` |  |
| `transition` | Slider | `1` |  |
| `refraction` | Slider | `1` |  |
| `depth_border` | Slider | `1` |  |
| `depth_border_intensity` | Slider | `1` |  |
| `coast_waves` | Slider | `1` |  |

## What drives the Material node

- **Opacity** <- subgraph `depth fade.msubgraph`
  - **Fade Distance (In Meters)** <- parameter `transition`
- **Albedo** <- `float`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- portal Portal Out
- **Ambient Occlusion** <- expression `1-x`
  - **in** <- subgraph `reflection raymarched.msubgraph`
    - **Step Size** <- parameter (float)
    - **Last Step Size** <- parameter (float)
    - **Threshold** <- parameter (float)
    - **Roughness** <- parameter (float)
    - **Normal Tangent Space** <- portal Portal Out
- **Emission** <- `lerp` (Lerp)
  - **A** <- `_multiply` (Multiply)
    - **A** <- subgraph `refraction simple for thin objects.msubgraph`
      - **Translucence Color** <- `lerp` (Lerp)
        - **A** <- expression `x,y,z,w`
          - **in** <- parameter `shallow_color`
        - **B** <- expression `x,y,z,w`
          - **in** <- parameter `deep_color`
        - **Coefficient** <- `saturate` (Saturate)
          - **Value** <- `pow` (Power)
            - ...
      - **Fake Refraction Intensity** <- parameter `refraction`
      - **Translucence Roughness** <- parameter (float)
      - **Normal Tangent Space** <- portal Portal Out
    - **B** <- expression `1-x`
      - **in** <- subgraph `fresnel.msubgraph`
        - **Normal Tangent Space** <- portal Portal Out
  - **B** <- `_multiply` (Multiply)
    - **A** <- subgraph `reflection raymarched.msubgraph`
      - **Step Size** <- parameter (float)
      - **Last Step Size** <- parameter (float)
      - **Threshold** <- parameter (float)
      - **Roughness** <- parameter (float)
      - **Normal Tangent Space** <- portal Portal Out
    - **B** <- subgraph `reflection raymarched.msubgraph`
      - **Step Size** <- parameter (float)
      - **Last Step Size** <- parameter (float)
      - **Threshold** <- parameter (float)
      - **Roughness** <- parameter (float)
      - **Normal Tangent Space** <- portal Portal Out
  - **Coefficient** <- subgraph `fresnel pbr.msubgraph`
    - **Roughness** <- parameter (float)
    - **Normal Tangent Space** <- portal Portal Out
- **Tessellation Vertex Offset Tangent Space** <- expression `0,0,x`
  - **in** <- `_multiply` (Multiply)
    - **A** <- `lerp` (Lerp)
      - **A** <- `_multiply` (Multiply)
        - **A** <- parameter `coast_waves`
        - **B** <- `saturate` (Saturate)
          - **Value** <- `_subtract` (Subtract)
            - ...
      - **B** <- `saturate` (Saturate)
        - **Value** <- `_subtract` (Subtract)
          - **A** <- `_add` (Add)
            - ...
          - **B** <- `_multiply` (Multiply)
            - ...
      - **Coefficient** <- expression `z`
        - **in** <- portal Portal Out
    - **B** <- parameter `height_scale`

## Node inventory

`Parameter` x41, `Expression` x13, `SubGraph` x12, `_multiply` x10, `PortalOut` x7, `Surface Custom Texture` x7, `Vertex UV 1` x7, `float` x5, `lerp` x4, `PortalIn` x2, `_add` x2, `_subtract` x2, `reorientNormalBlend` x2, `saturate` x2, `Final`, `Material`, `SampleTexture`, `pow`

## Subgraphs used

- `fresnel.msubgraph`
- `reflection raymarched.msubgraph`
- `refraction simple for thin objects.msubgraph`
- `fresnel pbr.msubgraph`
- `depth fade.msubgraph`
- `flowmap_panner.msubgraph`

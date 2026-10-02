# procedural_damaged_building

This example illustrates how to create a material combining several layers.

- **Sample:** Multi-Layered Material Example
- **Source:** `art_samples/material_examples/multi_layered_material/materials/procedural_damaged_building.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 123 nodes, 119 links, 36 parameters

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
| `base_settings` | Group |  |  |
| `3d_noise_tiling` | Slider | `0.10000000149011612` |  |
| `mask_3d_contrast` | Slider | `1` |  |
| `layers_bump` | Slider | `0.014999999664723873` |  |
| `layer_0` | Group |  |  |
| `albedo_0` | Texture2D |  | `checker_d.texture` |
| `normal_0` | Texture2D |  | `normal.texture` |
| `albedo_color_0` | Color | `1 1 1 1` |  |
| `shading_0` | Texture2D |  | `white.texture` |
| `metalness_0` | Slider | `1` |  |
| `roughness_0` | Slider | `1` |  |
| `parallax_0` | Texture2D |  | `checker_d.texture` |
| `parallax_0_scale` | Slider | `1` |  |
| `tiling_0` | Slider | `1` |  |
| `layer_1` | Group |  |  |
| `albedo_1` | Texture2D |  | `checker_d.texture` |
| `normal_1` | Texture2D |  | `normal.texture` |
| `heightmap_1` | Texture2D |  | `white.texture` |
| `shading_1` | Texture2D |  | `white.texture` |
| `albedo_color_1` | Color | `1 1 1 1` |  |
| `metalness_1` | Slider | `1` |  |
| `roughness_1` | Slider | `1` |  |
| `mask_intensity_1` | Slider | `1` |  |
| `contrast_1` | Slider | `1` |  |
| `width_1` | Slider | `1` |  |
| `layer_2` | Group |  |  |
| `albedo_2` | Texture2D |  | `white.texture` |
| `normal_2` | Texture2D |  | `normal.texture` |
| `shading_2` | Texture2D |  | `white.texture` |
| `heightmap_2` | Texture2D |  | `white.texture` |
| `albedo_color_2` | Color | `1 1 1 1` |  |
| `metalness_2` | Slider | `0` |  |
| `roughness_2` | Slider | `0.5` |  |
| `mask_intensity_2` | Slider | `1` |  |
| `contrast_2` | Slider | `1` |  |
| `width_2` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- `lerp` (Lerp)
    - **A** <- expression `x,y,z`
      - **in** <- `_multiply` (Multiply)
        - **A** <- expression `x,y,z`
          - **in** <- `SampleTexture` (SampleTexture: Default)
            - ...
        - **B** <- expression `x,y,z`
          - **in** <- parameter `albedo_color_0`
    - **B** <- `_multiply` (Multiply)
      - **A** <- expression `x,y,z`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `albedo_1`
      - **B** <- expression `x,y,z`
        - **in** <- parameter `albedo_color_1`
    - **Coefficient** <- portal Portal Out
  - **B** <- `_multiply` (Multiply)
    - **A** <- expression `x,y,z`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `albedo_2`
    - **B** <- expression `x,y,z`
      - **in** <- parameter `albedo_color_2`
  - **Coefficient** <- portal Portal Out
- **Metalness** <- `lerp` (Lerp)
  - **A** <- `lerp` (Lerp)
    - **A** <- `_multiply` (Multiply)
      - **A** <- expression `x`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `shading_0`
          - **UV** <- portal Portal Out
      - **B** <- parameter `metalness_0`
    - **B** <- `_multiply` (Multiply)
      - **A** <- expression `x`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `shading_1`
      - **B** <- parameter `metalness_1`
    - **Coefficient** <- portal Portal Out
  - **B** <- `_multiply` (Multiply)
    - **A** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `shading_2`
    - **B** <- parameter `metalness_2`
  - **Coefficient** <- portal Portal Out
- **Roughness** <- `lerp` (Lerp)
  - **A** <- `lerp` (Lerp)
    - **A** <- `_multiply` (Multiply)
      - **A** <- expression `y`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `shading_0`
          - **UV** <- portal Portal Out
      - **B** <- parameter `roughness_0`
    - **B** <- `_multiply` (Multiply)
      - **A** <- expression `y`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `shading_1`
      - **B** <- parameter `roughness_1`
    - **Coefficient** <- portal Portal Out
  - **B** <- `_multiply` (Multiply)
    - **A** <- expression `y`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `shading_2`
    - **B** <- parameter `roughness_2`
  - **Coefficient** <- portal Portal Out
- **Normal Tangent Space** <- `reorientNormalBlend` (Reorient Normal Blend)
  - **Base Normal** <- `lerp` (Lerp)
    - **A** <- `lerp` (Lerp)
      - **A** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `normal_0`
        - **UV** <- portal Portal Out
        - **Normal Intensity** <- parameter (float)
      - **B** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `normal_1`
      - **Coefficient** <- portal Portal Out
    - **B** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `normal_2`
    - **Coefficient** <- portal Portal Out
  - **Detail Normal** <- subgraph `normal from height value.msubgraph`
    - **Height Value** <- `lerp` (Lerp)
      - **A** <- portal Portal Out
      - **B** <- `float`
      - **Coefficient** <- portal Portal Out
    - **Height (Meters)** <- parameter `layers_bump`

## Node inventory

`Parameter` x34, `Expression` x18, `SampleTexture` x16, `PortalOut` x15, `_multiply` x13, `lerp` x9, `SubGraph` x4, `PortalIn` x3, `float` x2, `Final`, `Material`, `Surface Custom Texture`, `Texture3D`, `Vertex Position`, `Vertex UV 0`, `Vertex UV 1`, `overlay`, `reorientNormalBlend`

## Subgraphs used

- `contrast.msubgraph`
- `normal from height value.msubgraph`
- `blend by height simple.msubgraph`

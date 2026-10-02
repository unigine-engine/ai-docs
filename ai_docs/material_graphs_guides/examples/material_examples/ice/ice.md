# ice

This example demonstrates how to create an effect of a multi-layered ice material.

- **Sample:** Ice Example
- **Source:** `art_samples/material_examples/ice/materials/ice.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 65 nodes, 67 links, 10 parameters

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
| `Outer Color` | Color | `0.16470600664615676 0.5529410243034385 0.5607839822769165 1` |  |
| `Outer Color Intensity` | Slider | `0.34999999403953647` |  |
| `Inner Color` | Color | `0.003921569790691136 0.003921569790691136 0.1333329975605012 1` |  |
| `Inner Color Intensity` | Slider | `0.34999999403953647` |  |
| `Emission Color` | Color | `0.07058820128440857 0.45490199327469016 0.42352899909019576 1` |  |
| `Emission Intensity` | Slider | `1` |  |
| `Translucency` | Slider | `1` |  |
| `Parallax Intensity` | Slider | `0.11999999731779099` |  |
| `Parallax Min Layers` | Slider | `32` |  |
| `Parallax Max Layers` | Slider | `32` |  |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- `lerp` (Lerp)
    - **A** <- `lerp` (Lerp)
      - **A** <- expression `x,y,z`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- `Texture2D`
          - **UV** <- subgraph `parallax occlusion mapping.msubgraph`
            - ...
      - **B** <- expression `x,x,x`
        - **in** <- `float`
      - **Coefficient** <- expression `x`
        - **in** <- `_multiply` (Multiply)
          - **A** <- `pow` (Power)
            - ...
          - **B** <- `float`
    - **B** <- expression `x,y,z`
      - **in** <- parameter `Outer Color`
    - **Coefficient** <- parameter `Outer Color Intensity`
  - **B** <- expression `x,y,z`
    - **in** <- parameter `Inner Color`
  - **Coefficient** <- `_multiply` (Multiply)
    - **A** <- expression `1-x`
      - **in** <- portal Portal Out
    - **B** <- parameter `Inner Color Intensity`
- **Roughness** <- `_multiply` (Multiply)
  - **A** <- expression `x`
    - **in** <- `lerp` (Lerp)
      - **A** <- `float`
      - **B** <- expression `x`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- `Texture2D`
          - **UV** <- `Vertex UV 0`
      - **Coefficient** <- expression `1-x`
        - **in** <- `_multiply` (Multiply)
          - **A** <- `pow` (Power)
            - ...
          - **B** <- `float`
  - **B** <- `float`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- `Texture2D`
  - **UV** <- `Vertex UV 0`
  - **Normal Intensity** <- `float`
- **Translucent** <- parameter `Translucency`
- **Emission** <- `_multiply` (Multiply)
  - **A** <- `_multiply` (Multiply)
    - **A** <- `lerp` (Lerp)
      - **A** <- `pow` (Power)
        - **Value** <- expression `1-x`
          - **in** <- portal Portal Out
        - **Power** <- `float`
      - **B** <- `float`
      - **Coefficient** <- subgraph `fresnel.msubgraph`
    - **B** <- `srgbInv` (Srgb Inverse)
      - **Color** <- expression `x,y,z`
        - **in** <- parameter `Emission Color`
  - **B** <- parameter `Emission Intensity`

## Node inventory

`Expression` x13, `Parameter` x10, `float` x8, `SampleTexture` x5, `Texture2D` x5, `_multiply` x5, `lerp` x5, `Vertex UV 0` x4, `PortalOut` x2, `SubGraph` x2, `pow` x2, `Final`, `Material`, `PortalIn`, `srgbInv`

## Subgraphs used

- `fresnel.msubgraph`
- `parallax occlusion mapping.msubgraph`

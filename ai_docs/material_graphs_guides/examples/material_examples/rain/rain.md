# rain

This example demonstrates how to create an effect of raindrops on a surface.

- **Sample:** Rain Example
- **Source:** `art_samples/material_examples/rain/materials/rain.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 51 nodes, 51 links, 5 parameters

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
| `albedo_color` | Color | `1 1 1 1` |  |
| `roughness` | Slider | `0.5` |  |
| `Drops` | Group |  |  |
| `drops_speed` | Slider | `1` |  |
| `drops_tiling` | Slider | `4` |  |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- parameter `albedo_color`
- **Roughness** <- `lerp` (Lerp)
  - **A** <- parameter `roughness`
  - **B** <- `float`
  - **Coefficient** <- `_multiply` (Multiply)
    - **A** <- `pow` (Power)
      - **Value** <- expression `x`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- `Texture2D`
          - **UV** <- `_add` (Add)
            - ...
      - **Power** <- `float`
    - **B** <- `saturate` (Saturate)
      - **Value** <- `_multiply` (Multiply)
        - **A** <- `_multiply` (Multiply)
          - **A** <- expression `x`
            - ...
          - **B** <- expression `x`
            - ...
        - **B** <- `float`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- `Texture2D`
  - **UV** <- portal Portal Out
  - **Normal Intensity** <- `saturate` (Saturate)
    - **Value** <- `_multiply` (Multiply)
      - **A** <- `_multiply` (Multiply)
        - **A** <- expression `x`
          - **in** <- `SampleTexture` (SampleTexture: Default)
            - ...
        - **B** <- expression `x`
          - **in** <- `saturate` (Saturate)
            - ...
      - **B** <- `float`

## Node inventory

`Expression` x8, `float` x8, `_multiply` x6, `Parameter` x4, `PortalOut` x4, `SampleTexture` x4, `Texture2D` x4, `saturate` x3, `Final`, `Material`, `PortalIn`, `Time`, `Vertex UV 0`, `_add`, `_subtract`, `lerp`, `pow`, `rerange`

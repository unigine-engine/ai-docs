# fade_by_depth

This example demonstrates how to implement an effect of fading by depth.

- **Sample:** Fade By Depth Example
- **Source:** `art_samples/material_examples/fade_by_depth/materials/fade_by_depth.mgraph`
- **Graph type:** 2 (Mesh Transparent PBR)
- **Size:** 25 nodes, 24 links, 3 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 2 (Tangent) |
| `vertex_mode` | 0 (Position) |
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
| `Intersection Power` | Slider | `5` |  |
| `Fresnel Power` | Slider | `3` |  |
| `Emission Color` | Color | `0 1 1 1` |  |

## What drives the Material node

- **Opacity** <- `saturate` (Saturate)
  - **Value** <- `_add` (Add)
    - **A** <- `pow` (Power)
      - **Value** <- `_subtract` (Subtract)
        - **A** <- `float`
        - **B** <- `saturate` (Saturate)
          - **Value** <- `_subtract` (Subtract)
            - ...
      - **Power** <- parameter `Intersection Power`
    - **B** <- `pow` (Power)
      - **Value** <- `_subtract` (Subtract)
        - **A** <- `float`
        - **B** <- `saturate` (Saturate)
          - **Value** <- `_dot_product` (Dot Product)
            - ...
      - **Power** <- parameter `Fresnel Power`
- **Albedo** <- `float`
- **Emission** <- parameter `Emission Color`

## Node inventory

`Parameter` x3, `_subtract` x3, `float` x3, `saturate` x3, `pow` x2, `Depth Opacity`, `Final`, `Material`, `SampleTexture`, `Screen UV`, `Vertex Normal`, `Vertex Position`, `View Direction`, `_add`, `_dot_product`, `length`

# loop

This example demonstrates how to use loops when creating materials.

- **Sample:** Loop Example
- **Source:** `art_samples/material_examples/loop/materials/loop.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 17 nodes, 20 links, 2 parameters

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
| `Texture` | Texture2D |  | `factory_brick_alb.texture` |
| `blur` | Slider | `0` |  |

## What drives the Material node

- **Albedo** <- `_divide` (Divide)
  - **A** <- `_add` (Add)
    - **A** <- `LoopBegin` (Loop Begin)
      - **Texture_Sample** <- `float3`
    - **B** <- expression `x,y,z`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `Texture`
        - **UV** <- `_add` (Add)
          - **A** <- `_multiply` (Multiply)
            - ...
          - **B** <- `Vertex UV 0`
  - **B** <- `LoopBegin` (Loop Begin)
    - **Texture_Sample** <- `float3`

## Node inventory

`Parameter` x2, `_add` x2, `_multiply` x2, `Expression`, `Final`, `LoopBegin`, `LoopEnd`, `Material`, `SampleTexture`, `Vertex UV 0`, `_divide`, `float`, `float3`, `vogelDisk`

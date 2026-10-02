# material_graph

This example demonstrates how to create a simple UV-panner to animate UV coordinates in a material.

- **Sample:** Panner Example
- **Source:** `art_samples/material_examples/panner/materials/material_graph.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 17 nodes, 19 links, 4 parameters

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
| `Albedo` | Texture2D |  | `jct_pavement_alb.texture` |
| `Normal` | Texture2D |  | `jct_pavement_n.texture` |
| `U Speed` | Slider | `0.20000000298023224` |  |
| `V Speed` | Slider | `0.20000000298023224` |  |

## What drives the Material node

- **Albedo** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Albedo`
  - **UV** <- `_compose_float2` (Compose Float2)
    - **X** <- `_add` (Add)
      - **A** <- expression `x`
        - **in** <- `Vertex UV 0`
      - **B** <- `_multiply` (Multiply)
        - **A** <- `Time` (Auto Game Time)
        - **B** <- parameter `U Speed`
    - **Y** <- `_add` (Add)
      - **A** <- expression `y`
        - **in** <- `Vertex UV 0`
      - **B** <- `_multiply` (Multiply)
        - **A** <- `Time` (Auto Game Time)
        - **B** <- parameter `V Speed`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Normal`
  - **UV** <- `_compose_float2` (Compose Float2)
    - **X** <- `_add` (Add)
      - **A** <- expression `x`
        - **in** <- `Vertex UV 0`
      - **B** <- `_multiply` (Multiply)
        - **A** <- `Time` (Auto Game Time)
        - **B** <- parameter `U Speed`
    - **Y** <- `_add` (Add)
      - **A** <- expression `y`
        - **in** <- `Vertex UV 0`
      - **B** <- `_multiply` (Multiply)
        - **A** <- `Time` (Auto Game Time)
        - **B** <- parameter `V Speed`

## Node inventory

`Parameter` x4, `Expression` x2, `SampleTexture` x2, `_add` x2, `_multiply` x2, `Final`, `Material`, `Time`, `Vertex UV 0`, `_compose_float2`

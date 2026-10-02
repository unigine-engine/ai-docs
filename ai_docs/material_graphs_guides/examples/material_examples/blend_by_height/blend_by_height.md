# blend_by_height

This example demonstrates how to perform blending based on heightmaps when creating materials.

- **Sample:** Blend by Height Example
- **Source:** `art_samples/material_examples/blend_by_height/materials/blend_by_height.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 38 nodes, 39 links, 10 parameters

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
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo 0` | Texture2D |  | `white.texture` |
| `albedo 1` | Texture2D |  | `white.texture` |
| `normal 0` | Texture2D |  | `normal.texture` |
| `normal 1` | Texture2D |  | `normal.texture` |
| `height 0` | Texture2D |  | `black.texture` |
| `height 1` | Texture2D |  | `black.texture` |
| `contrast` | Slider | `10` |  |
| `height 0 scale` | Slider | `0.05000000074505832` |  |
| `height 1 scale` | Slider | `0.019999999552965247` |  |
| `uv transform` | Float4 | `1 1 1 1` |  |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo 0`
      - **UV** <- portal Portal Out
  - **B** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo 1`
      - **UV** <- portal Portal Out
  - **Coefficient** <- subgraph `blend by height.msubgraph`
    - **Height 0 (Avarage Color Should Be Gray)** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `height 0`
        - **UV** <- portal Portal Out
    - **Height 0 Scale (In Meters)** <- parameter `height 0 scale`
    - **Height 1 (Avarage Color Should Be Gray)** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `height 1`
        - **UV** <- portal Portal Out
    - **Height 1 Scale (In Meters)** <- parameter `height 1 scale`
    - **Contrast** <- parameter `contrast`
- **Normal Tangent Space** <- `lerp` (Lerp)
  - **A** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `normal 0`
    - **UV** <- portal Portal Out
  - **B** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `normal 1`
    - **UV** <- portal Portal Out
  - **Coefficient** <- subgraph `blend by height.msubgraph`
    - **Height 0 (Avarage Color Should Be Gray)** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `height 0`
        - **UV** <- portal Portal Out
    - **Height 0 Scale (In Meters)** <- parameter `height 0 scale`
    - **Height 1 (Avarage Color Should Be Gray)** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `height 1`
        - **UV** <- portal Portal Out
    - **Height 1 Scale (In Meters)** <- parameter `height 1 scale`
    - **Contrast** <- parameter `contrast`
- **Tessellation Vertex Offset Tangent Space** <- expression `0,0,x`
  - **in** <- subgraph `blend by height.msubgraph`
    - **Height 0 (Avarage Color Should Be Gray)** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `height 0`
        - **UV** <- portal Portal Out
    - **Height 0 Scale (In Meters)** <- parameter `height 0 scale`
    - **Height 1 (Avarage Color Should Be Gray)** <- expression `x`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `height 1`
        - **UV** <- portal Portal Out
    - **Height 1 Scale (In Meters)** <- parameter `height 1 scale`
    - **Contrast** <- parameter `contrast`

## Node inventory

`Parameter` x10, `Expression` x7, `PortalOut` x6, `SampleTexture` x6, `lerp` x2, `Final`, `Material`, `PortalIn`, `SubGraph`, `Vertex UV 0`, `_add`, `_multiply`

## Subgraphs used

- `blend by height.msubgraph`

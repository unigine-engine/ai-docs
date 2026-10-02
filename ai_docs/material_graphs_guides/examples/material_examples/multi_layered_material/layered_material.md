# layered_material

This example illustrates how to create a material combining several layers.

- **Sample:** Multi-Layered Material Example
- **Source:** `art_samples/material_examples/multi_layered_material/materials/layered_material.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 44 nodes, 42 links, 8 parameters

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
| `Albedo A` | Texture2D |  | `factory_brick_alb.texture` |
| `Albedo B` | Texture2D |  | `jct_pavement_alb.texture` |
| `Albedo C` | Texture2D |  | `wood_2_alb.texture` |
| `Albedo D` | Texture2D |  | `stones_alb.texture` |
| `Normal A` | Texture2D |  | `factory_brick_n.texture` |
| `Normal B` | Texture2D |  | `jct_pavement_n.texture` |
| `Normal C` | Texture2D |  | `wood_2_n.texture` |
| `Normal D` | Texture2D |  | `rocks_n.texture` |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- `lerp` (Lerp)
    - **A** <- `lerp` (Lerp)
      - **A** <- expression `x,y,z`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `Albedo A`
      - **B** <- expression `x,y,z`
        - **in** <- `SampleTexture` (SampleTexture: Default)
          - **Texture** <- parameter `Albedo B`
      - **Coefficient** <- expression `x`
        - **in** <- portal Portal Out
    - **B** <- expression `x,y,z`
      - **in** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `Albedo C`
    - **Coefficient** <- expression `y`
      - **in** <- portal Portal Out
  - **B** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `Albedo D`
  - **Coefficient** <- expression `z`
    - **in** <- portal Portal Out
- **Normal Tangent Space** <- `lerp` (Lerp)
  - **A** <- `lerp` (Lerp)
    - **A** <- `lerp` (Lerp)
      - **A** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `Normal A`
      - **B** <- `SampleTexture` (SampleTexture: Default)
        - **Texture** <- parameter `Normal B`
      - **Coefficient** <- expression `x`
        - **in** <- portal Portal Out
    - **B** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `Normal C`
    - **Coefficient** <- expression `y`
      - **in** <- portal Portal Out
  - **B** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `Normal D`
  - **Coefficient** <- expression `z`
    - **in** <- portal Portal Out

## Node inventory

`Expression` x10, `SampleTexture` x9, `Parameter` x8, `PortalOut` x6, `lerp` x6, `Final`, `Material`, `PortalIn`, `Surface Custom Texture`, `Vertex UV 1`

# two-layered_material

This example illustrates how to create a material combining several layers.

- **Sample:** Multi-Layered Material Example
- **Source:** `art_samples/material_examples/multi_layered_material/materials/two-layered_material.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 74 nodes, 71 links, 19 parameters

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
| `hightmap` | Texture2D |  | `white.texture` |
| `hightmap_tiling` | Slider | `1` |  |
| `blend_contrast` | Slider | `1` |  |
| `blend_width` | Slider | `1` |  |
| `bump_intensity` | Slider | `1` |  |
| `layer_0` | Group |  |  |
| `albedo` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `0` |  |
| `roughness` | Slider | `0.5` |  |
| `tiling` | Slider | `1` |  |
| `layer_1` | Group |  |  |
| `albedo_1` | Texture2D |  | `white.texture` |
| `normal_1` | Texture2D |  | `normal.texture` |
| `color_1` | Color | `1 1 1 1` |  |
| `metalness_1` | Slider | `0` |  |
| `roughness_1` | Slider | `0.5` |  |
| `tiling_1` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- `_multiply` (Multiply)
    - **A** <- expression `x,y,z`
      - **in** <- subgraph `triplanar color.msubgraph`
        - **Texture2D** <- parameter `albedo`
        - **Tiling** <- expression `x,x,x`
          - **in** <- parameter `tiling`
    - **B** <- expression `x,y,z`
      - **in** <- parameter `color`
  - **B** <- `_multiply` (Multiply)
    - **A** <- expression `x,y,z`
      - **in** <- subgraph `triplanar color.msubgraph`
        - **Texture2D** <- parameter `albedo_1`
        - **Tiling** <- expression `x,x,x`
          - **in** <- parameter `tiling_1`
    - **B** <- expression `x,y,z`
      - **in** <- parameter `color_1`
  - **Coefficient** <- portal Portal Out
- **Metalness** <- `lerp` (Lerp)
  - **A** <- parameter `metalness`
  - **B** <- parameter `metalness_1`
  - **Coefficient** <- portal Portal Out
- **Roughness** <- `lerp` (Lerp)
  - **A** <- parameter `roughness`
  - **B** <- parameter `roughness_1`
  - **Coefficient** <- portal Portal Out
- **Normal Tangent Space** <- `reorientNormalBlend` (Reorient Normal Blend)
  - **Base Normal** <- `lerp` (Lerp)
    - **A** <- `RotateSpace` (Rotate Space)
      - **Object** <- subgraph `triplanar normal.msubgraph`
        - **NormalMap Texture** <- parameter `normal`
        - **Tiling** <- expression `x,x,x`
          - **in** <- parameter `tiling`
    - **B** <- `RotateSpace` (Rotate Space)
      - **Object** <- subgraph `triplanar normal.msubgraph`
        - **NormalMap Texture** <- parameter `normal_1`
        - **Tiling** <- expression `x,x,x`
          - **in** <- parameter `tiling_1`
    - **Coefficient** <- portal Portal Out
  - **Detail Normal** <- subgraph `normal from height value.msubgraph`
    - **Height Value** <- portal Portal Out
    - **Height (Meters)** <- parameter `bump_intensity`

## Node inventory

`Parameter` x24, `Expression` x11, `SubGraph` x7, `_multiply` x6, `PortalOut` x5, `SampleTexture` x5, `Vertex UV 0` x4, `lerp` x4, `RotateSpace` x2, `Final`, `Material`, `PortalIn`, `Surface Custom Texture`, `Vertex UV 1`, `reorientNormalBlend`

## Subgraphs used

- `blend by height simple.msubgraph`
- `normal from height value.msubgraph`
- `triplanar color.msubgraph`
- `triplanar normal.msubgraph`

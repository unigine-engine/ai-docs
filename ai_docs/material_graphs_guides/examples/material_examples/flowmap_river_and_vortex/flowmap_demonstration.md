# flowmap_demonstration

Using the Flowmap Panner node to create rivers, and vortexes.

- **Sample:** Flowmap River and Vortex Example
- **Source:** `art_samples/material_examples/flowmap_river_and_vortex/materials/flowmap_demonstration.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 34 nodes, 33 links, 8 parameters

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
| `albedo_color` | Color | `1 1 1 1` |  |
| `roughness` | Slider | `0.5` |  |
| `tiling` | Float2 | `1 1` |  |
| `speed` | Slider | `0.7500000000000014` |  |
| `flowmap_strength` | Slider | `0.5` |  |
| `normal_intensity` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- parameter `albedo_color`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- `reorientNormalBlend` (Reorient Normal Blend)
  - **Base Normal** <- `reorientNormalBlend` (Reorient Normal Blend)
    - **Base Normal** <- subgraph `flowmap_panner.msubgraph`
      - **Source Texture** <- parameter `normal`
      - **FlowMap Texture (0-1)** <- `Surface Custom Texture`
      - **Source Tiling** <- parameter `tiling`
      - **FlowMap UV** <- `Vertex UV 1`
      - **Speed** <- parameter `speed`
      - **Strength** <- parameter `flowmap_strength`
      - **Normal Intensity** <- parameter `normal_intensity`
    - **Detail Normal** <- subgraph `flowmap_panner.msubgraph`
      - **Source Texture** <- parameter `normal`
      - **FlowMap Texture (0-1)** <- `Surface Custom Texture`
      - **Source Tiling** <- `_multiply` (Multiply)
        - **A** <- parameter `tiling`
        - **B** <- `float`
      - **FlowMap UV** <- `Vertex UV 1`
      - **Speed** <- parameter `speed`
      - **Strength** <- parameter `flowmap_strength`
      - **Normal Intensity** <- parameter `normal_intensity`
  - **Detail Normal** <- subgraph `flowmap_panner.msubgraph`
    - **Source Texture** <- parameter `normal`
    - **FlowMap Texture (0-1)** <- `Surface Custom Texture`
    - **Source Tiling** <- `_multiply` (Multiply)
      - **A** <- parameter `tiling`
      - **B** <- `float`
    - **FlowMap UV** <- `Vertex UV 1`
    - **Speed** <- parameter `speed`
    - **Strength** <- parameter `flowmap_strength`
    - **Normal Intensity** <- parameter `normal_intensity`

## Node inventory

`Parameter` x17, `SubGraph` x3, `Surface Custom Texture` x3, `Vertex UV 1` x3, `_multiply` x2, `float` x2, `reorientNormalBlend` x2, `Final`, `Material`

## Subgraphs used

- `flowmap_panner.msubgraph`

# uv_tiling_and_offset

This example demonstrates how to implement UV adjustment (tiling and offset) in a material.

- **Sample:** UV Tiling and Offset Example
- **Source:** `art_samples/material_examples/uv_tiling_and_offset/materials/uv_tiling_and_offset.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 14 nodes, 13 links, 4 parameters

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
| `albedo` | Texture2D |  | `stones_alb.texture` |
| `normal` | Texture2D |  | `rocks_n.texture` |
| `UV Offset` | Float2 | `0 0` |  |
| `UV Tiling` | Float2 | `1 1` |  |

## What drives the Material node

- **Albedo** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `albedo`
  - **UV** <- subgraph `tiling and offset.msubgraph`
    - **UV** <- `Vertex UV 0`
    - **Tiling** <- parameter `UV Tiling`
    - **Offset** <- parameter `UV Offset`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
  - **UV** <- subgraph `tiling and offset.msubgraph`
    - **UV** <- `Vertex UV 0`
    - **Tiling** <- parameter `UV Tiling`
    - **Offset** <- parameter `UV Offset`

## Node inventory

`Parameter` x6, `SampleTexture` x2, `SubGraph` x2, `Vertex UV 0` x2, `Final`, `Material`

## Subgraphs used

- `tiling and offset.msubgraph`

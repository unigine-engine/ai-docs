# test_subgraphs

This example demonstrates how to create Subgraphs and use them in your Material Graphs.

- **Sample:** Custom Subgraphs Example
- **Source:** `art_samples/material_examples/custom_subgraphs/materials/test_subgraphs.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 34 nodes, 33 links, 3 parameters

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
| `Albedo` | Texture2D |  | `factory_brick_alb.texture` |
| `Normal` | Texture2D |  | `factory_brick_n.texture` |
| `Panner Speed` | Float2 | `1 0` |  |

## What drives the Material node

- **Albedo** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Albedo`
  - **UV** <- subgraph `uv panner.msubgraph`
    - **UV** <- `Vertex UV 0`
    - **Speed** <- parameter `Panner Speed`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Normal`
  - **UV** <- subgraph `uv panner.msubgraph`
    - **UV** <- `Vertex UV 0`
    - **Speed** <- parameter `Panner Speed`

## Node inventory

`float3` x4, `float4` x4, `Parameter` x3, `float2` x3, `SampleTexture` x2, `SubGraph` x2, `Final`, `Material`, `Texture2D`, `Texture2DArray`, `Texture3D`, `TextureCube`, `Vertex UV 0`, `bool`, `float`, `int`, `int2`, `int3`, `int4`, `matrix2Row`, `matrix3Row`, `matrix4Row`

## Subgraphs used

- `all_types_of_data.msubgraph`
- `uv panner.msubgraph`

# geometry_inflation

- **Source:** `showcase_content/materials/base_materials/geometry_inflation.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 9 nodes, 8 links, 4 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 2 (Tangent) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 2 (Tangent) |
| `vertex_mode` | 1 (Offset) |
| `two_sided` | True |
| `tessellation` | False |
| `depth_test` | True |
| `blend_mode` | 0 |
| `cast_gi` | False |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `albedo_color` | Color | `1 1 1 1` |  |
| `inflation_start_distance` | Slider | `0` |  |
| `inflation_scale` | Slider | `0.025000000372529037` |  |
| `inflation_maximum_distance` | Slider | `300` |  |

## What drives the Material node

- **Albedo** <- expression `x,y,z`
  - **in** <- parameter `albedo_color`
- **Roughness** <- `float`
- **Vertex Offset Tangent Space** <- subgraph `?`
  - **Inflation Start Distance** <- parameter `inflation_start_distance`
  - **Inflation Scale** <- parameter `inflation_scale`
  - **Inflation Maximum** <- parameter `inflation_maximum_distance`

## Node inventory

`Parameter` x4, `Expression`, `Final`, `Material`, `SubGraph`, `float`

## Subgraphs used

- `69e057aabf8d5feaba84e81da1c6c61e9cf31148`

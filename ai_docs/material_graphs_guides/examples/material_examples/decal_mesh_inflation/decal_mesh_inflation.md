# decal_mesh_inflation

This example demonstrates how to implement Geometry Inflation based on camera distance for Mesh Decals. The technique helps preserve visibility for very thin elements when TAA is enabled. For 3D objects (e.g., lampposts, pipes, ropes, cables, antennas, etc.), it works by offsetting vertices along their normal vectors, making them appear slightly thicker as they move farther away from the camera. For meshes see the Geometry Inflation sample.

- **Sample:** Decal Mesh Inflation
- **Source:** `art_samples/material_examples/decal_mesh_inflation/materials/decal_mesh_inflation.mgraph`
- **Graph type:** 4 (Decal PBR)
- **Size:** 22 nodes, 22 links, 14 parameters

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
| `cast_gi` | False |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `inflation` | Bool | `0` |  |
| `albedo` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `albedo_color` | Color | `1 1 1 1` |  |
| `metalness` | Slider | `0` |  |
| `roughness` | Slider | `0.5` |  |
| `parameter_0` | Group |  |  |
| `inflate u/v` | Static Int | `0` |  |
| `inflation_scale` | Slider | `1` |  |
| `inflation_min_threshold` | Slider | `0` |  |
| `inflation_max_threshold` | Slider | `1000` |  |
| `angle_inflation` | Bool | `0` |  |
| `angle_inflation_intensity` | Slider | `1` |  |
| `angle_power` | Slider | `1` |  |

## What drives the Material node

- **Opacity** <- expression `w`
  - **in** <- `_multiply` (Multiply)
    - **A** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo`
    - **B** <- parameter `albedo_color`
- **Albedo** <- `_multiply` (Multiply)
  - **A** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `albedo`
  - **B** <- parameter `albedo_color`
- **Metalness** <- parameter `metalness`
- **Roughness** <- parameter `roughness`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `normal`
- **Vertex Offset Tangent Space** <- `Branch`
  - **Condition** <- parameter `inflation`
  - **True** <- subgraph `decal_mesh_inflation.msubgraph`
    - **Inflate U(0) / V(1)** <- parameter `inflate u/v`
    - **Inflation Scale** <- parameter `inflation_scale`
    - **Inflation Min Threshold** <- parameter `inflation_min_threshold`
    - **Angle Inflation** <- parameter `angle_inflation`
    - **Angle Inflation Intensity** <- parameter `angle_inflation_intensity`
    - **Angle Power** <- parameter `angle_power`
    - **Inflation Max Threshold** <- parameter `inflation_max_threshold`
  - **False** <- `float3`

## Node inventory

`Parameter` x13, `SampleTexture` x2, `Branch`, `Expression`, `Final`, `Material`, `SubGraph`, `_multiply`, `float3`

## Subgraphs used

- `decal_mesh_inflation.msubgraph`

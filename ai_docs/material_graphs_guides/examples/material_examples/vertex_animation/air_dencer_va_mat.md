# air_dencer_va_mat

This example demonstrates how to use a vertex animation texture in UNIGINE.

- **Sample:** Vertex Animation Example
- **Source:** `art_samples/material_examples/vertex_animation/materials/air_dencer_va_mat.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 44 nodes, 40 links, 13 parameters

## Settings

| field | value |
|---|---|
| `normal_space` | 1 (Object) |
| `vertex_position_space` | 1 (Object) |
| `vertex_offset_space` | 0 (World) |
| `vertex_mode` | 0 (Position) |
| `two_sided` | True |
| `tessellation` | False |
| `depth_test` | True |
| `blend_mode` | 0 |
| `depth_shadow` | True |
| `screen_projection` | False |

## Parameters

Names a child `.mat` writes with `<parameter name="...">`.

| name | type | default | asset |
|---|---|---|---|
| `Surface_material` | Group |  |  |
| `albedo_color` | Color | `1 1 1 1` |  |
| `albedo` | Texture2D |  | `white.texture` |
| `shading` | Texture2D |  | `white.texture` |
| `normal` | Texture2D |  | `normal.texture` |
| `roughness` | Slider | `1` |  |
| `normal_intensity` | Slider | `1` |  |
| `translucent_intensity` | Slider | `0` |  |
| `Animation` | Group |  |  |
| `position_offsets_object_space` | Texture2D |  | `white.texture` |
| `normals_object_space` | Texture2D |  | `white.texture` |
| `animation_speed` | Slider | `1` |  |
| `vertex_offset_intensity` | Slider | `1` |  |

## What drives the Material node

- **Albedo** <- portal Portal Out
- **Roughness** <- portal Portal Out
- **Normal Object Space** <- portal Portal Out
- **Translucent** <- parameter `translucent_intensity`
- **Vertex Position Object Space** <- portal Portal Out

## Node inventory

`Parameter` x10, `SampleTexture` x5, `Expression` x4, `PortalIn` x4, `PortalOut` x4, `Vertex UV 0` x3, `_multiply` x3, `RotateSpace` x2, `Final`, `Material`, `Time`, `Vertex Position`, `Vertex UV 1`, `VertexInterpolation`, `_add`, `_compose_float2`, `reorientNormalBlend`

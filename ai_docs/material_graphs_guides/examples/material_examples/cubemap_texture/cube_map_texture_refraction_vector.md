# cube_map_texture_refraction_vector

This example demonstrates the creation of materials applying custom cubemap textures for reflective and refractive materials.

- **Sample:** Cubemap Texture Example
- **Source:** `art_samples/material_examples/cubemap_texture/materials/cube_map_texture_refraction_vector.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 15 nodes, 14 links, 2 parameters

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
| `Roughness` | Slider | `1` |  |
| `IOR` | Slider | `1.5` |  |

## What drives the Material node

- **Albedo** <- `float`
- **Roughness** <- `float`
- **Emission** <- expression `x,y,z`
  - **in** <- `SampleTexture` (SampleTexture: Mip)
    - **Texture** <- `TextureCube`
    - **Direction** <- `refract` (Refract)
      - **Ray Direction** <- expression `-x,-y,-z`
        - **in** <- `View Direction`
      - **Normal** <- `Vertex Normal`
      - **Refraction Index** <- `_divide` (Divide)
        - **A** <- `float`
        - **B** <- parameter `IOR`
    - **Mip** <- parameter `Roughness`

## Node inventory

`float` x3, `Expression` x2, `Parameter` x2, `Final`, `Material`, `SampleTexture`, `TextureCube`, `Vertex Normal`, `View Direction`, `_divide`, `refract`

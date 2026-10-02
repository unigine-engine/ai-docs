# fresnel_effect

This example demonstrates how to implement the Fresnel effect with respect to a normal map used when creating materials.

- **Sample:** Fresnel Effect Example
- **Source:** `art_samples/material_examples/fresnel_effect/materials/fresnel_effect.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 11 nodes, 11 links, 4 parameters

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
| `Albedo` | Texture2D |  | `jct_pavement_alb.texture` |
| `Normal` | Texture2D |  | `jct_pavement_n.texture` |
| `Color` | Color | `0.5803920030593877 1 0.239215999841691 1` |  |
| `Power` | Slider | `2` |  |

## What drives the Material node

- **Albedo** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Albedo`
- **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
  - **Texture** <- parameter `Normal`
- **Emission** <- `_multiply` (Multiply)
  - **A** <- subgraph `fresnel.msubgraph`
    - **Normal Tangent Space** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `Normal`
    - **Power** <- parameter `Power`
  - **B** <- expression `x,y,z`
    - **in** <- parameter `Color`

## Node inventory

`Parameter` x4, `SampleTexture` x2, `Expression`, `Final`, `Material`, `SubGraph`, `_multiply`

## Subgraphs used

- `fresnel.msubgraph`

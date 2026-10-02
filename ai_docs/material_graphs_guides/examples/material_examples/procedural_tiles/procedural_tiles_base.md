# procedural_tiles_base

This example demonstrates how to create a procedurally damaged tiled material with two layers.

- **Sample:** Procedural Tiles Example
- **Source:** `art_samples/material_examples/procedural_tiles/materials/procedural_tiles_base.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 68 nodes, 65 links, 16 parameters

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
| `Background` | Group |  |  |
| `albedo_background` | Texture2D |  | `white.texture` |
| `normal_background` | Texture2D |  | `normal.texture` |
| `roughness_background` | Slider | `0.5` |  |
| `Tiles` | Group |  |  |
| `albedo_tiles` | Texture2D |  | `white.texture` |
| `normal_tiles` | Texture2D |  | `normal.texture` |
| `tiles_mask` | Texture2D |  | `white.texture` |
| `tiles_mask_offset` | Texture2D |  | `white.texture` |
| `tiles_mask_damage` | Texture2D |  | `white.texture` |
| `mask_additional` | Texture2D |  | `white.texture` |
| `tiles_bump_intensity` | Slider | `1` |  |
| `parallax_intensity` | Slider | `0.0020000000949949082` |  |
| `Other Parameters` | Group |  |  |
| `damage_level` | Slider | `1` |  |
| `tiling` | Float2 | `1 1` |  |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo_background`
      - **UV** <- portal Portal Out
  - **B** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `albedo_tiles`
      - **UV** <- portal Portal Out
  - **Coefficient** <- portal Portal Out
- **Roughness** <- `lerp` (Lerp)
  - **A** <- parameter `roughness_background`
  - **B** <- expression `x`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- `Texture2D`
      - **UV** <- portal Portal Out
  - **Coefficient** <- portal Portal Out
- **Normal Tangent Space** <- `reorientNormalBlend` (Reorient Normal Blend)
  - **Base Normal** <- `lerp` (Lerp)
    - **A** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `normal_background`
      - **UV** <- portal Portal Out
    - **B** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `normal_tiles`
      - **UV** <- portal Portal Out
    - **Coefficient** <- portal Portal Out
  - **Detail Normal** <- subgraph `normal from height value.msubgraph`
    - **Height Value** <- portal Portal Out
    - **Height (Meters)** <- parameter `tiles_bump_intensity`

## Node inventory

`Parameter` x13, `PortalOut` x13, `SampleTexture` x9, `Expression` x7, `_multiply` x4, `float` x4, `PortalIn` x3, `lerp` x3, `SubGraph` x2, `Texture2D` x2, `_add` x2, `Final`, `Material`, `Vertex UV 0`, `reorientNormalBlend`, `rerange`, `saturate`

## Subgraphs used

- `parallax simple.msubgraph`
- `normal from height value.msubgraph`

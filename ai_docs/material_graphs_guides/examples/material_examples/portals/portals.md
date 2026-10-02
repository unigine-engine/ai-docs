# portals

This example demonstrates how to use portals in your materials.

- **Sample:** Portals Example
- **Source:** `art_samples/material_examples/portals/materials/portals.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 12 nodes, 8 links, 3 parameters

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
| `Color A` | Color | `1 0 0 1` |  |
| `Color B` | Color | `0 1 0 1` |  |
| `Lerp` | Slider | `0.5` |  |

## What drives the Material node

- **Albedo** <- `lerp` (Lerp)
  - **A** <- portal Portal Out
  - **B** <- portal Portal Out
  - **Coefficient** <- portal Portal Out

## Node inventory

`Parameter` x3, `PortalIn` x3, `PortalOut` x3, `Final`, `Material`, `lerp`

# combobox_example

This example demonstrates how to use comboboxes in your materials.

- **Sample:** Combobox Example
- **Source:** `art_samples/material_examples/combobox/materials/combobox_example.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 40 nodes, 39 links, 13 parameters

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
| `material_type` | Combobox | `0` |  |
| `wood` | Group |  |  |
| `wood_albedo` | Texture2D |  | `white.texture` |
| `wood_normal` | Texture2D |  | `normal.texture` |
| `wood_roughness` | Slider | `0.7500000000000004` |  |
| `stone` | Group |  |  |
| `stone_albedo` | Texture2D |  | `white.texture` |
| `stone_normal` | Texture2D |  | `normal.texture` |
| `stone_roughness` | Slider | `0.5` |  |
| `metal` | Group |  |  |
| `metal_albedo` | Texture2D |  | `white.texture` |
| `metal_normal` | Texture2D |  | `normal.texture` |
| `metal_roughness` | Slider | `0.25` |  |

## What drives the Material node

- **Albedo** <- `ComboboxSwitch` (Combobox Switch)
  - **Combobox** <- parameter `material_type`
  - **wood** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `wood_albedo`
      - **UV** <- portal Portal Out
  - **stone** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `stone_albedo`
      - **UV** <- portal Portal Out
  - **metal** <- expression `x,y,z`
    - **in** <- `SampleTexture` (SampleTexture: Default)
      - **Texture** <- parameter `metal_albedo`
      - **UV** <- portal Portal Out
- **Metalness** <- `ComboboxSwitch` (Combobox Switch)
  - **Combobox** <- parameter `material_type`
  - **wood** <- `float`
  - **stone** <- `float`
  - **metal** <- `float`
- **Roughness** <- `ComboboxSwitch` (Combobox Switch)
  - **Combobox** <- parameter `material_type`
  - **wood** <- parameter `wood_roughness`
  - **stone** <- parameter `stone_roughness`
  - **metal** <- parameter `metal_roughness`
- **Normal Tangent Space** <- `ComboboxSwitch` (Combobox Switch)
  - **Combobox** <- parameter `material_type`
  - **wood** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `wood_normal`
    - **UV** <- portal Portal Out
  - **stone** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `stone_normal`
    - **UV** <- portal Portal Out
  - **metal** <- `SampleTexture` (SampleTexture: Default)
    - **Texture** <- parameter `metal_normal`
    - **UV** <- portal Portal Out

## Node inventory

`Parameter` x12, `PortalOut` x6, `SampleTexture` x6, `ComboboxSwitch` x4, `float` x4, `Expression` x3, `Final`, `Material`, `PortalIn`, `Vertex UV 0`, `_multiply`

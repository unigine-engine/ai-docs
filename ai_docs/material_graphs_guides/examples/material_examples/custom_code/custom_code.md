# custom_code

This example demonstrates how to create and use nodes containing a custom shader code.

- **Sample:** Custom Code Example
- **Source:** `art_samples/material_examples/custom_code/materials/custom_code.mgraph`
- **Graph type:** 0 (Mesh Opaque PBR)
- **Size:** 6 nodes, 6 links, 2 parameters

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
| `A` | Slider | `0.25` |  |
| `B` | Slider | `0.5` |  |

## What drives the Material node

- **Albedo** <- `float`
- **Metalness** <- `Function` (Function: Function 1)
  - **A** <- parameter `A`
  - **B** <- parameter `B`
- **Roughness** <- `Function` (Function: Function 1)
  - **A** <- parameter `A`
  - **B** <- parameter `B`

## Node inventory

`Parameter` x2, `Final`, `Function`, `Material`, `float`

## Inline code

Held in the node's `props`, written verbatim into the shader.

**Function**

```hlsl
float function_1(in float a, in float b, out float c)
{
	c = lerp(a, b, 0.5f);
	return a+b;
}
```

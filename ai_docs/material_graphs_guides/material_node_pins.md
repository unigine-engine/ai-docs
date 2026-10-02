# Material Node Pins

The input pins of the `Material` node are not a fixed list. The Editor composes them from the `material` block of the graph, so the same pin can carry a different label in two graphs, and a pin can be absent entirely.

Since links bind by pin label, a link written against the wrong label does not connect, and nothing reports it.

Taken from `FinalGraph::update_outputs` in `source/editor2/apps/editor/src/material_editor/MaterialGraph.cpp`, UNIGINE 2.22.

**What a pin's value means is a separate question from what it is called, and the place to settle it is the abstract material the graph compiles into** - for a mesh, `data/core/materials/abstract/mesh/mesh.abstmat` in the SDK. It is plain text, and it shows how your value is consumed. `Velocity` is the cautionary case: the documentation calls it a screen-space pixel offset, while the abstract material does

```
gbuffer.velocity = OUT_FRAG_VELOCITY;
...
gbuffer.velocity.y *= -1.0f;
gbuffer.velocity += getScreenVelocity(old_position, new_position);
```

so the value is in NDC rather than pixels, its y is flipped, and it is *added* to the geometric velocity instead of replacing it. A graph built on the documented reading compiles perfectly and is wrong. When a pin's units, sign or blending matter, read the `.abstmat`.

## Labels composed from settings

`<space>` below is filled in from the setting named beside it.

| pin | label | setting | values |
|---|---|---|---|
| normal | `Normal <space> Space` | `normal_space` | 0 World · 1 Object · 2 Tangent · 3 View |
| vertex, position mode | `Vertex Position <space> Space` | `vertex_mode` = 0, then `vertex_position_space` | 0 Camera World · 1 Object · 2 View · 3 Absolute World |
| vertex, offset mode | `Vertex Offset <space> Space` | `vertex_mode` = 1, then `vertex_offset_space` | 0 World · 1 Object · 2 Tangent · 3 View |
| tessellation factor | `Tessellation Factor`, float | `tessellation` = true | always this label |
| tessellation, position mode | `Tessellation Vertex <space> Position` | `tessellation` = true and `vertex_mode` = 0 | as `vertex_position_space` |
| tessellation, offset mode | `Tessellation Vertex Offset <space> Space` | `tessellation` = true and `vertex_mode` = 1 | as `vertex_offset_space` |
| depth | **`Depth Offset` when `depth_mode` is 0**, `Depth` when it is 1 | `depth_mode` | 0 Offset · 1 Override |

Read the depth row twice: `depth_mode` 0 is `DepthMode::OFFSET`, it is the Editor's default, and it gives the label `Depth Offset`. The shorter label belongs to the other value.

A graph with `"normal_space": 2` takes `Normal Tangent Space`; the same graph switched to `0` takes `Normal World Space` instead, and every link written against the old label is dropped.

Older graphs in the samples carry labels this version no longer produces - `Emissive` for `Emission`, `Tangent Normal` for `Normal Tangent Space`. Follow the tables here rather than copying a label out of an old example.

## Per graph type

`<vertex>` stands for the vertex and tessellation pins from the table above, which every mesh and decal type ends with.

### type 0 — Mesh Opaque PBR

- `Albedo` float3
- `Metalness` float
- `Roughness` float
- `Specular` float
- `Microfiber` float
- `Normal <space> Space` float3
- `Translucent` float
- `Ambient Occlusion` float
- `Emission` float3
- `Velocity` float2 — when `force_velocity` is true
- `Reactivity` float
- `Auxiliary` float4
- `Depth Offset` float — when `depth_mode` is 0 (Offset)
- `Depth` float — when `depth_mode` is 1 (Override)
- `<vertex>`

### type 1 — Mesh Alpha Test PBR

- `Opacity` float
- `Opacity Clip Threshold` float
- `Albedo` float3
- `Metalness` float
- `Roughness` float
- `Specular` float
- `Microfiber` float
- `Normal <space> Space` float3
- `Translucent` float
- `Ambient Occlusion` float
- `Emission` float3
- `Velocity` float2 — when `force_velocity` is true
- `Reactivity` float
- `Auxiliary` float4
- `Auxiliary Clip Threshold` float
- `Depth Offset` float — when `depth_mode` is 0 (Offset)
- `Depth` float — when `depth_mode` is 1 (Override)
- `<vertex>`

### type 2 — Mesh Transparent PBR

- `Opacity` float
- `Albedo` float3
- `Metalness` float
- `Roughness` float
- `Specular` float
- `Microfiber` float
- `Normal <space> Space` float3
- `Translucent` float
- `Ambient Occlusion` float
- `Emission` float3
- `Velocity` float2 — when `force_velocity` and `velocity_write` are both true
- `Reactivity` float — when `reactivity_write` is true
- `Auxiliary` float4
- `Auxiliary Clip Threshold` float
- `Blur` float
- `Refraction Screen UV Offset` float2
- `Depth Offset` float — when `depth_mode` is 0 (Offset)
- `Depth` float — when `depth_mode` is 1 (Override)
- `<vertex>`
- `PostEffects Clip Threshold` float — when any of `opacity_depth_write`, `velocity_write`, `reactivity_write`, `surface_id_write` is true
- `Shadow Clip Threshold` float
- `Shadow Opacity` float

### type 3 — Mesh Transparent Unlit

- `Opacity` float
- `Color` float3
- `Velocity` float2 — when `force_velocity` and `velocity_write` are both true
- `Reactivity` float — when `reactivity_write` is true
- `Auxiliary` float4
- `Auxiliary Clip Threshold` float
- `Blur` float
- `Refraction Screen UV Offset` float2
- `Depth Offset` float — when `depth_mode` is 0 (Offset)
- `Depth` float — when `depth_mode` is 1 (Override)
- `<vertex>`
- `PostEffects Clip Threshold` float — when any of `opacity_depth_write`, `velocity_write`, `reactivity_write`, `surface_id_write` is true

### type 4 — Decal PBR

- `Opacity` float
- `Albedo` float3
- `Opacity (Albedo)` float
- `Metalness` float
- `Specular` float
- `Translucent` float
- `Opacity (Metalness Specular Translucent)` float
- `Roughness` float
- `Microfiber` float
- `Opacity (Roughness Microfiber)` float
- `Normal <space> Space` float3
- `Opacity (Normal)` float
- `Ambient Occlusion` float
- `Opacity (Ambient Occlusion)` float
- `Emission` float3
- `Auxiliary` float4
- `Opacity (Auxiliary)` float
- `<vertex>`

### type 5 — Decal Water

- `Opacity` float
- `Albedo` float3
- `Opacity (Albedo)` float
- `Normal <space> Space` float3
- `Opacity (Normal)` float
- `Emission` float3
- `Auxiliary` float4
- `Opacity (Auxiliary)` float
- `<vertex>`

### type 6 — Post Effect

- `Opacity` float
- `Screen Color` float3


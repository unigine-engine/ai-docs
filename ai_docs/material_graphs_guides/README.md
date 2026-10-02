# Writing UNIGINE Material Graphs by Hand

A `.mgraph` is JSON. Write it, place it under the project's `data/`, and the Editor
imports it as a base material.

This page has two parts. **Rules** is everything needed to write a file that loads
and does what you meant; read it top to bottom once, then use it as a lookup. **Why**
explains the mechanism behind each rule, for when a rule did not fit your case.

```
README.md              this page
node_index.md          405 node types in 1820 configurations: key, pins, props
subgraph_index.md      60 ready-made subgraphs in the SDK core, with asset guids
material_node_pins.md  the Material node's pins, per graph type and settings
SUMMARY.md             one line per example
examples/
    skeletons/         3 hand-written graphs to start from
    material_examples/ 53 graphs from the art samples, one technique each
    base_materials/    27 production base materials from the art sample scenes
```

| you need | open |
|---|---|
| the key a node is written under | [node_index.md](node_index.md), column **key** |
| a node's pins for the settings you chose | [node_index.md](node_index.md), *Nodes whose pins depend on their settings* |
| a ready-made subgraph, its guid and pins | [subgraph_index.md](subgraph_index.md) |
| the `Material` node's pins for your graph type | [material_node_pins.md](material_node_pins.md) |
| a graph that does something similar | [SUMMARY.md](SUMMARY.md) |
| a valid file to start from | [examples/skeletons/](examples/skeletons/) |
| what the docs leave out | `<sdk>/data/core/` — see *Why*, last section |

---

# Rules

## R0. Before writing a graph

1. Check whether a shipped base material already does it. The SDK has 167 under
   `<sdk>/data/core/materials/base/`, plain text. Inheriting costs a short `.mat`.
2. Check [subgraph_index.md](subgraph_index.md). Fresnel, blend by height, flipbook,
   triplanar, parallax occlusion, depth fade, grass and tree animation are subgraphs in
   core; each is one node in your file.
3. Find the closest example in [SUMMARY.md](SUMMARY.md) and copy it. Start from
   [examples/skeletons/](examples/skeletons/) only when nothing is close.

## R1. The file

Five top-level keys, in this order:

```json
{
  "material":   { },
  "parameters": { },
  "version":    "2.22.0.0",
  "nodes":      { },
  "anchors":    { }
}
```

- **Keys repeat.** Two `SampleTexture` nodes are two entries both keyed `SampleTexture`;
  every link is a separate entry keyed `anchor`. Any reader you write must keep
  duplicates — in Python, `json.load(f, object_pairs_hook=...)`.
- `version` must equal the Editor's version string or the import logs an error.

## R2. The `material` block

**Write all nine of these.** A missing one is read as `0`, whatever `0` means there.

| field | values | `0` means |
|---|---|---|
| `type` | 0 Mesh Opaque PBR · 1 Mesh Alpha Test PBR · 2 Mesh Transparent PBR · 3 Mesh Transparent Unlit · 4 Decal PBR · 5 Decal Water · 6 Post Effect | opaque mesh |
| `normal_space`, `vertex_offset_space` | 0 World · 1 Object · 2 Tangent · 3 View | world |
| `vertex_position_space` | 0 Camera World · 1 Object · 2 View · 3 Absolute World | camera world |
| `vertex_mode` | 0 Position · 1 Offset | position |
| `blend_mode` | 0 Alpha Blend · 1 Additive · 2 Multiplicative · 3 Disable · 4 Custom | alpha blend |
| `depth_mode` | 0 Offset · 1 Override | offset |
| `decal_tbn_mode` | 0 Mesh · 1 Up · 2 GBuffer Normal · 3 GBuffer Depth | mesh |
| `normal_blend_mode` | 0 Alpha Blend · 1 Additive | alpha blend |

Every other field keeps the Editor's default when omitted. Copy the whole block from an
example of the **same `type`** anyway, and check the copy carries `advanced_mode` — one
example, `fade_by_depth/base_white.mgraph`, predates 2.22 and its block is wrong.

These settings compose the `Material` node's pin labels. `"normal_space": 2` gives a
pin `Normal Tangent Space`; `0` gives `Normal World Space`. Take the labels from
[material_node_pins.md](material_node_pins.md) for your `type` and settings.

## R3. Nodes

The **JSON key is the node type**. Take it from the **key** column of
[node_index.md](node_index.md), verbatim. The display name is a different string for
most nodes:

| family | key | shown as |
|---|---|---|
| 38 arithmetic and logic nodes, leading underscore | `_add`, `_multiply`, `_dot_product`, `_equal`, `_compose_float3` | Add, Multiply, Dot Product, Equal, Compose Float3 |
| 38 math functions, shader spelling | `abs`, `pow`, `mul3`, `invLerp`, `rsqrt` | Absolute, Power, Matrix Multiply 3x3, Inverse Lerp, Reciprocal Square Root |
| 30 screen buffers | `SSAO`, `Depth`, `GBuffer Albedo` | Texture Buffer SSAO, Texture Buffer Depth, … |

A name that is not in the **key** column is not a key. An unknown key loads as an error
node and logs `unknown node`.

**Build the logic from nodes.** Use a `Function` only for what nodes cannot express: on
the canvas it is a single box, and none of its steps can be previewed or adjusted
there. A formula that would otherwise take a chain of math nodes fits in one
`Expression`, calls such as `nrand` included — see *The Expression node* in
[node_index.md](node_index.md).

Minimal node:

```json
"_multiply": {
  "label": "Multiply",
  "guid": "3452fbd08c4a9cef6a172582823fa6f98482a404",
  "x": 1200,
  "y": 640,
  "props": { }
}
```

- `guid` — exactly 40 hex characters, unique in the file. Invent it. Any other length
  reads as an empty guid: the node still loads, but every link to it fails with
  `can't find input node` / `can't find output node`. Keep two by convention, because
  every example uses them: `Material` = `829f90678c21529ab2138131aaaf08dc82560e8b`,
  `Final` = `0f2f417e3b3b7ac5ee9bad604fcb013f4b641d92`.
- `x`, `y` — layout only. 300–400 apart, left to right.
- `label` — cosmetic, and the Editor replaces it with the default on save.
- `props` — read **by position**. Keep the order and the count from an example of that
  node type. A combobox prop is written as the **index** of its value; the indices are
  in [node_index.md](node_index.md), section *Combobox choices* and in every
  configuration table.
- `inputs` / `outputs` blocks may be left out for most nodes; the loader rebuilds pins
  from the type. Exceptions are in R4.

## R4. Node-level fields

Some node types carry settings as **fields next to `guid`**, outside `props`. Missing
ones mean a misconfigured node, usually with different pins, so its links fail too.

| node | required fields | values |
|---|---|---|
| `Parameter` and every constant node: `float` `float2` `float3` `float4` `int` `int2` `int3` `int4` `bool` `Color (Float3)` `Color (Float4)` `Texture2D` `Texture2DInt` `Texture3D` `Texture2DArray` `TextureCube` `TextureRamp (R)` `(RG)` `(RGB)` `(RGBA)` | `type`; on `Parameter` also `parameter_guid` | `type` ∈ `float` `int` `uint` `bool` `float2` `int2` `uint2` `float3` `int3` `uint3` `float4` `int4` `uint4` `float2x2` `float3x3` `float4x4` `Texture2D` `Texture2DInt` `TextureCube` `Texture3D` `Texture2DArray` `TextureRamp` |
| `SampleTexture` | `texture_type`, `sampler_type`, `texture_data`, `normal_space` | `texture_type`: the six texture values above · `sampler_type`: `Default` `Mip` `Mip offset` `Grad` `Fetch` `Point` `Catmull` `Cubic` `Cubic Mip` `Manual linear` · `texture_data`: `Asset` `Color` `GBuffer Albedo` `GBuffer Shading` `GBuffer Normal` `GBuffer Features` `GBuffer Velocity` `Native Depth` `Linear Depth` `Unpack Normal` `Bent Normal` `SSAO` `DoF Mask` `Auto Exposure` `Curvature` `Refraction Mask` `Transparent Blur` · `normal_space`: `Tangent Space for UV0` `Tangent Space for UV1` `Tangent Space Auto Calculated` `Object Space` |
| `ComboboxSwitch`, `LoopBegin`, `LoopEnd`, `Inputs`, `Outputs` | the whole `inputs` block | copy the shape from an example of that node; the loader reads the block without checking it exists, so a node without it can crash the Editor |
| `SubGraph` | `props[0].asset` = the subgraph's asset guid | from [subgraph_index.md](subgraph_index.md) for core subgraphs |

Without `type`, a constant or `Parameter` node does not load at all (`can't load node`),
and every link to it is dropped. In the examples, `type` is the **last** key of the
node body, after `outputs` — do not lose it when copying.

**These fields decide the node's pins.** Choose them first, then take the pin labels
from the configuration table for that node in [node_index.md](node_index.md).
`SampleTexture` with `texture_data` = `Asset` has a `Normal Intensity` input and a
`Tangent Normal` or `Object Normal` output; with `Fetch` its `UV` becomes `Coord`; with
`GBuffer Shading` it has four outputs and no `Color`.

**An `asset` field names another file by a guid from that file's `.meta`** — in a
`SubGraph` prop, in the prop of a texture constant, and in a texture parameter's
`value.asset`. Which of its guids depends on what the `.meta` lists. Write the one you
pick as 40 hex, without the `guid://` prefix that `.mat` files use:

| the target's `.meta` lists | write |
|---|---|
| a `<runtime … link="1">` line — an image converted to `.texture` | the id of the `link="1"` line |
| only a `<runtime … link="0">` line — a `.texture` file, a `.msubgraph`, an image used as is | that id; it equals `<guid>` |

For an image converted to `.texture`, `<guid>` is the source image: a graph naming it
compiles to a material that points at the raw file instead of the imported texture.
Core subgraph guids are in [subgraph_index.md](subgraph_index.md); every other core
file's `.meta` is in the SDK under `<sdk>/data/core/`.

## R5. Links

```json
"anchor": {
  "input_label":  "Albedo",
  "input_node":   "<guid of the node receiving the value>",
  "output_label": "Color",
  "output_node":  "<guid of the node producing the value>"
}
```

`output_node` produces, `input_node` receives.

A link binds to a pin in this order: **label** (exactly one pin with that label), then
**id**, then saved **index** if the id at that index matches. Write the label; add the
id whenever the label is generated rather than fixed:

| output of | label is | write |
|---|---|---|
| a math node (`_add`, `lerp`, `saturate` …) | empty | `"output_label": "", "output_id": <id from node_index>` |
| a constant node | the value as formatted: `1.0`, `0.1`, `0.0 0.0 1.0`, `3` | the formatted value, plus `"output_id": 0` |
| a `Parameter` node | `value.name` of its parameter | that name |
| `Expression` | the expression text, set after loading | the text, plus `"output_id": 0` |
| `Vertex Position` and other space-selecting nodes | the selected space | the space, per the configuration table |

Pins printed as `""(id 0)` in [node_index.md](node_index.md) are the empty-label case;
`""` is the label and the number is the id. Neither `unnamed` nor the parentheses go in
the file.

Types cast implicitly where it makes sense: `float4` into a `float3` pin, `float` into
`float3`.

Every graph ends with `Material.Material → Final.Material`.

## R6. Parameters

```json
"parameter": {
  "type": "Color",
  "guid": "26e571acbb2c411bbb4203be69d4d80582cce9a0",
  "value": {
    "type": "float4",
    "name": "albedo_color",
    "min_value": 0, "max_value": 1,
    "value_x": 1, "value_y": 1, "value_z": 1, "value_w": 1
  }
}
```

- Outer `type` is the widget (`Color`, `Slider`, `Texture2D`, `Combobox`, …);
  `value.type` is the data type.
- `guid` is internal to the file. Invent it; the `Parameter` node's `parameter_guid`
  must equal it. A `parameter_guid` that matches no declared parameter turns the node
  into a constant of its `type`, with a constant's output label. Links written against
  the parameter's name then fail with `can't find output "<name>"`, and one carrying
  `output_id` binds to the constant without a word. Either way the material compiles
  with a fixed value that no child `.mat` can override.
- `value.name` is what a child `.mat` writes: `<parameter name="albedo_color">…`. It is
  also the `Parameter` node's output label.
- A texture parameter's `value.asset` follows the rule at the end of R4. Without one
  the parameter gets an engine default and still compiles.

## R7. Import and verify

1. Place the file under the project's `data/`. Never write its `.meta` or touch
   `guids.db`.
2. **The Editor imports new and changed files only while its window is active.** While
   the user works in another window, your file waits until they switch back. With the
   Editor's MCP tools, import it yourself; without them, ask the user to switch to the
   Editor.
   - a new file: `asset_import`. It returns the guid of the compiled `.basemat` and the
     loader's messages. `already_imported: true` means the Editor got there first; the
     messages are then only in the console.
   - a changed file: `asset_action` with `action: reimport`. `asset_import` answers
     `already a project asset` and does not reimport.
3. **Read the console once the Editor has compiled the graph.** It does so shortly after
   an import or a reimport and frames the loader's messages:

   ```
   ---- Reimport material graphs ----
   ERROR:	Material Graph loading error (node:"float" file:"b09_rotated_uv.mgraph"): can't load node
   ERROR:	Material Graph loading error (node:"float" file:"b09_rotated_uv.mgraph"): can't find output "0.5"
   Material graphs generate runtimes: 5 (21ms) ----
   Reimport material graphs: 5 (21ms) ----
   ```

   Over MCP read it with `read_console_log`; the same lines are in `bin/editor_log.txt`.
   Each message names its file. None naming yours between the two `Reimport material
   graphs` lines means every node loaded and every link found a pin.
4. **Ask the user to close the graph in the Material Editor before you edit its file.**
   The Editor writes a `.mgraph` only on Save in the Material Editor. A reimport reloads
   an open graph from your file and drops whatever was unsaved in the window; a Save
   made before the reimport writes the window's older state over your file.
5. Three things fail in three places:

| symptom | where the answer is | look for |
|---|---|---|
| a node is missing or is an error node | Editor console at import | `unknown node`, `can't load node`, `guid conflict` (any case) |
| a value never reaches an output | `data/.runtimes/<xx>/<guid>.basemat` | the `OUT_FRAG_*` for that input has no assignment; the parameter has `< shared=false>` instead of `shader_name=` |
| **nothing is drawn although the graph is correct** | **`bin/editor_log.txt`** | `Compilation log`, `can't compile pass` |

## Checklist

- [ ] `material` block: all nine zero-defaulting fields written, `type` matches the example copied
- [ ] every node key is in the **key** column of node_index.md
- [ ] the logic is built from nodes; a `Function` holds only what nodes cannot express
- [ ] every node guid exactly 40 hex characters and unique in the file
- [ ] every `asset` guid taken from the target's `.meta` as R4 says
- [ ] `props` in the same order and count as the example; combobox values are indices
- [ ] `type` on every `Parameter` and constant node; four fields on every `SampleTexture`
- [ ] pin labels taken from the configuration row matching the settings written
- [ ] `output_id` on every link out of an `Expression`, a constant, or an unnamed output
- [ ] `Material` pin labels match material_node_pins.md for this `type` and settings
- [ ] each `parameter_guid` matches a declared parameter
- [ ] `Material.Material → Final.Material` present
- [ ] after import: no loader message naming the file between the `Reimport material graphs` lines; `.basemat` assigns every intended `OUT_FRAG_*`; `editor_log.txt` has no compilation error

---

# Why

## The node registry has no file

The Editor builds the list of node types in memory at startup — 58 hardcoded
constructors, every function in the UUSL shader headers, and one entry per `.msubgraph`
asset. Nothing writes it out. [node_index.md](node_index.md) was produced by
instantiating each type inside the Editor and reading its pins and props back, in every
combination of its settings; that is why it is the only complete list, and why a
name that is not in it does not exist.

Key and display name are the same string for 131 of the 405 types. The 38 arithmetic
nodes carry a leading underscore; the 38 math functions keep their UUSL name and get a
display name from a vocabulary (`mul3` → Matrix Multiply 3x3); the 30 buffers get
`Texture Buffer` prefixed in the documentation only.

## Why nine fields become zero

`FinalGraph::loadJson` reads the `material` block two ways:

```cpp
normal_space_ = RotateSpace(root->getInt("normal_space"));   // missing → 0
root->read("two_sided", two_sided_);                          // missing → untouched
```

`getInt` returns 0 for an absent child. The nine fields in R2 are the ones read that
way; the rest are read into variables the constructor already set. `depth_mode` 0 is
`DepthMode::OFFSET`, which is why the `Material` node's depth pin is labelled
`Depth Offset` in the default case and `Depth` at 1.

## How a link finds its pin

```cpp
// match_anchor_index, MaterialGraph.cpp
label matches exactly one pin      → that pin
else a pin with this id            → that pin
else saved index, if its id matches → that pin
else                               → link dropped, "can't find output"
```

A pin that is already connected is skipped in the label pass, which is why feeding two
links into one input binds only the first.

Generated labels are why the id matters. A constant's output is labelled with its
value through `floatToStr`, which strips trailing zeros and guarantees one decimal:
`1` → `1.0`, `0.10` → `0.1`; integers print as `3`. An `Expression` is created with one
input and one output, both labelled `""` with id 0, and the text becomes the label only
after the whole graph has loaded — so at link time the label cannot match and the id is
the only route.

## Duplicate guids are repaired, silently for the links

On load every node guid is checked against the ones seen so far. A repeat is logged as

```
Material Graph loading error (node:"<label>" file:"<graph>"): guid conflict <guid>
```

and the second node gets a fresh guid. The links still carry the old guid, and it now
names the first node — the graph loads, compiles, and is wired to the wrong node.

A node written without a `guid` usually shows up the same way: the loader keeps the
value it read for the node before, finds it taken, and gives this node a fresh guid that
no link can name.

The same words in capitals, `Material Graph validation error:"GUID conflict <guid>"`,
come from the Editor validating a graph that is already open. A search that ignores case
finds both.

## Why labels do not survive

`MatNode::save` writes `label`; `MatNode::load` never reads it. The label comes from
the node's constructor, and several node types regenerate it on every update
(`SampleTexture` writes `SampleTexture: <sampler>`). The canvas never shows a label you
wrote, and the first Save in the Material Editor replaces it in the file.

## Where `type` sits

In 2.22 `MatNodeVariable::save` writes `type` as the first key of the node. The
examples were saved by an earlier Editor and carry it last, after `outputs`. The loader
does not care about order; the rule in R4 is about not dropping it when copying an
example.

## Texture defaults

A texture parameter or constant with no asset gets `core/textures/common/checker_d`
for `Texture2D` and `Texture2DInt`, `environment_default` for `TextureCube`,
`clouds/curl_noise_3d` for `Texture3D`, `common/noise` for `Texture2DArray`.

## The three checks see three different things

The import console reports what the **loader** refused. The `.basemat` shows what the
**generator** produced — a link that bound to the wrong pin leaves a parameter declared
`< shared=false>` and no `OUT_FRAG_*` assignment, and the console says nothing. The
HLSL compiler runs after both and reports only to `bin/editor_log.txt`:

```
ERROR: Compilation log Shader:"fragment"  hlsl.hlsl:7429:5: error: use of undeclared identifier 'sin'
ERROR:                                    sin(in0,out0,out1);
ERROR:  Material: ".runtimes/28/2894787aed78cf6050337d2f527f02ed1be27232.basemat"
```

That one is the `sin` node in mode `Out(sin,cos)`; see *Configurations that do not
compile* in [node_index.md](node_index.md). An object that is simply not drawn is
indistinguishable from an unassigned material until this log is read.

A parameter that reached an output, for comparison:

```
Color "albedo_color"=[1.000000 1.000000 1.000000 1.000000] <shader_name="var_4b93d847...">
...
		OUT_FRAG_ALBEDO = var_1;
```

## The runtime material

Import compiles the graph to a base material named `<graph file name>.basemat` under
`data/.runtimes/<first two hex of guid>/<guid>.basemat`. Child `.mat` files inherit by
that runtime guid, which lives in the `.meta`. Rewriting the `.mgraph` keeps the guid;
renaming the file changes the alias.

## The core sources are in the SDK, unpacked

```
<sdk>/data/core/materials/base/…          167 .basemat, plain text
<sdk>/data/core/materials/shaders/…       UUSL sources and headers
<sdk>/data/core/materials/abstract/…      what a graph compiles into: mesh.abstmat, post.abstmat
<sdk>/data/core/subgraphs/*.msubgraph     the 60 subgraphs
```

A project has only the packed `core.ung`. Read the SDK copy for anything the
documentation leaves out: the space a buffer is in, what a subgraph pin expects, how a
`Material` input is consumed. `mesh.abstmat` shows, for instance, that `Velocity` is
added to the geometric velocity in NDC with y flipped, which the documentation does
not say.

# Material Graph Node Index

405 node types in 1820 configurations, read out of the Editor itself: every entry was instantiated, every combination of its settings applied, and the pins and props taken off the live object each time. 363 of them carry the description the Editor shows as a tooltip.

## How to read this

**One row is a node in one configuration, not a node.** A node's pins are not fixed: 41 of the 405 types rebuild them from their own settings, and the **settings** column says which setting values produced the pins on that row. Write those settings into the node and you get those pins; write different ones and the labels your links bind by change with them.

`SampleTexture` is the one to be careful with. With `texture_data` set to `Asset` it grows a `Normal Intensity` input and a second output - `Tangent Normal` or `Object Normal`, whichever `normal_space` picks - and that is how most graphs in the SDK use it. With `sampler_type` at `Fetch` its `UV` input becomes `Coord`, typed `int2`. With `texture_data` at `GBuffer Shading` it has four outputs and no `Color` at all. Find the row whose settings match what you intend to write.

**key** is the string you write as the JSON key of a node in a `.mgraph`. **name** is what the Editor's palette and the documentation call it. They differ for most nodes: the node keyed `_add` is documented as **Add**.

**pins** are the labels links bind by, written `label:type`.

A pin printed as `""(id 0)` has **no label**. Its label is the empty string, and that is what the link carries - `"output_label": ""` - with `"output_id": 0` alongside it so the loader can find the pin by id when the empty label matches nothing. Do not write `unnamed` or the parenthesis anywhere; they are not part of the name. This is the normal shape of a math node's single output: of the 341 unlabelled pins here, 338 are outputs.

```json
"anchor": {
  "input_label": "Albedo",  "input_node": "<the node receiving it>",
  "output_label": "",  "output_id": 0,  "output_node": "<the math node>"
}
```

A type of `undefined` - 354 of the 6652 pins here - means the pin has no type of its own and takes the one it is given. `_add` has two of them: connect a `float3` and the node adds float3s. It is not a missing type or a broken entry.

**Pin ids look inconsistent because they come from two places.** A node class written by hand numbers its pins from a small enum - `SampleTexture` uses 4 for `Texture`, 5 for the coordinate, 11 for `Normal Intensity`. A node reflected out of a shader header takes `String::hash` of the shader variable name instead, which is where `-509366906` comes from. Neither is something you invent: an id is copied from this table or left out entirely.

**In palette** marks the nodes you can add by hand in the Editor. The others exist all the same and are written the same way in a file - `Parameter`, `Final`, `Inputs` and `Outputs` are created together with the graph rather than picked from the menu.

## Identifiers: what is what

A `.mgraph` carries four different kinds of identifier. Only the first comes from this table.

| where | what it is | who writes it |
|---|---|---|
| `inputs[].id` / `outputs[].id` here | **pin id**, a plain integer, often negative, unique within its node | copy from this table into an anchor's `input_id` / `output_id` when you want the fallback |
| `nodes.<Key>.guid` | **node id**, 40 hex characters, unique within the file | you invent it |
| `parameters.parameter.guid` + a `Parameter` node's `parameter_guid` | **parameter id**, 40 hex, internal to the graph | you invent it, and use the same value in both places |
| `props[].asset`, `guid://...` | **asset guid**, 40 hex, identifies a real file in the project | take it from the project, never invent |

The shapes make them hard to mix up: a pin id is a number, everything else is 40 hex characters. Pin ids repeat across different nodes - 1652 of the 6657 pins in this table have id 0 - and that is fine, because the loader looks for the id only among the pins of the node the link points at.

Write the pin **label** first; the id is the fallback the loader tries when no single pin carries that label. Two node types need the fallback in practice: `Expression`, whose pins are unnamed until the graph finishes loading, and constant nodes, whose output label is the value as the Editor formats it.

## basic inputs

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Back` | Back | yes | [4 configurations](#back) | - | World:float3 | 0:Space=Combobox | [Provides access to the Back direction, one of the main axes or cubemap faces. It corresponds to the negative Y-axis. The coordinate space of the output value ( World,...](../md_docs/content/materials/graph/node_library/input/back.md) |
| `Down` | Down | yes | [4 configurations](#down) | - | World:float3 | 0:Space=Combobox | [Provides access to the Down direction, one of the main axes or cubemap faces. It corresponds to the negative Z-axis. The coordinate space of the output value ( World,...](../md_docs/content/materials/graph/node_library/input/down.md) |
| `Forward` | Forward | yes | [4 configurations](#forward) | - | World:float3 | 0:Space=Combobox | [Provides access to the Forward direction, one of the main axes or cubemap faces. It corresponds to the positive Y-axis. The coordinate space of the output value (...](../md_docs/content/materials/graph/node_library/input/forward.md) |
| `Golden Ratio` | Golden Ratio | yes | fixed | - | ""(id 0):float | - | [Outputs the golden ratio constant ( 1.618033989f ).](../md_docs/content/materials/graph/node_library/math/golden_ratio.md) |
| `Left` | Left | yes | [4 configurations](#left) | - | World:float3 | 0:Space=Combobox | [Provides access to the Left direction, one of the main axes or cubemap faces. It corresponds to the negative X-axis. The coordinate space of the output value ( World,...](../md_docs/content/materials/graph/node_library/input/left.md) |
| `Material Mask` | Material Mask | yes | fixed | - | ""(id 0):int | - | [Provides access to the Material Mask of the material.](../md_docs/content/materials/graph/node_library/input/material_mask.md) |
| `Maximum Possible Float` | Maximum Possible Float | yes | fixed | - | ""(id 0):float | - | [Displays the largest possible value for the 32-bit floating-point variable.](../md_docs/content/materials/graph/node_library/math/maximum_possible_float.md) |
| `Maximum Possible Half` | Maximum Possible Half | yes | fixed | - | ""(id 0):float | - | [Displays the largest possible value for the half (16-bit) floating-point variable.](../md_docs/content/materials/graph/node_library/math/maximum_possible_half.md) |
| `Maximum Possible Int` | Maximum Possible Int | yes | fixed | - | ""(id 0):int | - | [Displays the largest possible value for the integer variable.](../md_docs/content/materials/graph/node_library/math/maximum_possible_int.md) |
| `Minimum Possible Float` | Minimum Possible Float | yes | fixed | - | ""(id 0):float | - | [Displays the smallest possible value for the 32-bit floating-point variable.](../md_docs/content/materials/graph/node_library/math/minimum_possible_float.md) |
| `Minimum Possible Int` | Minimum Possible Int | yes | fixed | - | ""(id 0):int | - | [Displays the smallest possible value for the integer variable.](../md_docs/content/materials/graph/node_library/math/minimum_possible_int.md) |
| `Pi` | Pi | yes | fixed | - | ""(id 0):float | - | [Outputs the pi constant ( 3.141592654f ).](../md_docs/content/materials/graph/node_library/math/pi.md) |
| `Right` | Right | yes | [4 configurations](#right) | - | World:float3 | 0:Space=Combobox | [Provides access to the Right direction, one of the main axes or cubemap faces. It corresponds to the positive X-axis. The coordinate space of the output value (...](../md_docs/content/materials/graph/node_library/input/right.md) |
| `Up` | Up | yes | [4 configurations](#up) | - | World:float3 | 0:Space=Combobox | [Provides access to the Up direction, one of the main axes or cubemap faces. It corresponds to the positive Z-axis. The coordinate space of the output value ( World,...](../md_docs/content/materials/graph/node_library/input/up.md) |
| `_compose_float2` | Compose Float2 | yes | fixed | X:float, Y:float | ""(id 1723312480):float2 | - | [Creates a float2 vector from 2 float components.](../md_docs/content/materials/graph/node_library/misc/compose_float2.md) |
| `_compose_float3` | Compose Float3 | yes | fixed | X:float, Y:float, Z:float | ""(id 1723312480):float3 | - | [Creates a float3 vector from 3 float components.](../md_docs/content/materials/graph/node_library/misc/compose_float3.md) |
| `_compose_float4` | Compose Float4 | yes | fixed | X:float, Y:float, Z:float, W:float | ""(id 1723312480):float4 | - | [Creates a float4 vector from 4 float components.](../md_docs/content/materials/graph/node_library/misc/compose_float4.md) |
| `_compose_float_by_exponent` | Compose Float By Exponent | yes | fixed | X:undefined, Exponent:undefined | ""(id 1723312480):undefined | - | [Creates a float value from the mantissa and exponent values.](../md_docs/content/materials/graph/node_library/misc/compose_float_by_exponent.md) |
| `_compose_int2` | Compose Int2 | yes | fixed | X:int, Y:int | ""(id 1723312480):int2 | - | [Creates an int2 vector from 2 int components.](../md_docs/content/materials/graph/node_library/misc/compose_int2.md) |
| `_compose_int3` | Compose Int3 | yes | fixed | X:int, Y:int, Z:int | ""(id 1723312480):int3 | - | [Creates a int3 vector from 3 int components.](../md_docs/content/materials/graph/node_library/misc/compose_int3.md) |
| `_compose_int4` | Compose Int4 | yes | fixed | X:int, Y:int, Z:int, W:int | ""(id 1723312480):int4 | - | [Creates a int4 vector from 4 int components.](../md_docs/content/materials/graph/node_library/misc/compose_int4.md) |
| `_decompose_float_by_exponent` | Decompose Float By Exponent | yes | fixed | Value:undefined | Mantissa:undefined, Exponent:undefined | - | [Decomposes a float value to the mantissa and exponent values.](../md_docs/content/materials/graph/node_library/misc/decompose_float_by_exponent.md) |
| `bool` | Bool | yes | fixed | - | false:bool | 0:(no label)=Bool | [Outputs a specified boolean value. To change the output value, double-click on the output value word (false), check the box, and click outside this field.](../md_docs/content/materials/graph/node_library/input/bool.md) |
| `float` | Float | yes | fixed | - | 1.0:float | 0:(no label)=Float | [Outputs a single float value. To set the required output value, double-click on the output float value (1.0), edit it, and click outside this field.](../md_docs/content/materials/graph/node_library/input/float.md) |
| `float2` | Float2 | yes | fixed | - | 1.0 1.0:float2 | 0:(no label)=Float2 | [Outputs a vector of two float values. To set the required output values, double-click on the output values (1.0 1.0), edit them, and click outside this field.](../md_docs/content/materials/graph/node_library/input/float2.md) |
| `float3` | Float3 | yes | fixed | - | 1.0 1.0 1.0:float3 | 0:(no label)=Float3 | [Outputs a vector of three float values. To set the required output values, double-click on the output values (1.0 1.0 1.0), edit them, and click outside this field.](../md_docs/content/materials/graph/node_library/input/float3.md) |
| `float4` | Float4 | yes | fixed | - | 1.0 1.0 1.0 1.0:float4 | 0:(no label)=Float4 | [Outputs a vector of four float values. To set the required output values, double-click on the output values (1.0 1.0 1.0 1.0), edit them, and click outside this field.](../md_docs/content/materials/graph/node_library/input/float4.md) |
| `int` | Int | yes | fixed | - | 0:int | 0:(no label)=Int | [Outputs a single integer value. To set the required output value, double-click on the output float value (0), edit it, and click outside this field.](../md_docs/content/materials/graph/node_library/input/int.md) |
| `int2` | Int2 | yes | fixed | - | 0 0:int2 | 0:(no label)=Int2 | [Outputs a vector of two integer values. To set the required output values, double-click on the output values (0 0), edit them, and click outside this field.](../md_docs/content/materials/graph/node_library/input/int2.md) |
| `int3` | Int3 | yes | fixed | - | 0 0 0:int3 | 0:(no label)=Int3 | [Outputs a vector of three integer values. To set the required output values, double-click on the output values (0 0 0), edit them, and click outside this field.](../md_docs/content/materials/graph/node_library/input/int3.md) |
| `int4` | Int4 | yes | fixed | - | 0 0 0 0:int4 | 0:(no label)=Int4 | [Outputs a vector of four integer values. To set the required output values, double-click on the output values (0 0 0 0), edit them, and click outside this field.](../md_docs/content/materials/graph/node_library/input/int4.md) |

## bits

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `_bits_and` | Bits And | yes | fixed | A:undefined, B:undefined | Result:undefined | - | [Performs the Bitwise AND operation with input values A and B . The bits of the first operand is compared with the corresponding bits in the second operand. The...](../md_docs/content/materials/graph/node_library/logical/bits_and.md) |
| `_bits_negative` | Bits Negative | yes | fixed | Value:undefined | Result:undefined | - | [Performs the Bitwise NOT operation with an input value A . This operation inverts each bit of its operand.](../md_docs/content/materials/graph/node_library/logical/bits_negative.md) |
| `_bits_or` | Bits Or | yes | fixed | A:undefined, B:undefined | Result:undefined | - | [Performs the Bitwise OR operation with input values A and B . The bits of the first operand is compared with the corresponding bits in the second operand. The...](../md_docs/content/materials/graph/node_library/logical/bits_or.md) |
| `_bits_shift_left` | Bits Shift Left | yes | fixed | A:undefined, B:undefined | Result:undefined | - | [Shifts bit pattern in the operand A to the left by the number of bits specified by the operand B .](../md_docs/content/materials/graph/node_library/logical/bits_shift_left.md) |
| `_bits_shift_right` | Bits Shift Right | yes | fixed | A:undefined, B:undefined | Result:undefined | - | [Shifts bit pattern in the operand A to the right by the number of bits specified by the operand B .](../md_docs/content/materials/graph/node_library/logical/bits_shift_right.md) |
| `_bits_xor` | Bits Xor | yes | fixed | A:undefined, B:undefined | Result:undefined | - | [Performs the Bitwise XOR (exclusive or) operation with input values A and B . The bits of the first operand are compared with the corresponding bits in the second...](../md_docs/content/materials/graph/node_library/logical/bits_xor.md) |
| `firstbithigh` | First Bit High | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the location of the first set bit starting from the highest order bit and working downward, per component.](../md_docs/content/materials/graph/node_library/math/first_bit_high.md) |
| `firstbitlow` | First Bit Low | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the location of the first set bit starting from the lowest order bit and working upward, per component.](../md_docs/content/materials/graph/node_library/math/first_bit_low.md) |
| `hasBit` | Has Bit | yes | fixed | Value:undefined, Bit:undefined | ""(id 1723312480):undefined | - | [This node checks the specified Bit of the input Value (or individual components of input vectors), and returns the corresponding floating value &#8212; either 1.0f ,...](../md_docs/content/materials/graph/node_library/logical/has_bit.md) |
| `reversebits` | Reverse Bits | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Reverses the bits of the input value.](../md_docs/content/materials/graph/node_library/math/reverse_bits.md) |

## camera

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Camera Direction` | Camera Direction | yes | [4 configurations](#camera-direction) | - | World:float3 | 0:Space=Combobox | [Provides access to the inverted normalized Camera Direction Vector . Unlike the View Direction Vector it has the same value for all pixels on the screen. The...](../md_docs/content/materials/graph/node_library/input/camera_direction.md) |
| `Camera Far` | Camera Far | yes | fixed | - | ""(id 0):float | - | [Provides access to the Far Plane distance of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/camera_far.md) |
| `Camera IFar` | Camera IFar | yes | fixed | - | ""(id 0):float | - | [Provides access to the reciprocal Far Plane distance (1/far) of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/camera_ifar.md) |
| `Camera INear` | Camera INear | yes | fixed | - | ""(id 0):float | - | [Provides access to the reciprocal Near Plane distance (1/near) of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/camera_inear.md) |
| `Camera Near` | Camera Near | yes | fixed | - | ""(id 0):float | - | [Provides access to the Near Plane distance of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/camera_near.md) |
| `Camera Offset` | Camera Offset | yes | fixed | - | ""(id 0):float3 | - | [Provides access to the additional transformation ( Offset ) for the camera. This transformation is applied after the modelview transformation. Offset does not affect...](../md_docs/content/materials/graph/node_library/input/camera_offset.md) |
| `Camera Position` | Camera Position | yes | [4 configurations](#camera-position) | - | Camera World:float3 | 0:Space=Combobox | [Provides access to the Position of the camera currently being used for rendering. The coordinate space of the output value ( Camera World, Object, View, Absolute...](../md_docs/content/materials/graph/node_library/input/camera_position.md) |
| `View Direction` | View Direction | yes | [4 configurations](#view-direction) | - | World:float3 | 0:Space=Combobox | [Provides access to the normalized View Direction Vector - a vector looking from a point on a surface to the camera. Unlike the Camera Direction Vector it has...](../md_docs/content/materials/graph/node_library/input/view_direction.md) |

## checking

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Is Auxiliary Pass` | Is Auxiliary Pass | yes | fixed | - | ""(id 0):bool | - | [Outputs a boolean value indicating that Auxiliary rendering pass is currently in progress. You can pass this value to a Branch node to change the look of your...](../md_docs/content/materials/graph/node_library/input/is_auxiliary_pass.md) |
| `Is Baking GI` | Is Baking GI | yes | fixed | - | ""(id 0):bool | - | [Outputs a boolean value indicating that baking Global Illumination (GI) is currently in progress. You can pass this value to a Branch node to change the look of your...](../md_docs/content/materials/graph/node_library/input/is_baking_gi.md) |
| `Is Front Face` | Is Front Face | yes | fixed | - | ""(id 0):bool | - | [Outputs a boolean value indicating which polygon face is surrently rendered, front ( True ) or back ( False ). You can pass this value to a Branch node to change the...](../md_docs/content/materials/graph/node_library/input/is_front_face.md) |
| `Is GBuffer Pass` | Is GBuffer Pass | yes | fixed | - | ""(id 0):bool | - | [Outputs a boolean value indicating that GBuffer pass is currently in progress. You can pass this value to a Branch node to change the look of your material during the...](../md_docs/content/materials/graph/node_library/input/is_gbuffer_pass.md) |
| `Is Lightmap` | Is Lightmap | yes | fixed | - | ""(id 0):bool | - | [Outputs a boolean value indicating that lightmaps are used for the surface to which the material is assigned. You can pass this value to a Branch node to change the...](../md_docs/content/materials/graph/node_library/input/is_lightmap.md) |
| `Is Shadow Pass` | Is Shadow Pass | yes | fixed | - | ""(id 0):bool | - | [Outputs a boolean value indicating that shadow rendering pass is currently in progress. You can pass this value to a Branch node to change the look of your material...](../md_docs/content/materials/graph/node_library/input/is_shadow_pass.md) |
| `all` | All | yes | fixed | Value:undefined | ""(id 1723312480):bool | - | [Outputs true if all components of the input are non-zero; otherwise, false .](../md_docs/content/materials/graph/node_library/math/all.md) |
| `any` | Any | yes | fixed | Value:undefined | ""(id 1723312480):bool | - | [Outputs true if any components of the input are non-zero; otherwise, false .](../md_docs/content/materials/graph/node_library/math/any.md) |
| `isOrtho` | Is Ortho | yes | fixed | Projection:float4x4 | ""(id 1723312480):bool | - | [Outputs a boolean value indicating is the input projection matrix is for parallel projection.](../md_docs/content/materials/graph/node_library/matrix/is_ortho.md) |
| `isfinite` | Is Finite | yes | fixed | Value:undefined | ""(id 1723312480):bool | - | [Outputs 1 if the value is a finite number, otherwise, 0 .](../md_docs/content/materials/graph/node_library/math/is_finite.md) |
| `isinf` | Is Infinity | yes | fixed | Value:undefined | ""(id 1723312480):bool | - | [Outputs 1 if the value is infinity, otherwise, 0 .](../md_docs/content/materials/graph/node_library/math/is_infinity.md) |
| `isnan` | Is Nan | yes | fixed | Value:undefined | ""(id 1723312480):bool | - | [Outputs 1 if the value is not a number, otherwise, 0 .](../md_docs/content/materials/graph/node_library/math/is_nan.md) |

## coding

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Function` | Function | yes | fixed | A:float, B:float | C:float | 0:(no label)=Code | Its pins come from the code you write in `props[0]`, so the ones shown here are only the example the node starts with. See *The Function node* below. [This node is used to write your own custom functions, you can have multiple functions inside a single node and even call one function from another. When to use the...](../md_docs/content/materials/graph/node_library/misc/function.md) |

## comparison

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Branch` | Branch | yes | [3 configurations](#branch) | Condition:bool, True:undefined, False:undefined | ""(id 0):undefined | 0:Mode=Combobox | [This node provides a dynamic branch to the shader. If input Condition is true, the return output will be equal to input True , otherwise it will be equal to input...](../md_docs/content/materials/graph/node_library/logical/branch.md) |
| `_equal` | Equal | yes | [2 configurations](#_equal) | A:undefined, B:undefined | ""(id 1723312480):bool | 0:Mode=Combobox | [Compares the two input values A and B and outputs the result: true if A is equal to B or false otherwise. If A and B have a different number of components, a cast is...](../md_docs/content/materials/graph/node_library/logical/equal.md) |
| `_greater` | Greater | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):bool | - | [Compares two input values A and B and outputs the result: true if A is greater than B or false otherwise. If A and B have a different number of components, a cast is...](../md_docs/content/materials/graph/node_library/logical/greater.md) |
| `_greater_or_equal` | Greater Or Equal | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):bool | - | [Compares two input values A and B and outputs the result: true if A is greater than or equal to B or false otherwise. If A and B have a different number of...](../md_docs/content/materials/graph/node_library/logical/greater_or_equal.md) |
| `_less` | Less | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):bool | - | [Compares two input values A and B and outputs the result: true if A is less than B or false otherwise. If A and B have a different number of components, a cast is...](../md_docs/content/materials/graph/node_library/logical/less.md) |
| `_less_or_equal` | Less Or Equal | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):bool | - | [Compares two input values A and B and outputs the result: true if A is less than or equal to B or false otherwise. If A and B have a different number of components, a...](../md_docs/content/materials/graph/node_library/logical/less_or_equal.md) |
| `_logical_and` | Logical And | yes | fixed | A:bool, B:bool | ""(id 1723312480):bool | - | [Performs the Logical AND operation with input values A and B and outputs the result: true if both A and B are true , otherwise, it returns false .](../md_docs/content/materials/graph/node_library/logical/logical_and.md) |
| `_logical_negative` | Logical Negative | yes | fixed | Value:bool | ""(id 1723312480):bool | - | [Performs the Logical NOT operation with an input value A and outputs the result: true if A is false , or false if A is true .](../md_docs/content/materials/graph/node_library/logical/logical_negative.md) |
| `_logical_or` | Logical Or | yes | fixed | A:bool, B:bool | ""(id 1723312480):bool | - | [Performs the Logical OR operation with input values A and B and outputs the result: true if either or both A and B are true , otherwise, it returns false .](../md_docs/content/materials/graph/node_library/logical/logical_or.md) |

## decals

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Decal Distance Fade Gradient` | Decal Distance Fade Gradient | yes | fixed | - | ""(id 0):float | - | [Outputs a decal fading value for the projected fragment point, based on the distance from the decal and its radius. The output varies in the [0; 1] range, where 0...](../md_docs/content/materials/graph/node_library/decal/decal_distance_fade_gradient.md) |
| `Decal Material Mask` | Decal Material Mask | yes | fixed | - | ""(id 0):uint | - | [Outputs the Material Mask of the decal.](../md_docs/content/materials/graph/node_library/decal/decal_material_mask.md) |
| `Decal Matrix IProjection` | Decal Matrix IProjection | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the inverse of the decal projection matrix that is defined only for Orthographic and Projected decals. For Mesh decals an identity matrix is returned.](../md_docs/content/materials/graph/node_library/decal/decal_matrix_iprojection.md) |
| `Decal Matrix Projection` | Decal Matrix Projection | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the projection matrix of the decal that is defined only for Orthographic and Projected decals. For Mesh decals an identity matrix is returned.](../md_docs/content/materials/graph/node_library/decal/decal_matrix_projection.md) |
| `Decal Plane` | Decal Plane | yes | fixed | - | ""(id 0):float4 | - | [Outputs the float4 vector that defines the decal plane in the view space (normal-distance).](../md_docs/content/materials/graph/node_library/decal/decal_plane.md) |
| `Decal Projected Normal` | Decal Projected Normal | yes | [4 configurations](#decal-projected-normal) | - | World:float3 | 0:Space=Combobox | [Outputs the normal vector of the projected decal mesh (for Mesh decals) or plane (for Projected and Orthographic decals). The coordinate space of the output value (...](../md_docs/content/materials/graph/node_library/decal/decal_projected_normal.md) |
| `Decal Projected Position` | Decal Projected Position | yes | [4 configurations](#decal-projected-position) | - | Camera World:float3 | 0:Space=Combobox | [Outputs the fragment position of the decal mesh (for Mesh decals) or plane (for Projected and Orthographic decals) corresponding to the fragment after being...](../md_docs/content/materials/graph/node_library/decal/decal_projected_position.md) |
| `Decal Radius` | Decal Radius | yes | fixed | - | ""(id 0):float | - | [Outputs the radius of the decal.](../md_docs/content/materials/graph/node_library/decal/decal_radius.md) |
| `Decal Scene Material Mask` | Decal Scene Material Mask | yes | fixed | - | ""(id 0):uint | - | [Outputs the Material Mask of the scene geometry onto which the decal is projected.](../md_docs/content/materials/graph/node_library/decal/decal_scene_material_mask.md) |
| `Decal Scene Normal` | Decal Scene Normal | yes | [4 configurations](#decal-scene-normal) | - | World:float3 | 0:Space=Combobox | [Outputs the fragment normal vector of the scene geometry before the decal is applied. The coordinate space of the output value ( World, Object, Tangent, View ) can be...](../md_docs/content/materials/graph/node_library/decal/decal_scene_normal.md) |
| `Decal Scene Position` | Decal Scene Position | yes | [4 configurations](#decal-scene-position) | - | Camera World:float3 | 0:Space=Combobox | [Outputs the fragment position of the scene geometry. The coordinate space of the output value ( World, Object, Tangent, View ) can be selected with the Space dropdown...](../md_docs/content/materials/graph/node_library/decal/decal_scene_position.md) |

## mathematic

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `_add` | Add | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the sum of the two input values A and B . Addition between vector data types are done per-component. If A and B have a different number of components, a cast...](../md_docs/content/materials/graph/node_library/math/add.md) |
| `_decrement` | Decrement | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the decremented input (or individual components of the input vector). Decrementing means subtracting 1 from the input value.](../md_docs/content/materials/graph/node_library/math/decrement.md) |
| `_divide` | Divide | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the result of the division of the two input values A and B . The operation for vector data types is done per-component. If A and B have a different number of...](../md_docs/content/materials/graph/node_library/math/divide.md) |
| `_divide_int` | Divide Int | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the integer part of the division result of the two input values A and B . The operation for vector data types is done per-component. If A and B have a...](../md_docs/content/materials/graph/node_library/math/divide_int.md) |
| `_dot_product` | Dot Product | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):float | - | [Outputs the dot product of two vectors A and B , which is the sum of the multiplication of each vectors components. For example, if A and B are 3-component vectors,...](../md_docs/content/materials/graph/node_library/math/dot_product.md) |
| `_increment` | Increment | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the incremented input (or individual components of the input vector). Incrementing means adding 1 to the input value.](../md_docs/content/materials/graph/node_library/math/increment.md) |
| `_mod` | Mod | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the integer remainder of the division of the two input values A and B . The operation for vector data types is done per-component. If A and B have a different...](../md_docs/content/materials/graph/node_library/math/mod.md) |
| `_multiply` | Multiply | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the product of the two input factor values A and B . Multiplication between vector data types is done per-component. If A and B have a different number of...](../md_docs/content/materials/graph/node_library/math/multiply.md) |
| `_subtract` | Subtract | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the subtraction result of the two input values A and B . Subtraction between vector data types are done per-component. If A and B have a different number of...](../md_docs/content/materials/graph/node_library/math/subtract.md) |
| `abs` | Absolute | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the absolute value of an input scalar value or individual components of input vectors. Simply put it removes any negative sign of a value, leaving only the...](../md_docs/content/materials/graph/node_library/math/absolute.md) |
| `acos` | ArcCosine | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the arccosine, in radians, of the input value (or individual components of the input vector). The output will be in the range [0, &#960;] assuming that the...](../md_docs/content/materials/graph/node_library/trigonometry/arccosine.md) |
| `asin` | ArcSine | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the arcsine, in radians, of the input value (or individual components of the input vector). The output will be in the range [-&#960;/2, &#960;/2] assuming...](../md_docs/content/materials/graph/node_library/trigonometry/arcsine.md) |
| `atan` | ArcTangent | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the arctangent, in radians, of the input value (or individual components of the input vector). The output will be in the range [-&#960;/2, &#960;/2] .](../md_docs/content/materials/graph/node_library/trigonometry/arctangent.md) |
| `atan2` | 2-Argument ArcTangent | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the arctangent, in radians, of the division of two input values A and B (or individual components of the input vectors). The output will be in the range...](../md_docs/content/materials/graph/node_library/trigonometry/2argument_arctangent.md) |
| `ceil` | Ceiling | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the smallest integer value, or whole number, that is greater than or equal to the input value. For example: Ceiling(4,2) = 5 Ceiling(-2,5) = -2](../md_docs/content/materials/graph/node_library/math/ceiling.md) |
| `clamp` | Clamp | yes | fixed | Value:undefined, Minimum:undefined, Maximum:undefined | ""(id 1723312480):undefined | - | [Outputs the input value clamped between Min and Max . Min is returned if input is less than Min value is returned if input is between Min and Max Max is returned if...](../md_docs/content/materials/graph/node_library/math/clamp.md) |
| `colorSaturation` | Color Saturation | yes | fixed | Color:float3, Saturation:float | ""(id 1723312480):float3 | - | [This node is used to modify the intensity of the input Color using the Saturation floating value within [0; 1] .](../md_docs/content/materials/graph/node_library/misc/color_saturation.md) |
| `cos` | Cosine | yes | fixed | Radians:undefined | ""(id 1723312480):undefined | - | [Outputs the cosine of the input value (or individual components of the input vector). The input must be in radians.](../md_docs/content/materials/graph/node_library/trigonometry/cosine.md) |
| `cosh` | Hyperbolic Cosine | yes | fixed | Radians:undefined | ""(id 1723312480):undefined | - | [Outputs the hyperbolic cosine of the input value (or individual components of the input vector). The input must be in radians.](../md_docs/content/materials/graph/node_library/trigonometry/hyperbolic_cosine.md) |
| `cross` | Cross | yes | fixed | Vector 0:float3, Vector 1:float3 | ""(id 1723312480):float3 | - | [This node computes the cross product of two float3 vectors A and B , resulting in a vector that is perpendicular to both and serves as the normal to the plane they...](../md_docs/content/materials/graph/node_library/math/cross.md) |
| `ddx` | DDX | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [This node outputs the partial derivatives of the specified input value with respect to the screen space x-coordinate. For more information on how the derivatives are...](../md_docs/content/materials/graph/node_library/math/ddx.md) |
| `ddx_coarse` | DDX Coarse | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [This node outputs a low precision partial derivative of the specified input value with respect to the screen space x-coordinate. For more information on how the...](../md_docs/content/materials/graph/node_library/math/ddx_coarse.md) |
| `ddx_fine` | DDX Fine | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [This node outputs a high precision partial derivative of the specified input value with respect to the screen space x-coordinate. For more information on how the...](../md_docs/content/materials/graph/node_library/math/ddx_fine.md) |
| `ddxy` | DDXY | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [This node outputs the sum of both partial derivatives of the specified input value with respect to the screen space x-coordinate and screen-space y-coordinate...](../md_docs/content/materials/graph/node_library/math/ddxy.md) |
| `ddy` | DDY | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [This node outputs the partial derivatives of the specified input value with respect to the screen space y-coordinate. For more information on how the derivatives are...](../md_docs/content/materials/graph/node_library/math/ddy.md) |
| `ddy_coarse` | DDY Coarse | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [This node outputs a low precision partial derivative of the specified input value with respect to the screen space y-coordinate. For more information on how the...](../md_docs/content/materials/graph/node_library/math/ddy_coarse.md) |
| `ddy_fine` | DDY Fine | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [This node outputs a high precision partial derivative of the specified input value with respect to the screen space y-coordinate. For more information on how the...](../md_docs/content/materials/graph/node_library/math/ddy_fine.md) |
| `exp` | Base-E Exponential | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Returns e raised to the specified power ( e value ).](../md_docs/content/materials/graph/node_library/math/basee_exponential.md) |
| `exp2` | Base-2 Exponential | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Returns 2 raised to the specified power ( 2 value ).](../md_docs/content/materials/graph/node_library/math/base2_exponential.md) |
| `faceforward` | Face Forward | yes | fixed | N:undefined, I:undefined, Ng:undefined | ""(id 1723312480):undefined | - | [Outputs a floating-point, surface normal vector that is facing the view direction. This node actually flips the surface-normal (if needed) to face in a direction...](../md_docs/content/materials/graph/node_library/misc/face_forward.md) |
| `floor` | Floor | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the largest integer value, or a whole number, that is less than or equal to the input value. For example: Floor(4,2) = 4 Floor(-2,5) = -3](../md_docs/content/materials/graph/node_library/math/floor.md) |
| `fmod` | FMod | yes | fixed | Dividend:undefined, Divisor:undefined | ""(id 1723312480):undefined | - | [Outputs the floating point remainder of the division of the two input values A and B . The operation for vector data types is done per-component. If A and B have a...](../md_docs/content/materials/graph/node_library/math/fmod.md) |
| `frac` | Frac | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - |  |
| `length` | Length | yes | fixed | Vector:undefined | ""(id 1723312480):float | - | [Outputs the euclidean length of the input vector which is the result of the following operation: Sqrt ( Dot ( Input, Input )) .](../md_docs/content/materials/graph/node_library/math/length.md) |
| `log` | Base-E Logarithm | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the natural logarithm of the input (or individual components of input vectors). The natural logarithm is also called base-e logarithm.](../md_docs/content/materials/graph/node_library/math/basee_logarithm.md) |
| `log10` | Base-10 Logarithm | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the base-10 logarithm of the input (or individual components of the input vector).](../md_docs/content/materials/graph/node_library/math/base10_logarithm.md) |
| `log2` | Base-2 Logarithm | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the base-2 logarithm of the input (or individual components of the input vector).](../md_docs/content/materials/graph/node_library/math/base2_logarithm.md) |
| `mad` | Multiply And Add | yes | fixed | Mvalue:undefined, Avalue:undefined, Bvalue:undefined | ""(id 1723312480):undefined | - | [Performs the M * A + B operation with input values M , A , and B .](../md_docs/content/materials/graph/node_library/math/multiply_and_add.md) |
| `max` | Maximum | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the bigger of the two input values A and B . Comparison between vector data types are done per-component. If A and B have a different number of components, a...](../md_docs/content/materials/graph/node_library/math/maximum.md) |
| `min` | Minimum | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Outputs the minimum of the two input values A and B . Comparison between vector data types are done per-component. If A and B have a different number of components, a...](../md_docs/content/materials/graph/node_library/math/minimum.md) |
| `modf` | ModF | yes | fixed | Value:undefined | Ip:undefined, ""(id 1723312480):undefined | - | [Splits a floating-point value into fractional and integer parts.](../md_docs/content/materials/graph/node_library/math/modf.md) |
| `normalize` | Normalize | yes | fixed | Vector:undefined | ""(id 1723312480):undefined | - | [This node is used to normalize an input vector, ensuring that it has a length of exactly 1 while maintaining its original direction. Normalization is crucial in...](../md_docs/content/materials/graph/node_library/math/normalize.md) |
| `overlay` | Overlay | yes | fixed | A:undefined, B:undefined, Coefficient:undefined | ""(id 1723312480):undefined | - | [The node performs the overlay of B over A with the blending coefficient in the range [0.0, 1.0]. Thus, with the coefficient of 0.0, the output will be A , and with...](../md_docs/content/materials/graph/node_library/misc/overlay.md) |
| `pow` | Power | yes | fixed | Value:undefined, Power:undefined | ""(id 1723312480):undefined | - | [Outputs Value to the Power -th power of the input scalars and vectors. With Power > 0 it corresponds to multiplying Value by itself Power times, e.g. Value = 2, Power...](../md_docs/content/materials/graph/node_library/math/power.md) |
| `rcp` | Reciprocal | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the reciprocal (multiplicative inverse) of the input. The operation for vector data types is done per-component.](../md_docs/content/materials/graph/node_library/math/reciprocal.md) |
| `reflect` | Reflect | yes | fixed | Incident:undefined, Normal:undefined | ""(id 1723312480):undefined | - | [Returns the reflection of the Incident vector off the surface defined by the Normal vector.](../md_docs/content/materials/graph/node_library/misc/reflect.md) |
| `refract` | Refract | yes | fixed | Ray Direction:undefined, Normal:undefined, Refraction Index:float | ""(id 1723312480):undefined | - | [Returns the refraction vector for the given Ray Direction vector, surface defined by the Normal vector and the Refraction Index . The Refraction Index is the ratio of...](../md_docs/content/materials/graph/node_library/misc/refract.md) |
| `round` | Round | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Rounds the input scalar or individual vector components to the nearest integer value.](../md_docs/content/materials/graph/node_library/math/round.md) |
| `rsqrt` | Reciprocal Square Root | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the reciprocal square root of the input value (or individual components of the input vector). The operation can be viewed as the inverse square root:...](../md_docs/content/materials/graph/node_library/math/reciprocal_square_root.md) |
| `saturate` | Saturate | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the input value clamped between 0 and 1 . 0 is returned if input is less than 0 value is returned if input is between 0 and 1 1 is returned if input is...](../md_docs/content/materials/graph/node_library/math/saturate.md) |
| `sign` | Sign | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs one, zero, or negative one according to the sign of the input scalar value or individual components of input vectors. 1 is returned if input is positive 0 is...](../md_docs/content/materials/graph/node_library/math/sign.md) |
| `sin` | Sine | yes | [2 configurations](#sin) | Radians:undefined | ""(id 1723312480):undefined | 0:Mode=Combobox | **The `Out(sin,cos)` configuration does not compile.** Use `In(radians) Out(return)` and a separate `cos` node. [Outputs the sine of the input value (or individual components of the input vector). The input must be in radians.](../md_docs/content/materials/graph/node_library/trigonometry/sine.md) |
| `sinh` | Hyperbolic Sine | yes | fixed | Radians:undefined | ""(id 1723312480):undefined | - | [Outputs the hyperbolic sine of the input value (or individual components of the input vector). The input must be in radians.](../md_docs/content/materials/graph/node_library/trigonometry/hyperbolic_sine.md) |
| `smoothstep` | Smooth Step | yes | fixed | Minimum:undefined, Maximum:undefined, Value:undefined | ""(id 1723312480):undefined | - | [Assuming that Max value is greater than Min : If input is less than Min then a value 0 is returned If input value is in the [ Min , Max ] range then a smooth Hermite...](../md_docs/content/materials/graph/node_library/math/smooth_step.md) |
| `sqrt` | Square Root | yes | fixed | Value:undefined | ""(id 1723312480):undefined | - | [Outputs the square root of the input value (or individual components of the input vector).](../md_docs/content/materials/graph/node_library/math/square_root.md) |
| `srgb` | Srgb | yes | fixed | Color:undefined | ""(id 1723312480):undefined | - | [This node converts RGB (Red, Green, Blue) color values to sRGB (standard RGB) format, which is in fact raising a value to the power of 2.2.](../md_docs/content/materials/graph/node_library/misc/srgb.md) |
| `srgbInv` | Srgb Inverse | yes | fixed | Color:undefined | ""(id 1723312480):undefined | - | [This node converts sRGB (standard RGB) color values to RGB (Red, Green, Blue) format, which is in fact raising a value to the power of 1/2.2.](../md_docs/content/materials/graph/node_library/misc/srgb_inverse.md) |
| `step` | Step | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Implements a step function: Outputs 1 if a value or vector component of A is less or equal than the value or corresponding vector component of B Outputs 0 if a value...](../md_docs/content/materials/graph/node_library/math/step.md) |
| `tan` | Tangent | yes | fixed | Radians:undefined | ""(id 1723312480):undefined | - | [Outputs the tangent of the input value (or individual components of the input vector). The input must be in radians.](../md_docs/content/materials/graph/node_library/trigonometry/tangent.md) |

## matrices

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Matrix Absolute World To Object` | Matrix Absolute World To Object | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the matrix for a transformation from Absolute World to Object coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_absolute_world_to_object.md) |
| `Matrix Absolute World To View` | Matrix Absolute World To View | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the matrix for a transformation from Absolute World to View coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_absolute_world_to_view.md) |
| `Matrix Camera IProjection` | Matrix Camera IProjection | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the inverse of the Projection matrix of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/matrix_camera_iprojection.md) |
| `Matrix Camera Projection` | Matrix Camera Projection | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the Projection matrix of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/matrix_camera_projection.md) |
| `Matrix Camera World To Object` | Matrix Camera World To Object | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the matrix for a transformation from Camera World To Object coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_camera_world_to_object.md) |
| `Matrix Camera World To View` | Matrix Camera World To View | yes | fixed | - | ""(id 0):float3x3 | - | [Outputs the matrix for a transformation from Camera World To View coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_camera_world_to_view.md) |
| `Matrix IModelview` | Matrix IModelview | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the inverse of the Model-View matrix of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/matrix_imodelview.md) |
| `Matrix IProjection` | Matrix IProjection | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the inverse of the Projection matrix currently being used for rendering. For example: post have ortographic projection, but camera projection is...](../md_docs/content/materials/graph/node_library/input/matrix_iprojection.md) |
| `Matrix Modelview` | Matrix Modelview | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the Model-View matrix of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/matrix_modelview.md) |
| `Matrix Object To Absolute World` | Matrix Object To Absolute World | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the matrix for a transformation from Object to Absolute World coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_object_to_absolute_world.md) |
| `Matrix Object To Camera World` | Matrix Object To Camera World | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the matrix for a transformation from Object to Camera World coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_object_to_camera_world.md) |
| `Matrix Object To View` | Matrix Object To View | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the matrix for a transformation from Object to View coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_object_to_view.md) |
| `Matrix Old IModelview` | Matrix Old IModelview | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the inverse of the Old Model-View matrix of the camera used for rendering of the previous frame.](../md_docs/content/materials/graph/node_library/input/matrix_old_imodelview.md) |
| `Matrix Old IModelview Delta` | Matrix Old IModelview Delta | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the delta of the Old Inverse Model-View and Inverse Model-View matrices of the camera used for rendering.](../md_docs/content/materials/graph/node_library/input/matrix_old_imodelview_delta.md) |
| `Matrix Old Modelview` | Matrix Old Modelview | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the Old Model-View matrix of the camera used for rendering of the previous frame.](../md_docs/content/materials/graph/node_library/input/matrix_old_modelview.md) |
| `Matrix Projection` | Matrix Projection | yes | fixed | - | ""(id 0):float4x4 | - | [Provides access to the Projection matrix currently being used for rendering. For example: post have ortographic projection, but camera projection is perspective.](../md_docs/content/materials/graph/node_library/input/matrix_projection.md) |
| `Matrix View To Absolute World` | Matrix View To Absolute World | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the matrix for a transformation from View to Absolute World coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_view_to_absolute_world.md) |
| `Matrix View To Camera World` | Matrix View To Camera World | yes | fixed | - | ""(id 0):float3x3 | - | [Outputs the matrix for a transformation from View to Camera World coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_view_to_camera_world.md) |
| `Matrix View To Object` | Matrix View To Object | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the matrix for a transformation from View to Object coordinates.](../md_docs/content/materials/graph/node_library/matrix/matrix_view_to_object.md) |
| `_get_matrix_column` | Get Matrix Column | yes | fixed | Matrix:undefined, Index:int | ""(id 1723312480):undefined | - | [Outputs the elements located in the given column of the matrix.](../md_docs/content/materials/graph/node_library/matrix/get_matrix_column.md) |
| `_get_matrix_row` | Get Matrix Row | yes | fixed | Matrix:undefined, Index:int | ""(id 1723312480):undefined | - | [Outputs the elements located in the given row of the matrix.](../md_docs/content/materials/graph/node_library/matrix/get_matrix_row.md) |
| `_get_matrix_value` | Get Matrix Value | yes | fixed | Matrix:undefined, X:int, Y:int | ""(id 1723312480):float | - | [Outputs the value located in the given row and column of the matrix.](../md_docs/content/materials/graph/node_library/matrix/get_matrix_value.md) |
| `_set_matrix_column` | Set Matrix Column | yes | fixed | Matrix:undefined, Index:int, Value:undefined | Matrix:undefined | - | [Sets values to the elements located in the given column of the matrix.](../md_docs/content/materials/graph/node_library/matrix/set_matrix_column.md) |
| `_set_matrix_row` | Set Matrix Row | yes | fixed | Matrix:undefined, Index:int, Value:undefined | Matrix:undefined | - | [Sets values to the elements located in the given row of the matrix.](../md_docs/content/materials/graph/node_library/matrix/set_matrix_row.md) |
| `_set_matrix_value` | Set Matrix Value | yes | fixed | Matrix:undefined, X:int, Y:int, Value:float | Matrix:undefined | - | [Sets the given value to the element located in the given row and column of the matrix.](../md_docs/content/materials/graph/node_library/matrix/set_matrix_value.md) |
| `basisX` | Basis X | yes | fixed | M:undefined | ""(id 1723312480):undefined | - | [Outputs the X-basis of the input 3x3 matrix.](../md_docs/content/materials/graph/node_library/matrix/basis_x.md) |
| `basisY` | Basis Y | yes | fixed | M:undefined | ""(id 1723312480):undefined | - | [Outputs the Y-basis of the input 3x3 matrix.](../md_docs/content/materials/graph/node_library/matrix/basis_y.md) |
| `basisZ` | Basis Z | yes | fixed | M:undefined | ""(id 1723312480):float3 | - | [Outputs the Z-basis of the input 3x3 matrix.](../md_docs/content/materials/graph/node_library/matrix/basis_z.md) |
| `composeTransform` | Compose Transform | yes | fixed | Position:float3, Rotation:float3x3, Scale:float3 | ""(id 1723312480):float4x4 | - | [Outputs the transformation matrix composed from the input position, rotation, and scale components.](../md_docs/content/materials/graph/node_library/matrix/compose_transform.md) |
| `cubeTransform` | Cube Transform | yes | fixed | Face:int | ""(id 1723312480):float3x3 | - | [Outputs the cube viewing matrix for the input cube face from 0 to 5: 0 &#8212; positive X face (right) 1 &#8212; negative X face (left) 2 &#8212; positive Y face...](../md_docs/content/materials/graph/node_library/matrix/cube_transform.md) |
| `decomposeEuler` | Decompose Euler | yes | fixed | Matrix:float3x3 | ""(id 1723312480):float3 | - | [Decomposes the input rotation matrix to the output vector of Euler angles (pitch, roll, yaw). The Euler angles are specified in the axis rotation sequence - XYZ. It...](../md_docs/content/materials/graph/node_library/matrix/decompose_euler.md) |
| `decomposeTransform` | Decompose Transform | yes | fixed | Transform:float4x4 | Position:float3, Rotation:float3x3, Scale:float3 | - | [Decomposes the input transformation matrix into the position, rotation, and scale components.](../md_docs/content/materials/graph/node_library/matrix/decompose_transform.md) |
| `determinant` | Determinant | yes | fixed | Matrix:undefined | ""(id 1723312480):float | - | [Returns the determinant of the given matrix.](../md_docs/content/materials/graph/node_library/matrix/determinant.md) |
| `frustum` | Frustum | yes | fixed | L:float, R:float, B:float, T:float, N:float, F:float | ""(id 1723312480):float4x4 | - | [Outputs the perspective projection matrix: 2.0 * znear / (right - left) 0.0 (right + left) / (right - left) 0.0 0.0 2.0 * znear / (top - bottom) (top + bottom) / (top...](../md_docs/content/materials/graph/node_library/matrix/frustum.md) |
| `inverse` | Inverse | yes | fixed | Matrix:float4x4 | ""(id 1723312480):float4x4 | - | [Returns inverse of a matrix. The inverse of a matrix is a matrix that if multiplied by the original would result in identity matrix: AA -1 = A -1 A = I.](../md_docs/content/materials/graph/node_library/matrix/inverse.md) |
| `inverseTransform` | Inverse Transform | yes | fixed | Matrix:float4x4 | ""(id 1723312480):float4x4 | - | [Inverts a matrix that consists of a 3x4 sub-matrix (upper left) and a translation vector. The last row of the matrix is ignored. Compared to the Inverse node, this...](../md_docs/content/materials/graph/node_library/matrix/inverse_transform.md) |
| `matrix2` | Matrix2 | yes | fixed | M00:float, M10:float, M01:float, M11:float | ""(id 1723312480):float2x2 | - | [Creates a 2x2 matrix from 4 float values.](../md_docs/content/materials/graph/node_library/matrix/matrix2.md) |
| `matrix2Col` | Compose Matrix2 By Column | yes | fixed | Coll 0:float2, Coll 1:float2 | ""(id 1723312480):float2x2 | - | [Creates a 2x2 matrix from vectors by placing them at the matrix columns.](../md_docs/content/materials/graph/node_library/matrix/compose_matrix2_by_column.md) |
| `matrix2Row` | Compose Matrix2 By Row | yes | fixed | Row 0:float2, Row 1:float2 | ""(id 1723312480):float2x2 | - | [Creates a 2x2 matrix from vectors by placing them at the matrix rows.](../md_docs/content/materials/graph/node_library/matrix/compose_matrix2_by_row.md) |
| `matrix3` | Compose Matrix3 | yes | fixed | M00:float, M10:float, M20:float, M01:float, M11:float, M21:float, M02:float, M12:float, M22:float | ""(id 1723312480):float3x3 | - | [Creates a 3x3 matrix from 9 float values.](../md_docs/content/materials/graph/node_library/matrix/compose_matrix3.md) |
| `matrix3Col` | Compose Matrix3 By Column | yes | fixed | Coll 0:float3, Coll 1:float3, Coll 2:float3 | ""(id 1723312480):float3x3 | - | [Creates a 3x3 matrix from vectors by placing them at the matrix columns.](../md_docs/content/materials/graph/node_library/matrix/compose_matrix3_by_column.md) |
| `matrix3Row` | Compose Matrix3 By Row | yes | fixed | Row 0:float3, Row 1:float3, Row 2:float3 | ""(id 1723312480):float3x3 | - | [Creates a 3x3 matrix from vectors by placing them at the matrix rows.](../md_docs/content/materials/graph/node_library/matrix/compose_matrix3_by_row.md) |
| `matrix4` | Compose Matrix4 | yes | fixed | M00:float, M10:float, M20:float, M30:float, M01:float, M11:float, M21:float, M31:float, M02:float, M12:float, M22:float, M32:float, M03:float, M13:float, M23:float, M33:float | ""(id 1723312480):float4x4 | - | [Creates a 4x4 matrix from 16 float values.](../md_docs/content/materials/graph/node_library/matrix/compose_matrix4.md) |
| `matrix4Col` | Compose Matrix4 By Column | yes | [2 configurations](#matrix4col) | Coll 0:float3, Coll 1:float3, Coll 2:float3 | ""(id 1723312480):float4x4 | 0:Mode=Combobox | [Creates a 4x4 matrix from vectors by placing them at the matrix columns.](../md_docs/content/materials/graph/node_library/matrix/compose_matrix4_by_column.md) |
| `matrix4Row` | Compose Matrix4 By Row | yes | [2 configurations](#matrix4row) | Row 0:undefined, Row 1:undefined, Row 2:undefined | ""(id 1723312480):float4x4 | 0:Mode=Combobox | [Creates a 4x4 matrix from vectors by placing them at the matrix rows.](../md_docs/content/materials/graph/node_library/matrix/compose_matrix4_by_row.md) |
| `mul3` | Matrix Multiply 3x3 | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Multiplies two 3x3 matrices.](../md_docs/content/materials/graph/node_library/matrix/matrix_multiply_3x3.md) |
| `mul4` | Matrix Multiply 4x4 | yes | fixed | A:undefined, B:undefined | ""(id 1723312480):undefined | - | [Multiplies two 4x4 matrices.](../md_docs/content/materials/graph/node_library/matrix/matrix_multiply_4x4.md) |
| `ortho` | Ortho | yes | fixed | L:float, R:float, B:float, T:float, N:float, F:float | ""(id 1723312480):float4x4 | - | [Outputs the parallel projection matrix: 2.0 / (right - left) 0.0 0.0 -(right + left) / (right - left) 0.0 2.0 / (top - bottom) 0.0 -(top + bottom) / (top - bottom)...](../md_docs/content/materials/graph/node_library/matrix/ortho.md) |
| `orthonormalize` | Orthonormalize | yes | [2 configurations](#orthonormalize) | Matrix:float3x3 | ""(id 1723312480):float3x3 | 0:Mode=Combobox | [Outputs the orthogonal matrix for the input one.](../md_docs/content/materials/graph/node_library/matrix/orthonormalize.md) |
| `perspective` | Perspective | yes | fixed | Fov:float, Aspect:float, N:float, F:float | ""(id 1723312480):float4x4 | - | [Outputs the perspective projection matrix.](../md_docs/content/materials/graph/node_library/matrix/perspective.md) |
| `rotateX` | Rotate X | yes | fixed | Angle:float | ""(id 1723312480):float3x3 | - | [Outputs the rotation matrix for the input angle, in degrees, around the X-axis.](../md_docs/content/materials/graph/node_library/matrix/rotate_x.md) |
| `rotateY` | Rotate Y | yes | fixed | Angle:float | ""(id 1723312480):float3x3 | - | [Outputs the rotation matrix for the input angle, in degrees, around the Y-axis.](../md_docs/content/materials/graph/node_library/matrix/rotate_y.md) |
| `rotateZ` | Rotate Z | yes | fixed | Angle:float | ""(id 1723312480):float3x3 | - | [Outputs the rotation matrix for the input angle, in degrees, around the Z-axis.](../md_docs/content/materials/graph/node_library/matrix/rotate_z.md) |
| `scale` | Scale | yes | [2 configurations](#scale) | Value:float3 | ""(id 1723312480):float3x3 | 0:Mode=Combobox | [Outputs the scaling matrix for the input scaling vector (X, Y, Z).](../md_docs/content/materials/graph/node_library/matrix/scale.md) |
| `translate` | Translate | yes | [2 configurations](#translate) | Position:float3 | ""(id 1723312480):float4x4 | 0:Mode=Combobox | [Outputs the translation matrix for the input Position vector (X, Y, Z).](../md_docs/content/materials/graph/node_library/matrix/translate.md) |
| `transpose` | Transpose | yes | fixed | Matrix:undefined | ""(id 1723312480):undefined | - | [Transposes the given matrix.](../md_docs/content/materials/graph/node_library/matrix/transpose.md) |

## noises and patterns

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `bayerNoise` | Bayer Noise | yes | fixed | Coord:undefined | ""(id 1723312480):float | - | [This node generates Bayer noise based on input coords using a 4x4 constant Bayer pattern.](../md_docs/content/materials/graph/node_library/procedural/bayer_noise.md) |
| `blueNoise` | Blue Noise | yes | fixed | Coord:undefined | ""(id 1723312480):float4 | - | [This node generates blue noise based on input coords using a 16x16 constant blue noise array.](../md_docs/content/materials/graph/node_library/procedural/blue_noise.md) |
| `blueNoiseTAA` | Blue Noise TAA | yes | fixed | Coord:undefined, Num Frame:uint | ""(id 1723312480):float4 | - | [This node generates blue noise based on input coords using a 16x16 constant blue noise array. You can specify the number of frames for the noise to change. It is a...](../md_docs/content/materials/graph/node_library/procedural/blue_noise_taa.md) |
| `blueNoiseTemporal` | Blue Noise Temporal | yes | fixed | Coord:undefined, Num Frame:uint | ""(id 1723312480):float4 | - | [This node generates blue noise based on input coords using a 16x16 constant blue noise array. You can specify the number of frames for the noise to change. It is a...](../md_docs/content/materials/graph/node_library/procedural/blue_noise_temporal.md) |
| `hammersley` | Hammersley | yes | fixed | I:uint, Num:uint | ""(id 1723312480):float2 | - | [Outputs X and Y coordinates of a point with the Index index in a Hammersley Point Set that describes uniform distribution of points in the [0; 1] range. Index - index...](../md_docs/content/materials/graph/node_library/procedural/hammersley.md) |
| `vogelDisk` | Vogel Disk | yes | [2 configurations](#vogeldisk) | I:uint, Count:uint | ""(id 1723312480):float2 | 0:Mode=Combobox | [Generates a set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside. Count - number of points...](../md_docs/content/materials/graph/node_library/procedural/vogel_disk.md) |

## packing

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `pack1212To888` | Pack1212To888 | yes | fixed | Value:float2 | ""(id 1723312480):float3 | - |  |
| `pack1616To8888` | Pack1616To8888 | yes | fixed | Value:float2 | ""(id 1723312480):float4 | - |  |
| `pack16To88` | Pack16To88 | yes | fixed | Value:float | ""(id 1723312480):float2 | - |  |
| `pack44To8` | Pack44To8 | yes | fixed | A:float, B:float | ""(id 1723312480):float | - |  |
| `pack8888To1616` | Pack8888To1616 | yes | fixed | Value:float4 | ""(id 1723312480):float2 | - |  |
| `pack888To1212` | Pack888To1212 | yes | fixed | Value:float3 | ""(id 1723312480):float2 | - |  |
| `pack88To16` | Pack88To16 | yes | fixed | Value:float2 | ""(id 1723312480):float | - |  |
| `pack8To44` | Pack8To44 | yes | fixed | Value:float | ""(id 1723312480):float2 | - |  |
| `packUnitVectorToOctahedron` | Pack Unit Vector To Octahedron | yes | fixed | Normal:float3 | ""(id 1723312480):float2 | - | [Encodes a normal (unit) vector into two-component one using octahedron encoding.](../md_docs/content/materials/graph/node_library/misc/pack_unit_vector_to_octahedron.md) |
| `unpackOctahedronToUnitVector` | Unpack Octahedron To Unit Vector | yes | fixed | Octahedron:float2 | ""(id 1723312480):float3 | - | [Decodes an octahedron vector into three-component normal (unit) one.](../md_docs/content/materials/graph/node_library/misc/unpack_octahedron_to_unit_vector.md) |

## portals

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `PortalIn` | Portal In | yes | fixed | ""(id 0):undefined | - | 0:Name=String · 1:Color=Color | [This node enables you to create a portal entrance (you can specify a name and color for it). When working with complex or large graphs, you may end up with your wires...](../md_docs/content/materials/graph/node_library/misc/portal_in.md) |
| `PortalOut` | Portal Out | yes | fixed | - | ""(id 0):undefined | 0:Portal=Combobox | [This node enables you to create a portal exit (you can select one of the existing Portal In entrances to connect to). When working with complex or large graphs, you...](../md_docs/content/materials/graph/node_library/misc/portal_out.md) |

## screen_parameters

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Screen Coord` | Screen Coord | yes | fixed | - | ""(id 0):uint2 | - | [Provides access to the position in the Screen Space Coordinates .](../md_docs/content/materials/graph/node_library/input/screen_coord.md) |
| `Screen IResolution` | Screen IResolution | yes | fixed | - | ""(id 0):float2 | - | [Provides access to the reciprocal Screen Resolution (1/width, 1/height) currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/screen_iresolution.md) |
| `Screen Resolution` | Screen Resolution | yes | fixed | - | ""(id 0):uint2 | - | [Provides access to the Screen Resolution (width, height), in pixels, currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/screen_resolution.md) |
| `Screen UV` | Screen UV | yes | fixed | - | ""(id 0):float2 | - | [Provides access to the position in the Screen UV coordinates. The output represent the Screen Coord node output normalized in the [0, 1] range. This node is useful...](../md_docs/content/materials/graph/node_library/input/screen_uv.md) |

## settings

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Settings Environment Ambient Intensity` | Settings Environment Ambient Intensity | yes | fixed | - | ""(id 0):float | - | [Outputs the Environment ambient intensity parameter.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Environment Reflection Intensity` | Settings Environment Reflection Intensity | yes | fixed | - | ""(id 0):float | - | [Outputs the Environment reflection intensity parameter.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Environment Sky Intensity` | Settings Environment Sky Intensity | yes | fixed | - | ""(id 0):float | - | [Outputs the Sky intensity parameter.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Color` | Settings Haze Color | yes | fixed | - | ""(id 0):float4 | - | [Outputs the color of the haze.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Density` | Settings Haze Density | yes | fixed | - | ""(id 0):float | - | [Outputs the haze density.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Gradient` | Settings Haze Gradient | yes | fixed | - | ""(id 0):float | - | [Outputs the Environment haze gradient.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Maximum Distance` | Settings Haze Maximum Distance | yes | fixed | - | ""(id 0):float | - | [Outputs the Haze maximum visible distance.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical` | Settings Haze Physical | yes | fixed | - | ""(id 0):float | - | [Outputs 1 if the Environment Haze Mode is set to Physical , otherwise &#8212; 0 .](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Ambient Color Saturation` | Settings Haze Physical Ambient Color Saturation | yes | fixed | - | ""(id 0):float | - | [Outputs the Intensity of the ambient color's contribution to the haze.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Ambient Light Intensity` | Settings Haze Physical Ambient Light Intensity | yes | fixed | - | ""(id 0):float | - | [Outputs the Intensity of the impact of the ambient lighting on haze.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Density` | Settings Haze Physical Density | yes | fixed | - | ""(id 0):float | - | [Outputs the Haze density for the Physical preset.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Falloff` | Settings Haze Physical Falloff | yes | fixed | - | ""(id 0):float | - | [Outputs the Height of the haze density gradient.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Start Height` | Settings Haze Physical Start Height | yes | fixed | - | ""(id 0):float | - | [Outputs the Reference height value for the two parameters (Half Visibility Distance and Haze Physical Falloff).](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Sun Color Saturation` | Settings Haze Physical Sun Color Saturation | yes | fixed | - | ""(id 0):float | - | [Outputs the Intensity of the impact of the sunlight on haze.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Sun Light Intensity` | Settings Haze Physical Sun Light Intensity | yes | fixed | - | ""(id 0):float | - | [Outputs the Intensity of the impact of the sunlight on haze.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Zero Visibility Height` | Settings Haze Physical Zero Visibility Height | yes | fixed | - | ""(id 0):float | - | [Outputs the height at which the haze completely overlaps the scene.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Scattering Mie Fresnel Power` | Settings Haze Scattering Mie Fresnel Power | yes | fixed | - | ""(id 0):float | - | [Outputs the Power of the Fresnel effect for Mie visibility.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Scattering Mie Intensity` | Settings Haze Scattering Mie Intensity | yes | fixed | - | ""(id 0):float | - | [Outputs the Minimum Mie intensity value for geometry-occluded areas.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Solid` | Settings Haze Solid | yes | fixed | - | ""(id 0):float | - | [Outputs 1 if the Environment Haze Mode is set to Solid , otherwise &#8212; 0 .](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Visibility` | Settings Haze Visibility | yes | fixed | - | ""(id 0):float | - | [Outputs 1 if haze is enabled, otherwise &#8212; 0 .](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Matrix Moon Rotation` | Settings Matrix Moon Rotation | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the moon rotation matrix.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Matrix Sky Transform` | Settings Matrix Sky Transform | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the sky transform matrix.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Matrix Sun Rotation` | Settings Matrix Sun Rotation | yes | fixed | - | ""(id 0):float4x4 | - | [Outputs the sun rotation matrix.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Render Translucent Color` | Settings Render Translucent Color | yes | fixed | - | ""(id 0):float4 | - | [Outputs the current Translucent Color.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Sky Altitude` | Settings Sky Altitude | yes | fixed | - | ""(id 0):float | - | [Outputs the sky altitude.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Sky Up` | Settings Sky Up | yes | [4 configurations](#settings-sky-up) | - | World:float3 | 0:Space=Combobox | [Outputs the sky up vector. The coordinate space of the output value ( World, Object, Tangent, View ) can be selected with the Space dropdown parameter (double-click...](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Supersampling` | Settings Supersampling | yes | fixed | - | ""(id 0):float | - | [Outputs the current Number of samples per pixel used for supersampling.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings TAA` | Settings TAA | yes | fixed | - | ""(id 0):float | - | [Outputs 1 if Temporal Anti-Aliasing is enabled, otherwise &#8212; 0 .](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Tessellation Density Multiplier` | Settings Tessellation Density Multiplier | yes | fixed | - | ""(id 0):float | - | [Outputs the global density multiplier for the adaptive hardware-accelerated tessellation.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Tessellation Distance Multiplier` | Settings Tessellation Distance Multiplier | yes | fixed | - | ""(id 0):float | - | [Outputs the global multiplier for all distance parameters of the adaptive hardware-accelerated tessellation used for distance-dependent optimization.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Tessellation Shadow Density Multiplier` | Settings Tessellation Shadow Density Multiplier | yes | fixed | - | ""(id 0):float | - | [Outputs the global Shadow Density multiplier for the Tessellated Displacement effect.](../md_docs/content/materials/graph/node_library/input/settings.md) |

## sky

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Moon Direction` | Moon Direction | yes | [4 configurations](#moon-direction) | - | World:float3 | 0:Space=Combobox | [Provides access to the direction vector of the World light source having the Moon scattering mode and currently used in the scene. If the scene doesn't have such a...](../md_docs/content/materials/graph/node_library/input/moon_direction.md) |
| `Sun Direction` | Sun Direction | yes | [4 configurations](#sun-direction) | - | World:float3 | 0:Space=Combobox | [Provides access to the direction vector of the World light source having the Sun scattering mode and currently used in the scene. If the scene doesn't have such a...](../md_docs/content/materials/graph/node_library/input/sun_direction.md) |

## texture

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Auto Exposure` | Texture Buffer Auto Exposure | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_auto_exposure.md) |
| `Auto White Balance` | Texture Buffer Auto White Balance | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_auto_white_balance.md) |
| `Auxiliary` | Texture Buffer Auxiliary | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_auxiliary.md) |
| `Bent Normal` | Texture Buffer Bent Normal | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_bent_normal.md) |
| `Clouds Screen` | Texture Buffer Clouds Screen | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_clouds_screen.md) |
| `Curvature` | Texture Buffer Curvature | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_curvature.md) |
| `DOF Mask` | Texture Buffer DOF Mask | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_dof_mask.md) |
| `Depth` | Texture Buffer Depth | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_depth.md) |
| `Depth Opacity` | Texture Buffer Depth Opacity | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_depth_opacity.md) |
| `Depth Opacity Fast` | Texture Buffer Depth Opacity Fast | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_depth_opacity_fast.md) |
| `GBuffer Albedo` | Texture Buffer GBuffer Albedo | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_gbuffer_albedo.md) |
| `GBuffer Normal` | Texture Buffer GBuffer Normal | yes | fixed | - | ""(id 0):Texture2D | - | The normals in this buffer are in **view space**. Core converts with `mul3(s_imodelview, n)` immediately after unpacking them. [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_gbuffer_normal.md) |
| `GBuffer Shading` | Texture Buffer GBuffer Shading | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_gbuffer_shading.md) |
| `GBuffer Velocity` | Texture Buffer GBuffer Velocity | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_gbuffer_velocity.md) |
| `LightMapTexture` | Light Map Texture | yes | fixed | - | ""(id 0):Texture2D | - | [This node represents a 2D light map texture, that is assigned to an object's surface in the Texture field of the Lightmaps group. The advantage of this texture is...](../md_docs/content/materials/graph/node_library/textures/light_map_texture.md) |
| `Normal Fast` | Texture Buffer Normal Fast | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_normal_fast.md) |
| `Refraction` | Texture Buffer Refraction | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_refraction.md) |
| `Refraction Mask` | Texture Buffer Refraction Mask | yes | fixed | - | ""(id 0):Texture2DInt | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_refraction_mask.md) |
| `SSAO` | Texture Buffer SSAO | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_ssao.md) |
| `SSGI` | Texture Buffer SSGI | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_ssgi.md) |
| `SSR` | Texture Buffer SSR | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_ssr.md) |
| `Screen Color` | Texture Buffer Screen Color | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_screen_color.md) |
| `Screen Color Old` | Texture Buffer Screen Color Old | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_screen_color_old.md) |
| `Screen Color Old Reprojection` | Texture Buffer Screen Color Old Reprojection | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_screen_color_old_reprojection.md) |
| `Screen Color Opacity` | Texture Buffer Screen Color Opacity | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_screen_color_opacity.md) |
| `Surface Custom Texture` | Surface Custom Texture | yes | fixed | - | ""(id 0):Texture2D | - | [The Surface Custom Texture node allows you to customize individual objects while maintaining shared material properties across multiple instances, for example: A...](../md_docs/content/materials/graph/node_library/textures/surface_custom_texture.md) |
| `TextureResolution` | Texture Resolution | yes | fixed | Texture:undefined, Mip:int | Width:int, Height:int, Depth/Layers:int | - | [This node takes an input Texture and outputs its Width and Height , is case a 3D Texure or a 2D Texture Array is connected to the input the node shall also output...](../md_docs/content/materials/graph/node_library/textures/texture_resolution.md) |
| `Transparent Blur` | Texture Buffer Transparent Blur | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_transparent_blur.md) |

## time parameters

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Frame` | Frame | yes | fixed | - | ""(id 0):int | - | [Outputs the number of the current game frame.](../md_docs/content/materials/graph/node_library/input/frame.md) |
| `Game Scale` | Game Scale | yes | fixed | - | ""(id 0):float | - | [Outputs the value that is used to scale frame duration. This value affects both the rendering rate (for example, particles spawn rate and material offsets) and...](../md_docs/content/materials/graph/node_library/input/game_scale.md) |
| `IFps` | IFps | yes | fixed | - | ""(id 0):float | - | [Outputs the scaled inverse FPS value (the time in seconds it took to complete the last frame). This value does not depend on the real FPS the hardware is capable of....](../md_docs/content/materials/graph/node_library/input/ifps.md) |
| `Time` | Time | yes | [6 configurations](#time) | - | ""(id 0):float | 0:Mode=Combobox · 1:Type=Combobox | [This node outputs a float value of time in seconds since the moment of the application startup. This node has parameters (see below) that define its behavior, to view...](../md_docs/content/materials/graph/node_library/misc/time.md) |

## tools

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Oblique Frustum Plane` | Oblique Frustum Plane | yes | fixed | - | ""(id 0):float4 | - | [Provides access to the Oblique frustum culling plane of the camera currently being used for rendering.](../md_docs/content/materials/graph/node_library/input/oblique_frustum_plane.md) |
| `_to_int` | To Int | yes | fixed | V:undefined | ""(id 1723312480):undefined | - | [Outputs the input value converted to the integer type.](../md_docs/content/materials/graph/node_library/misc/to_int.md) |
| `calcMipLevel` | Calc Mip Level | yes | fixed | Coord:float2 | ""(id 1723312480):float | - | [Outputs the mipmap level for the specified pixel position.](../md_docs/content/materials/graph/node_library/misc/calc_mip_level.md) |
| `calculateTBN` | Calculate TBN | yes | fixed | N:float3, Position:float3, UV:float2 | T:float3, B:float3, N:float3 | - | [Outputs the calculated Tangent, Binormal, and Normal vectors based on the Normal vector, Position vector, and UV.](../md_docs/content/materials/graph/node_library/misc/calculate_tbn.md) |
| `checkRange` | Check Range | yes | fixed | Value:undefined, Range Minimum:undefined, Range Maximum:undefined | ""(id 1723312480):bool | - | [This node checks if the input Value is inside the range defined by the input [Range Minimum, Range Maximum] . If the value is inside the range, it outputs True ,...](../md_docs/content/materials/graph/node_library/logical/check_range.md) |
| `degreesToRadians` | Degrees To Radians | yes | fixed | Degrees:undefined | ""(id 1723312480):undefined | - | [Outputs the input angle value (or individual components of the input vector) provided in degrees converted to radians. Radians on multi-component data types generates...](../md_docs/content/materials/graph/node_library/trigonometry/degrees_to_radians.md) |
| `fastPositionToScreenUV` | Fast Position To Screen UV | yes | fixed | Position View Space:undefined | ""(id 1723312480):float2 | - | [This node outputs a fast approximation of Screen UV based on the input coordinates of the position in the view space.](../md_docs/content/materials/graph/node_library/misc/fast_position_to_screen_uv.md) |
| `hclToRgb` | HCL To RGB | yes | fixed | HCL:float3 | ""(id 1723312480):float3 | - | [This node converts HCL (Hue, Chroma, Luminance) color values to RGB (Red, Green, Blue) color values.](../md_docs/content/materials/graph/node_library/misc/hcl_to_rgb.md) |
| `hcyToRgb` | HCY To RGB | yes | fixed | HCY:float3 | ""(id 1723312480):float3 | - | [This node converts HCY (Hue, Chroma, Luminance) color values to RGB (Red, Green, Blue) color values.](../md_docs/content/materials/graph/node_library/misc/hcy_to_rgb.md) |
| `hslToRgb` | HSL To RGB | yes | fixed | HSL:float3 | ""(id 1723312480):float3 | - | [This node converts HSL (Hue, Saturation, Lightness) color values to RGB (Red, Green, Blue) color values.](../md_docs/content/materials/graph/node_library/misc/hsl_to_rgb.md) |
| `hsvToRgb` | HSV To RGB | yes | fixed | HSV:float3 | ""(id 1723312480):float3 | - | [This node converts HSV (Hue, Saturation, Value) color values to RGB (Red, Green, Blue) color values.](../md_docs/content/materials/graph/node_library/misc/hsv_to_rgb.md) |
| `hueToRgb` | HUE To RGB | yes | fixed | HUE:float | ""(id 1723312480):float3 | - | [This node converts a HUE value in the [0; 1] range to an RGB color.](../md_docs/content/materials/graph/node_library/misc/hue_to_rgb.md) |
| `normalReconstructZ` | Normal Reconstruct Z | yes | fixed | Normal:undefined | ""(id 1723312480):float | - | [This node outputs a reconstructed vector Z-coordinate using the input X and Y coordinates, which are within the [-1, 1] range, i.e., the resulting vector has a unit...](../md_docs/content/materials/graph/node_library/misc/normal_reconstruct_z.md) |
| `normalToTBN` | Normal To TBN | yes | fixed | N:float3 | ""(id 1723312480):float3x3 | - | [Calculates TBN matrix containing Tangent, Binormal and Normal vectors out of a Normal vector.](../md_docs/content/materials/graph/node_library/misc/normal_to_tbn.md) |
| `normalizationTBN` | Normalization TBN | yes | fixed | T:float3, B:float3, N:float3, Sign Binormal:float | T:float3, B:float3, N:float3 | - | [Calculates normalized Tangent, Binormal, and Normal vectors.](../md_docs/content/materials/graph/node_library/misc/normalization_tbn.md) |
| `positionToNormal` | Position To Normal | yes | fixed | Position:undefined | ""(id 1723312480):float3 | - |  |
| `positionToScreenUV` | Position To Screen UV | yes | fixed | Position View Space:undefined | ""(id 1723312480):float2 | - |  |
| `radiansToDegrees` | Radians To Degrees | yes | fixed | Radians:undefined | ""(id 1723312480):undefined | - | [Outputs the input angle value (or individual components of the input vector) provided in radians converted to degree angle units. Degrees on multi-component data...](../md_docs/content/materials/graph/node_library/trigonometry/radians_to_degrees.md) |
| `reorientNormalBlend` | Reorient Normal Blend | yes | fixed | Base Normal:float3, Detail Normal:float3 | ""(id 1723312480):float3 | - | [This node is used for blending normals while preserving their correct orientation. It ensures that two normals are properly combined and remain correctly applied to a...](../md_docs/content/materials/graph/node_library/misc/reorient_normal_blend.md) |
| `reorientVectorBlend` | Reorient Vector Blend | yes | fixed | Main Vector:float3, Vector:float3, Rotation Vector:float3 | ""(id 1723312480):float3 | - | [Performs blending of vectors and outputs the reoriented vector.](../md_docs/content/materials/graph/node_library/misc/reorient_vector_blend.md) |
| `rerange` | Rerange | yes | fixed | In:undefined, In Range Minimum:float, In Range Maximum:float, Out Range Minimum:float, Out Range Maximum:float | ""(id 1723312480):undefined | - | [Outputs an input value In set within a source range [ In Range Min , In Range Max ] converted to a new one within a target range [ Out Range Min , Out Range Max ]....](../md_docs/content/materials/graph/node_library/math/rerange.md) |
| `rgbToHcl` | RGB To HCL | yes | fixed | RGB:float3 | ""(id 1723312480):float3 | - | [This node converts RGB (Red, Green, Blue) color values to HCL (Hue, Chroma, Luminance) color values.](../md_docs/content/materials/graph/node_library/misc/rgb_to_hcl.md) |
| `rgbToHcv` | RGB To HCV | yes | fixed | RGB:float3 | ""(id 1723312480):float3 | - | [This node converts RGB (Red, Green, Blue) color values to HCV (Hue, Chroma, Value) color values.](../md_docs/content/materials/graph/node_library/misc/rgb_to_hcv.md) |
| `rgbToHcy` | RGB To HCY | yes | fixed | RGB:float3 | ""(id 1723312480):float3 | - | [This node converts RGB (Red, Green, Blue) color values to HCY (Hue, Chroma, Luminance) color values.](../md_docs/content/materials/graph/node_library/misc/rgb_to_hcy.md) |
| `rgbToHsl` | RGB To HSL | yes | fixed | RGB:float3 | ""(id 1723312480):float3 | - | [This node converts RGB (Red, Green, Blue) color values to HSL (Hue, Saturation, Lightness) color values.](../md_docs/content/materials/graph/node_library/misc/rgb_to_hsl.md) |
| `rgbToHsv` | RGB To HSV | yes | fixed | RGB:float3 | ""(id 1723312480):float3 | - | [This node converts RGB (Red, Green, Blue) color values to HSV (Hue, Saturation, Value) color values.](../md_docs/content/materials/graph/node_library/misc/rgb_to_hsv.md) |
| `rgbToLuma` | RGB To Luma | yes | fixed | Color:undefined | ""(id 1723312480):float | - | [This node outputs the perceived brightness of the input Color .](../md_docs/content/materials/graph/node_library/misc/rgb_to_luma.md) |
| `rgbToYcbcr` | RGB To YCbCr | yes | fixed | RGB:float3 | ""(id 1723312480):float3 | - | [This node converts RGB (Red, Green, Blue) color values to Y&#8242;CbCr (Gamma-corrected Luminance, blue and red-difference chrominance) color values.](../md_docs/content/materials/graph/node_library/misc/rgb_to_ycbcr.md) |
| `rgbToYcgco` | RGB To YCgCo | yes | fixed | RGB:float3 | ""(id 1723312480):float3 | - | [This node converts RGB (Red, Green, Blue) color values to YCgCo (Luminance, Chrominance green, Chrominance orange) color values.](../md_docs/content/materials/graph/node_library/misc/rgb_to_ycgco.md) |
| `rgbToYuv` | RGB To YUV | yes | fixed | RGB:float3 | ""(id 1723312480):float3 | - | [This node converts RGB (Red, Green, Blue) color values to YUV (Luminance-Chrominance) color values.](../md_docs/content/materials/graph/node_library/misc/rgb_to_yuv.md) |
| `rotateAxis` | Rotate Axis | yes | fixed | Axis:float3, Radians:float | ""(id 1723312480):float3x3 | - | [Outputs the rotation matrix for the input angle, in radians, around the input axis.](../md_docs/content/materials/graph/node_library/matrix/rotate_axis.md) |
| `rotateEuler` | Rotate Euler | yes | fixed | Euler:float3 | ""(id 1723312480):float3x3 | - | [Outputs the rotation matrix from the input vector of Euler angles (pitch, roll, yaw). The Euler angles are specified in the axis rotation sequence - XYZ. It is an...](../md_docs/content/materials/graph/node_library/matrix/rotate_euler.md) |
| `rotateUV` | Rotate UV | yes | fixed | UV:float2, Angle:float | ""(id 1723312480):float2 | - | [This node is used to rotate the input UV coordinates to a specified Angle , in degrees, and outputs the resulting UV coordinates.](../md_docs/content/materials/graph/node_library/misc/rotate_uv.md) |
| `screenUVToViewDirection` | Screen UV To View Direction | yes | fixed | Screen UV:undefined | ""(id 1723312480):float3 | - | [This node outputs the View Direction vector in the view space based on the input Screen UV .](../md_docs/content/materials/graph/node_library/misc/screen_uv_to_view_direction.md) |
| `specularToMetalness` | Specular To Metalness | yes | fixed | Diffuse Color:float3, Specular Color:float3, Gloss:float | Albedo:float3, Metalness:float, Roughness:float, Specular:float | - | [Performs conversion of material features from the legacy specular workflow to PBR.](../md_docs/content/materials/graph/node_library/misc/specular_to_metalness.md) |
| `ycbcrToRgb` | YCbCr To RGB | yes | fixed | YCC:float3 | ""(id 1723312480):float3 | - | [This node converts Y&#8242;CbCr (Gamma-corrected Luminance, blue and red-difference chrominance) color values to RGB (Red, Green, Blue) color values.](../md_docs/content/materials/graph/node_library/misc/ycbcr_to_rgb.md) |
| `ycgcoToRgb` | YCgCo To RGB | yes | fixed | YCC:float3 | ""(id 1723312480):float3 | - | [This node converts YCgCo (Luminance, Chrominance green, Chrominance orange) color values to RGB (Red, Green, Blue) color values.](../md_docs/content/materials/graph/node_library/misc/ycgco_to_rgb.md) |
| `yuvToRgb` | YUV To RGB | yes | fixed | YUV:float3 | ""(id 1723312480):float3 | - | [This node converts YUV (Luminance-Chrominance) color values to RGB (Red, Green, Blue) color values.](../md_docs/content/materials/graph/node_library/misc/yuv_to_rgb.md) |

## vertex_attributes

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Instance ID` | Instance ID | yes | fixed | - | ""(id 0):uint | - | [Provides access to the per-instance identifier of initial geometry automatically generated by the runtime.](../md_docs/content/materials/graph/node_library/input/instance_id.md) |
| `Object Position` | Object Position | yes | [4 configurations](#object-position) | - | Camera World:float3 | 0:Space=Combobox | [Provides access to the Position of the Object. The coordinate space of the output value ( Camera World, Object, View, Absolute World ) can be selected with the Space...](../md_docs/content/materials/graph/node_library/input/object_position.md) |
| `Vertex Binormal` | Vertex Binormal | yes | [4 configurations](#vertex-binormal) | - | World:float3 | 0:Space=Combobox | [Provides access to the Binormal Vector of initial geometry. This vector is calculated based on UV 0. The coordinate space of the output value ( World, Object,...](../md_docs/content/materials/graph/node_library/input/vertex_binormal.md) |
| `Vertex Color` | Vertex Color | yes | fixed | - | ""(id 0):float4 | - | [Provides access to Vertex Color values of initial geometry. This vector is calculated based on UV 0.](../md_docs/content/materials/graph/node_library/input/vertex_color.md) |
| `Vertex Front face` | Vertex Front Face | yes | fixed | - | ""(id 0):bool | - | [Provides access to Vertex Front Face values of initial geometry.](../md_docs/content/materials/graph/node_library/input/vertex_front_face.md) |
| `Vertex ID` | Vertex ID | yes | fixed | - | ""(id 0):uint | - | [Provides access to the per-vertex identifier of initial geometry automatically generated by the runtime.](../md_docs/content/materials/graph/node_library/input/vertex_id.md) |
| `Vertex Normal` | Vertex Normal | yes | [4 configurations](#vertex-normal) | - | World:float3 | 0:Space=Combobox | [Provides access to the Normal Vector of initial geometry. This vector is calculated based on UV 0. The coordinate space of the output value ( World, Object, Tangent,...](../md_docs/content/materials/graph/node_library/input/vertex_normal.md) |
| `Vertex Position` | Vertex Position | yes | [4 configurations](#vertex-position) | - | Camera World:float3 | 0:Space=Combobox | [Provides access to Vertex Positions of initial geometry before applying any vertex transformations implemented in shaders. The coordinate space of the output value (...](../md_docs/content/materials/graph/node_library/input/vertex_position.md) |
| `Vertex Tangent` | Vertex Tangent | yes | [4 configurations](#vertex-tangent) | - | World:float3 | 0:Space=Combobox | [Provides access to the Tangent Vector of initial geometry. This vector is calculated based on UV 0. The coordinate space of the output value ( World, Object, Tangent,...](../md_docs/content/materials/graph/node_library/input/vertex_tangent.md) |
| `Vertex UV 0` | Vertex UV 0 | yes | fixed | - | ""(id 0):float2 | - | [This node retrieves the first set of UV coordinates from the mesh's vertex data, defining how textures are wrapped around a 3D model and positioned on the mesh. The...](../md_docs/content/materials/graph/node_library/input/vertex_uv_0.md) |
| `Vertex UV 1` | Vertex UV 1 | yes | fixed | - | ""(id 0):float2 | - | [This node retrieves the second set of UV coordinates from a mesh's vertex data, defining how textures are wrapped around a 3D model and positioned on the mesh. The...](../md_docs/content/materials/graph/node_library/input/vertex_uv_1.md) |
| `VertexInterpolation` | Vertex Interpolation | yes | fixed | ""(id 0):undefined | ""(id 1):undefined | - | [This node processes all logic passed to it in the vertex shader. This can highly improve the performance, if the visual result calculated per-vertex and linearly...](../md_docs/content/materials/graph/node_library/misc/vertex_interpolation.md) |

## uncategorised

| key | name | in palette | settings | inputs | outputs | props | what it does |
|---|---|---|---|---|---|---|---|
| `Animation Old Time` | Animation Old Time | yes | fixed | - | ""(id 0):float | - | [Outputs the previous render animation time for vegetation, in milliseconds.](../md_docs/content/materials/graph/node_library/misc/animation_old_time.md) |
| `Animation Time` | Animation Time | yes | fixed | - | ""(id 0):float | - | [Outputs the render animation time for vegetation, in milliseconds.](../md_docs/content/materials/graph/node_library/misc/animation_time.md) |
| `Camera Fov` | Camera Fov | yes | fixed | - | ""(id 0):float | - |  |
| `Color (Float3)` | Color (Float3) | yes | fixed | - | 1.0 1.0 1.0:float3 | 0:(no label)=Float3 | [Outputs an RGB color which is represented by a vector of three float values. To set the required output values, double-click on the output values (1.0 1.0 1.0), edit...](../md_docs/content/materials/graph/node_library/input/color_float3.md) |
| `Color (Float4)` | Color (Float4) | yes | fixed | - | 1.0 1.0 1.0 1.0:float4 | 0:(no label)=Float4 | [Outputs an RGBA color which is represented by a vector of four float values. To set the required output values, double-click on the output values (1.0 1.0 1.0 1.0),...](../md_docs/content/materials/graph/node_library/input/color_float4.md) |
| `ComboboxSwitch` | Combobox Switch | yes | fixed | Combobox:int | ""(id 0):undefined | - | [This node is an analog of the Branch , but with multiple options instead of only two. Connect a Combobox parameter node to the input. As a result only the branch that...](../md_docs/content/materials/graph/node_library/logical/combobox_switch.md) |
| `CurrentSurfaceParameters` | Current Surface Parameters | yes | fixed | - | Node ID:int, Surface:int, Instance:int, Material ID:uint, Light Map:uint | - | [Reads the custom parameters of the surface being shaded. Unlike Surface Parameters, this node samples no screen buffer: it takes the ID the renderer passes to the...](../md_docs/content/materials/graph/node_library/input/current_surface_parameters.md) |
| `Depth Old` | Texture Buffer Depth Old | yes | fixed | - | ""(id 0):Texture2D | - |  |
| `Direct Lights` | Texture Buffer Direct Lights | yes | fixed | - | ""(id 0):Texture2DArray | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_direct_lights.md) |
| `Expression` | Expression | yes | fixed | ""(id 0):undefined | ""(id 0):undefined | 0:(no label)=Code | Its output is unnamed until the graph has finished loading, so a link out of it must carry `output_id`. See *The Expression node* below. [This node is used to write simple arithmetic operations as well as to change the number of data components, or as a swizzle. The contents to be put to each channel...](../md_docs/content/materials/graph/node_library/misc/expression.md) |
| `Final` | Final |  | [per graph](material_node_pins.md) | Material | - | - | [The main output node that compiles a Material node to a base material.](../md_docs/content/materials/graph/node_library/misc/final.md) |
| `Indirect Diffuse Final` | Texture Buffer Indirect Diffuse Final | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_indirect_diffuse_final.md) |
| `Indirect Lights` | Texture Buffer Indirect Lights | yes | fixed | - | ""(id 0):Texture2DArray | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_indirect_lights.md) |
| `Indirect Specular Final` | Texture Buffer Indirect Specular Final | yes | fixed | - | ""(id 0):Texture2D | - | [Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the SampleTexture node and...](../md_docs/content/materials/graph/node_library/textures/texture_buffer_indirect_specular_final.md) |
| `Inputs` | Inputs |  | fixed | - | - | - |  |
| `LoopBegin` | Loop Begin | yes | fixed | - | Loop:Loop, Index:int, Maximum Iterations:int | 0:Maximum Iterations=Int | [Loops make it possible to repeat an arbitrary set of operations multiple times. The Loop Begin node enables you to create variables to which you can write data via...](../md_docs/content/materials/graph/node_library/misc/loop_begin.md) |
| `LoopEnd` | Loop End | yes | fixed | Loop:Loop, Break:bool | - | - | [Loops make it possible to repeat an arbitrary set of operations multiple times. The Loop Begin node enables you to create variables to which you can write data via...](../md_docs/content/materials/graph/node_library/misc/loop_end.md) |
| `Material` | Material | yes | [per graph](material_node_pins.md) | Albedo:float3, Metalness:float, Roughness:float, Specular:float, Microfiber:float, Normal Tangent Space:float3, Translucent:float, Ambient Occlusion:float, Emission:float3, Velocity:float2, Reactivity:float, Auxiliary:float4, Depth Offset:float, Vertex Offset Tangent Space:float3 | Material | - | [Generates a material. The set of input ports and supported features, as well as the type of the generated material, depends on the current Common Settings. A material...](../md_docs/content/materials/graph/node_library/misc/material.md) |
| `Material ID` | Material ID | yes | fixed | - | ""(id 0):uint | - |  |
| `MaterialParameters` | Material Parameters | yes | [5 configurations](#materialparameters) | Screen Position:int2 | Material ID:uint, Material Mask:uint, Screen-Space Shadows:uint, Shoreline Wetness:uint, Motion Blur:uint, SSAO:uint, SSR:uint, SSS:uint, DOF:uint | 0:Type=Combobox | [Reads the custom parameters of the material assigned to the surface drawn at a pixel. The node samples a Surface ID buffer, takes the Material ID stored in the...](../md_docs/content/materials/graph/node_library/input/material_parameters.md) |
| `MaterialParametersByID` | Material Parameters by ID | yes | fixed | Material ID:uint | Material Mask:uint, Screen-Space Shadows:uint, Shoreline Wetness:uint, Motion Blur:uint, SSAO:uint, SSR:uint, SSS:uint, DOF:uint | - | [Reads the custom parameters of the material with a given Material ID. It is the same node as Material Parameters, except that the ID comes from an input port instead...](../md_docs/content/materials/graph/node_library/input/material_parameters_by_id.md) |
| `MaterialQualitySwitch` | Material Quality Switch | yes | fixed | Low:undefined, Medium:undefined, High:undefined | ""(id 0):undefined | - | [Receives different implementations of the same material for different quality levels ( Low , Medium , High ) and outputs the corresponding implementation depending on...](../md_docs/content/materials/graph/node_library/misc/material_quality_switch.md) |
| `Outputs` | Outputs |  | fixed | - | - | - |  |
| `Parameter` | Parameter |  | fixed | - | ""(id 0):undefined | 0:(no label)=Float |  |
| `RotateSpace` | Rotate Space | yes | [16 configurations](#rotatespace) | World:undefined | World:undefined | 0:From=Combobox · 1:To=Combobox | [This node is used to transform a DIRECTION vector from one space ( World, Object, Tangent, View ) to another space. Suppose you have a vector in Object space and you...](../md_docs/content/materials/graph/node_library/misc/rotate_space.md) |
| `SampleTexture` | Sample Texture | yes | [1170 configurations](#sampletexture) | Texture:Texture2D, UV:float2 | Color:float4 | 0:Type=Combobox | [Takes an input texture (2D, 3D, 2D array, 2D int, or cubemap) and returns a value from this texture depending on the current parameter values selected for this node,...](../md_docs/content/materials/graph/node_library/textures/sample_texture.md) |
| `Screen Coord Before Upscale` | Screen Coord Before Upscale | yes | fixed | - | ""(id 0):uint2 | - | [Provides access to the position in the Screen Space Coordinates before the buffer is upscaled.](../md_docs/content/materials/graph/node_library/input/screen_coord_before_upscale.md) |
| `Settings Haze Physical Screen Space Global Illumination` | Settings Haze Physical Screen Space Global Illumination | yes | fixed | - | ""(id 0):float | - | [Outputs 1 if the Screen-Space Haze Global Illumination (SSHGI) effect is enabled, otherwise &#8212; 0 . SSHGI is a screen-space effect ensuring consistency of haze...](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Haze Physical Visibility Threshold` | Settings Haze Physical Visibility Threshold | yes | fixed | - | ""(id 0):float | - |  |
| `Settings Haze Scattering Mie Front Side Intensity` | Settings Haze Scattering Mie Front Side Intensity | yes | fixed | - | ""(id 0):float | - | [Outputs the Falloff of the Fresnel effect for Mie intensity.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `Settings Sun Color` | Settings Sun Color | yes | fixed | - | ""(id 0):float3 | - | [Outputs the Color multiplier for the Sun texture.](../md_docs/content/materials/graph/node_library/input/settings.md) |
| `ShadingQualitySwitch` | Shading Quality Switch | yes | fixed | Low:undefined, Medium:undefined, High:undefined | ""(id 0):undefined | - | [Receives different sets of shading features for different quality levels ( Low , Medium , High ) and outputs the corresponding implementation depending on the quality...](../md_docs/content/materials/graph/node_library/misc/shading_quality_switch.md) |
| `SubGraph` | Sub Graph | yes | fixed | - | - | 0:(no label)=SubGraph | [This is a custom node implementing certain functionality, constructed using other graph nodes, and saved to an .msubgraph asset on disk. To specify such an asset to...](../md_docs/content/materials/graph/node_library/misc/sub_graph.md) |
| `SurfaceIDRenderingMode` | Surface ID Rendering Mode | yes | fixed | - | Transparent Buffer Available:bool, Decal Buffer Available:bool, Water Buffer Available:bool, Scene Buffer Available:bool | - | [Reports which Surface ID buffers the current configuration provides, so that a graph can adapt to it instead of assuming. Only two of the four outputs actually vary:...](../md_docs/content/materials/graph/node_library/input/surface_id_rendering_mode.md) |
| `SurfaceParameters` | Surface Parameters | yes | [5 configurations](#surfaceparameters) | Screen Position:int2 | Node ID:int, Surface:int, Instance:int, Material ID:uint, Light Map:uint | 0:Type=Combobox | [Reads the custom parameters of the surface drawn at a pixel. The node samples a Surface ID buffer, finds the block that ID belongs to, and gives every value in it an...](../md_docs/content/materials/graph/node_library/input/surface_parameters.md) |
| `Texture2D` | Texture 2D | yes | [27 configurations](#texture2d) | - | checker_d.texture:Texture2D | 0:Path=Texture2D · 1:Wrap X=Combobox · 2:Wrap Y=Combobox · 3:Wrap Z=Combobox · 4:Anisotropy=Bool · 5:Force Streaming=Bool · 6:Manual Filtering=Bool | [This node represents the most widely used texture type. To sample data from such a texture connect it to the SampleTexture node and specify UV coordinates for reading...](../md_docs/content/materials/graph/node_library/textures/texture_2d.md) |
| `Texture2DArray` | Texture 2D Array | yes | [27 configurations](#texture2darray) | - | noise.texture:Texture2DArray | 0:Path=Texture2DArray · 1:Wrap X=Combobox · 2:Wrap Y=Combobox · 3:Wrap Z=Combobox · 4:Anisotropy=Bool · 5:Force Streaming=Bool · 6:Manual Filtering=Bool |  |
| `Texture2DInt` | Texture 2D Int | yes | [27 configurations](#texture2dint) | - | checker_d.texture:Texture2DInt | 0:Path=Texture2DInt · 1:Wrap X=Combobox · 2:Wrap Y=Combobox · 3:Wrap Z=Combobox · 4:Anisotropy=Bool · 5:Force Streaming=Bool · 6:Manual Filtering=Bool |  |
| `Texture3D` | Texture 3D | yes | [27 configurations](#texture3d) | - | curl_noise_3d.texture:Texture3D | 0:Path=Texture3D · 1:Wrap X=Combobox · 2:Wrap Y=Combobox · 3:Wrap Z=Combobox · 4:Anisotropy=Bool · 5:Force Streaming=Bool · 6:Manual Filtering=Bool | [This node represents the texture type that is used to store some spatial information (like clouds or fog density, or voxel lighting data), it is also called a Volume...](../md_docs/content/materials/graph/node_library/textures/texture_3d.md) |
| `TextureCube` | Texture Cube | yes | [27 configurations](#texturecube) | - | environment_default.texture:TextureCube | 0:Path=TextureCube · 1:Wrap X=Combobox · 2:Wrap Y=Combobox · 3:Wrap Z=Combobox · 4:Anisotropy=Bool · 5:Force Streaming=Bool · 6:Manual Filtering=Bool | [This node represents a texture, that combines six images mapped onto a cube, and is mainly used to create a 360&#176; panorama. To sample data from such a texture...](../md_docs/content/materials/graph/node_library/textures/texture_cube.md) |
| `TextureRamp (R)` | Texture Ramp (R) | yes | fixed | - | Texture:TextureRamp | 0:Ramp=TextureRamp R · 1:Anisotropy=Bool |  |
| `TextureRamp (RG)` | Texture Ramp (RG) | yes | fixed | - | Texture:TextureRamp | 0:Ramp=TextureRamp RG · 1:Anisotropy=Bool |  |
| `TextureRamp (RGB)` | Texture Ramp (RGB) | yes | fixed | - | Texture:TextureRamp | 0:Ramp=TextureRamp RGB · 1:Anisotropy=Bool |  |
| `TextureRamp (RGBA)` | Texture Ramp (RGBA) | yes | fixed | - | Texture:TextureRamp | 0:Ramp=TextureRamp RGBA · 1:Anisotropy=Bool |  |
| `TransformSpace` | Transform Space | yes | [16 configurations](#transformspace) | Camera World:undefined | Camera World:undefined | 0:From=Combobox · 1:To=Combobox | [This node is used to transform a POSITION vector from one space ( Camera World, Object, View, Absolute World ) to another space. Suppose you have a position...](../md_docs/content/materials/graph/node_library/misc/transform_space.md) |
| `Upscale Factor` | Upscale Factor | yes | fixed | - | ""(id 0):float2 | - | [Provides the buffer to viewport aspect ratio value (width / upscaled width).](../md_docs/content/materials/graph/node_library/input/upscale_factor.md) |
| `distance` | Distance | yes | fixed | Position 0:undefined, Position 1:undefined | ""(id 1723312480):float | - | [Outputs the distance scalar between the two input positions.](../md_docs/content/materials/graph/node_library/math/distance.md) |
| `getDecalSurfaceID` | Get Decal Surface ID | yes | fixed | Coord:int2 | Surface ID:uint | - |  |
| `getOpaqueSurfaceID` | Get Opaque Surface ID | yes | fixed | Coord:int2 | Surface ID:uint | - |  |
| `getOpaqueSurfaceIDUV` | Get Opaque Surface ID UV | yes | fixed | UV:float2 | Surface ID:uint | - |  |
| `getSceneSurfaceID` | Get Scene Surface ID | yes | fixed | Coord:int2 | Surface ID:uint | - |  |
| `getSceneSurfaceIDUV` | Get Scene Surface ID UV | yes | fixed | UV:float2 | Surface ID:uint | - |  |
| `getTransparentSurfaceID` | Get Transparent Surface ID | yes | fixed | Coord:int2 | Surface ID:uint | - |  |
| `getWaterSurfaceID` | Get Water Surface ID | yes | fixed | Coord:int2 | Surface ID:uint | - |  |
| `get_resource_sampler_id` | Get Resource Sampler Id | yes | fixed | Slot:uint | ""(id 1723312480):uint | - |  |
| `get_resource_structured_buffer_id` | Get Resource Structured Buffer Id | yes | fixed | Slot:uint | ""(id 1723312480):uint | - |  |
| `get_resource_texture_id` | Get Resource Texture Id | yes | fixed | Slot:uint | ""(id 1723312480):uint | - |  |
| `invLerp` | Inverse Lerp | yes | fixed | A:undefined, B:undefined, Value:undefined | ""(id 1723312480):undefined | - | [This node outputs the coefficient of the value within a specified interval calculated according to the following formula: (Value - A) / (B - A) clamped within 0.0f...](../md_docs/content/materials/graph/node_library/math/inverse_lerp.md) |
| `isEmptyMaterialID` | Is Empty Material ID | yes | fixed | Material Id:uint | ""(id 1723312480):bool | - |  |
| `isEmptySurfaceID` | Is Empty Surface ID | yes | fixed | Surface Id:uint | ""(id 1723312480):bool | - |  |
| `isSkyMaterialID` | Is Sky Material ID | yes | fixed | Material Id:uint | ""(id 1723312480):bool | - |  |
| `isSkySurfaceID` | Is Sky Surface ID | yes | fixed | Surface Id:uint | ""(id 1723312480):bool | - |  |
| `isValidMaterialID` | Is Valid Material ID | yes | fixed | Material Id:uint | ""(id 1723312480):bool | - |  |
| `isValidSurfaceID` | Is Valid Surface ID | yes | fixed | Surface Id:uint | ""(id 1723312480):bool | - |  |
| `kronecker` | Kronecker | yes | fixed | Dimension:uint, Frame:uint, Offset:float2 | ""(id 1723312480):float2 | - |  |
| `length2` | Length Squared | yes | fixed | Vector:undefined | ""(id 1723312480):float | - | [Outputs the squared length of the input vector. This method is much faster than Length &#8212; the calculation is basically the same only without the slow Sqrt call....](../md_docs/content/materials/graph/node_library/math/length_squared.md) |
| `lerp` | Lerp | yes | fixed | A:undefined, B:undefined, Coefficient:undefined | ""(id 1723312480):undefined | - | [This node is used to blend (linear interpolation) between two input values or colors A and B depending on the Coefficient . if Coefficient = 0 the node outputs A...](../md_docs/content/materials/graph/node_library/math/lerp.md) |
| `lerp3` | Lerp3 | yes | fixed | A:undefined, B:undefined, C:undefined, Coefficient:float | ""(id 1723312480):undefined | - | [This node is used to blend (linear interpolation) between three input values A , B , and C depending on the Coefficient . if Coefficient = 0 the node outputs A value...](../md_docs/content/materials/graph/node_library/math/lerp3.md) |
| `mirrorUV` | Mirror UV | yes | fixed | UV:float2 | ""(id 1723312480):float2 | - | [This node is used to mirror the input UV coordinates, and outputs the resulting UV coordinates. Mirrored UV Tiling](../md_docs/content/materials/graph/node_library/misc/mirror_uv.md) |
| `tanh` | Hyperbolic Tangent | yes | fixed | Radians:undefined | ""(id 1723312480):undefined | - | [Outputs the hyperbolic tangent of the input value (or individual components of the input vector). The input must be in radians.](../md_docs/content/materials/graph/node_library/trigonometry/hyperbolic_tangent.md) |
| `uniformDisk` | Uniform Disk | yes | fixed | Xi:float2 | ""(id 1723312480):float2 | - |  |

## Nodes whose pins depend on their settings

41 node types rebuild their pins when their own settings change, so the row in the table above is only their default. Each one is below, with the setting values that produce each set of pins.

**A value shown as `1 `Object`` is written to the file as the number.** A combobox prop is stored by position, so `props` carries `"x": 1` and never the word. Settings without a number - `texture_type`, `texture_data` - are node-level fields and are written as the string itself.

A cell listing several values means those values all give the same pins. An empty setting cell means that setting does not exist in that configuration - `SampleTexture` only offers `Normal Space` when `texture_data` is `Asset`.

Each table was checked against the dump: every configuration the Editor produced is matched by exactly one row here, with the same pins.

### Back

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Branch

3 configurations.

**inputs**

| inputs |
|---|
| Condition:bool, True:undefined, False:undefined |

**outputs**

| outputs |
|---|
| (unnamed):undefined |

### Camera Direction

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Camera Position

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `Camera World` | Camera World:float3 |
| 1 `Object` | Object:float3 |
| 2 `View` | View:float3 |
| 3 `Absolute World` | Absolute World:float3 |

### Decal Projected Normal

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Decal Projected Position

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `Camera World` | Camera World:float3 |
| 1 `Object` | Object:float3 |
| 2 `View` | View:float3 |
| 3 `Absolute World` | Absolute World:float3 |

### Decal Scene Normal

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Decal Scene Position

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `Camera World` | Camera World:float3 |
| 1 `Object` | Object:float3 |
| 2 `View` | View:float3 |
| 3 `Absolute World` | Absolute World:float3 |

### Down

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Forward

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Left

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### MaterialParameters

5 configurations.

**inputs**

| inputs |
|---|
| Screen Position:int2 |

**outputs**

| outputs |
|---|
| Material ID:uint, Material Mask:uint, Screen-Space Shadows:uint, Shoreline Wetness:uint, Motion Blur:uint, SSAO:uint, SSR:uint, SSS:uint, DOF:uint |

### Moon Direction

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Object Position

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `Camera World` | Camera World:float3 |
| 1 `Object` | Object:float3 |
| 2 `View` | View:float3 |
| 3 `Absolute World` | Absolute World:float3 |

### Right

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### RotateSpace

16 configurations.

**inputs**

| From | inputs |
|---|---|
| 0 `World` | World:undefined |
| 1 `Object` | Object:undefined |
| 2 `Tangent` | Tangent:undefined |
| 3 `View` | View:undefined |

**outputs**

| To | outputs |
|---|---|
| 0 `World` | World:undefined |
| 1 `Object` | Object:undefined |
| 2 `Tangent` | Tangent:undefined |
| 3 `View` | View:undefined |

### SampleTexture

1170 configurations.

**inputs**

| Type | texture_data | texture_type | inputs |
|---|---|---|---|
| 0 `Default`, 3 `Grad`, 7 `Cubic`, 9 `Manual linear` | any | Texture2DInt | Texture:Texture2DInt, UV:float2 |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | Asset | Texture2D | Texture:Texture2D, UV:float2, Normal Intensity:float |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Normal Intensity:float |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | Asset | Texture3D | Texture:Texture3D, UVW:float3, Normal Intensity:float |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | Asset | TextureCube | Texture:TextureCube, Direction:float3, Normal Intensity:float |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | Asset | TextureRamp | Texture:TextureRamp, U:float, Normal Intensity:float |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | any but Asset | Texture2D | Texture:Texture2D, UV:float2 |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | any but Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | any but Asset | Texture3D | Texture:Texture3D, UVW:float3 |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | any but Asset | TextureCube | Texture:TextureCube, Direction:float3 |
| 0 `Default`, 7 `Cubic`, 9 `Manual linear` | any but Asset | TextureRamp | Texture:TextureRamp, U:float |
| 1 `Mip`, 8 `Cubic Mip` | Asset | Texture2D | Texture:Texture2D, UV:float2, Mip:float, Normal Intensity:float |
| 1 `Mip`, 8 `Cubic Mip` | Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Mip:float, Normal Intensity:float |
| 1 `Mip`, 8 `Cubic Mip` | Asset | Texture3D | Texture:Texture3D, UVW:float3, Mip:float, Normal Intensity:float |
| 1 `Mip`, 8 `Cubic Mip` | Asset | TextureCube | Texture:TextureCube, Direction:float3, Mip:float, Normal Intensity:float |
| 1 `Mip`, 8 `Cubic Mip` | Asset | TextureRamp | Texture:TextureRamp, U:float, Mip:float, Normal Intensity:float |
| 1 `Mip`, 8 `Cubic Mip` | any | Texture2DInt | Texture:Texture2DInt, UV:float2, Mip:float |
| 1 `Mip`, 8 `Cubic Mip` | any but Asset | Texture2D | Texture:Texture2D, UV:float2, Mip:float |
| 1 `Mip`, 8 `Cubic Mip` | any but Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Mip:float |
| 1 `Mip`, 8 `Cubic Mip` | any but Asset | Texture3D | Texture:Texture3D, UVW:float3, Mip:float |
| 1 `Mip`, 8 `Cubic Mip` | any but Asset | TextureCube | Texture:TextureCube, Direction:float3, Mip:float |
| 1 `Mip`, 8 `Cubic Mip` | any but Asset | TextureRamp | Texture:TextureRamp, U:float, Mip:float |
| 2 `Mip offset` | Asset | Texture2D | Texture:Texture2D, UV:float2, Mip Offset:float, Normal Intensity:float |
| 2 `Mip offset` | Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Mip Offset:float, Normal Intensity:float |
| 2 `Mip offset` | Asset | Texture3D | Texture:Texture3D, UVW:float3, Mip Offset:float, Normal Intensity:float |
| 2 `Mip offset` | Asset | TextureCube | Texture:TextureCube, Direction:float3, Mip Offset:float, Normal Intensity:float |
| 2 `Mip offset` | Asset | TextureRamp | Texture:TextureRamp, U:float, Mip Offset:float, Normal Intensity:float |
| 2 `Mip offset` | any | Texture2DInt | Texture:Texture2DInt, UV:float2, Mip Offset:float |
| 2 `Mip offset` | any but Asset | Texture2D | Texture:Texture2D, UV:float2, Mip Offset:float |
| 2 `Mip offset` | any but Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Mip Offset:float |
| 2 `Mip offset` | any but Asset | Texture3D | Texture:Texture3D, UVW:float3, Mip Offset:float |
| 2 `Mip offset` | any but Asset | TextureCube | Texture:TextureCube, Direction:float3, Mip Offset:float |
| 2 `Mip offset` | any but Asset | TextureRamp | Texture:TextureRamp, U:float, Mip Offset:float |
| 3 `Grad` | Asset | Texture2D | Texture:Texture2D, UV:float2, DDX:float2, DDY:float2, Normal Intensity:float |
| 3 `Grad` | Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, DDX:float2, DDY:float2, Normal Intensity:float |
| 3 `Grad` | Asset | Texture3D | Texture:Texture3D, UVW:float3, DDX:float3, DDY:float3, Normal Intensity:float |
| 3 `Grad` | Asset | TextureCube | Texture:TextureCube, Direction:float3, DDX:float3, DDY:float3, Normal Intensity:float |
| 3 `Grad` | Asset | TextureRamp | Texture:TextureRamp, U:float, DDX:float2, Normal Intensity:float |
| 3 `Grad` | any but Asset | Texture2D | Texture:Texture2D, UV:float2, DDX:float2, DDY:float2 |
| 3 `Grad` | any but Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, DDX:float2, DDY:float2 |
| 3 `Grad` | any but Asset | Texture3D | Texture:Texture3D, UVW:float3, DDX:float3, DDY:float3 |
| 3 `Grad` | any but Asset | TextureCube | Texture:TextureCube, Direction:float3, DDX:float3, DDY:float3 |
| 3 `Grad` | any but Asset | TextureRamp | Texture:TextureRamp, U:float, DDX:float2 |
| 4 `Fetch` | Asset | Texture2D | Texture:Texture2D, Coord:int2, Mip:int, Normal Intensity:float |
| 4 `Fetch` | Asset | Texture2DArray | Texture:Texture2DArray, Coord:int2, Index:int, Mip:int, Normal Intensity:float |
| 4 `Fetch` | Asset | Texture3D | Texture:Texture3D, Coord:uint3, Mip:int, Normal Intensity:float |
| 4 `Fetch` | Asset | TextureRamp | Texture:TextureRamp, Coord:int, Mip:int, Normal Intensity:float |
| 4 `Fetch` | any | Texture2DInt | Texture:Texture2DInt, Coord:int2, Mip:int |
| 4 `Fetch` | any but Asset | Texture2D | Texture:Texture2D, Coord:int2, Mip:int |
| 4 `Fetch` | any but Asset | Texture2DArray | Texture:Texture2DArray, Coord:int2, Index:int, Mip:int |
| 4 `Fetch` | any but Asset | Texture3D | Texture:Texture3D, Coord:uint3, Mip:int |
| 4 `Fetch` | any but Asset | TextureRamp | Texture:TextureRamp, Coord:int, Mip:int |
| 4 `Fetch`, 5 `Point` | Asset | TextureCube | Texture:TextureCube, Normal Intensity:float |
| 4 `Fetch`, 5 `Point` | any but Asset | TextureCube | Texture:TextureCube |
| 5 `Point` | Asset | Texture2D | Texture:Texture2D, UV:float2, Mip:int, Normal Intensity:float |
| 5 `Point` | Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Mip:int, Normal Intensity:float |
| 5 `Point` | Asset | Texture3D | Texture:Texture3D, UVW:float3, Mip:int, Normal Intensity:float |
| 5 `Point` | Asset | TextureRamp | Texture:TextureRamp, U:float, Mip:int, Normal Intensity:float |
| 5 `Point` | any | Texture2DInt | Texture:Texture2DInt, UV:float2, Mip:int |
| 5 `Point` | any but Asset | Texture2D | Texture:Texture2D, UV:float2, Mip:int |
| 5 `Point` | any but Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Mip:int |
| 5 `Point` | any but Asset | Texture3D | Texture:Texture3D, UVW:float3, Mip:int |
| 5 `Point` | any but Asset | TextureRamp | Texture:TextureRamp, U:float, Mip:int |
| 6 `Catmull` | Asset | Texture2D | Texture:Texture2D, UV:float2, Sharpness:float, Normal Intensity:float |
| 6 `Catmull` | Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Sharpness:float, Normal Intensity:float |
| 6 `Catmull` | Asset | Texture3D | Texture:Texture3D, UVW:float3, Sharpness:float, Normal Intensity:float |
| 6 `Catmull` | Asset | TextureCube | Texture:TextureCube, Direction:float3, Sharpness:float, Normal Intensity:float |
| 6 `Catmull` | Asset | TextureRamp | Texture:TextureRamp, U:float, Sharpness:float, Normal Intensity:float |
| 6 `Catmull` | any | Texture2DInt | Texture:Texture2DInt, UV:float2, Sharpness:float |
| 6 `Catmull` | any but Asset | Texture2D | Texture:Texture2D, UV:float2, Sharpness:float |
| 6 `Catmull` | any but Asset | Texture2DArray | Texture:Texture2DArray, UV:float2, Index:int, Sharpness:float |
| 6 `Catmull` | any but Asset | Texture3D | Texture:Texture3D, UVW:float3, Sharpness:float |
| 6 `Catmull` | any but Asset | TextureCube | Texture:TextureCube, Direction:float3, Sharpness:float |
| 6 `Catmull` | any but Asset | TextureRamp | Texture:TextureRamp, U:float, Sharpness:float |

**outputs**

| Normal Space | texture_data | texture_type | outputs |
|---|---|---|---|
| 0 `Tangent Space for UV0`, 1 `Tangent Space for UV1`, 2 `Tangent Space Auto Calculated` | Asset | any but Texture2DInt | Color:float4, Tangent Normal:float3 |
| 3 `Object Space` | Asset | any but Texture2DInt | Color:float4, Object Normal:float3 |
| — | Asset, Color | Texture2DInt | Int:int |
| — | Auto Exposure | any | Exposure:float, Luminance:float |
| — | Bent Normal, Unpack Normal | any | Normal:float3 |
| — | Color | any but Texture2DInt | Color:float4 |
| — | Curvature | any | Curvature:float |
| — | DoF Mask | any | Far Mask:float, Near Mask:float |
| — | GBuffer Albedo | any | Albedo:float3, Occlusion:float |
| — | GBuffer Features | any | Bevel:float, Cavity Mask:float, Convexity Mask:float |
| — | GBuffer Normal | any | Normal:float3, Roughness:float |
| — | GBuffer Shading | any | Metalness:float, Specular:float, Translucent:float, Microfiber:float |
| — | GBuffer Velocity | any | Velocity:float2 |
| — | Linear Depth, Native Depth | any | Depth:float |
| — | Refraction Mask | any | Refraction Mask:uint |
| — | SSAO | any | Ambient Occlusion:float |
| — | Transparent Blur | any | Transparent Blur:float |

### Settings Sky Up

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Sun Direction

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### SurfaceParameters

5 configurations.

**inputs**

| inputs |
|---|
| Screen Position:int2 |

**outputs**

| outputs |
|---|
| Node ID:int, Surface:int, Instance:int, Material ID:uint, Light Map:uint |

### Texture2D

27 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| outputs |
|---|
| checker_d.texture:Texture2D |

### Texture2DArray

27 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| outputs |
|---|
| noise.texture:Texture2DArray |

### Texture2DInt

27 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| outputs |
|---|
| checker_d.texture:Texture2DInt |

### Texture3D

27 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| outputs |
|---|
| curl_noise_3d.texture:Texture3D |

### TextureCube

27 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| outputs |
|---|
| environment_default.texture:TextureCube |

### Time

6 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| outputs |
|---|
| (unnamed):float |

### TransformSpace

16 configurations.

**inputs**

| From | inputs |
|---|---|
| 0 `Camera World` | Camera World:undefined |
| 1 `Object` | Object:undefined |
| 2 `View` | View:undefined |
| 3 `Absolute World` | Absolute World:undefined |

**outputs**

| To | outputs |
|---|---|
| 0 `Camera World` | Camera World:undefined |
| 1 `Object` | Object:undefined |
| 2 `View` | View:undefined |
| 3 `Absolute World` | Absolute World:undefined |

### Up

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Vertex Binormal

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Vertex Normal

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### Vertex Position

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `Camera World` | Camera World:float3 |
| 1 `Object` | Object:float3 |
| 2 `View` | View:float3 |
| 3 `Absolute World` | Absolute World:float3 |

### Vertex Tangent

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### View Direction

4 configurations.

**inputs**

| inputs |
|---|
| - |

**outputs**

| Space | outputs |
|---|---|
| 0 `World` | World:float3 |
| 1 `Object` | Object:float3 |
| 2 `Tangent` | Tangent:float3 |
| 3 `View` | View:float3 |

### _equal

2 configurations.

**inputs**

| Mode | inputs |
|---|---|
| 0 `In(a,b) Out(return)` | A:undefined, B:undefined |
| 1 `In(a,b,epsilon) Out(return)` | A:float, B:float, Epsilon:float |

**outputs**

| outputs |
|---|
| (unnamed):bool |

### matrix4Col

2 configurations.

**inputs**

| Mode | inputs |
|---|---|
| 0 `In(coll_0,coll_1,coll_2) Out(return)` | Coll 0:float3, Coll 1:float3, Coll 2:float3 |
| 1 `In(coll_0,coll_1,coll_2,coll_3) Out(return)` | Coll 0:undefined, Coll 1:undefined, Coll 2:undefined, Coll 3:undefined |

**outputs**

| outputs |
|---|
| (unnamed):float4x4 |

### matrix4Row

2 configurations.

**inputs**

| Mode | inputs |
|---|---|
| 0 `In(row_0,row_1,row_2) Out(return)` | Row 0:undefined, Row 1:undefined, Row 2:undefined |
| 1 `In(row_0,row_1,row_2,row_3) Out(return)` | Row 0:undefined, Row 1:undefined, Row 2:undefined, Row 3:undefined |

**outputs**

| outputs |
|---|
| (unnamed):float4x4 |

### orthonormalize

2 configurations.

**inputs**

| Mode | inputs |
|---|---|
| 0 `In(mat) Out(return)` | Matrix:float3x3 |
| 1 `In(x,y,z) Out(x,y,z)` | X:float3, Y:float3, Z:float3 |

**outputs**

| Mode | outputs |
|---|---|
| 0 `In(mat) Out(return)` | (unnamed):float3x3 |
| 1 `In(x,y,z) Out(x,y,z)` | X:float3, Y:float3, Z:float3 |

### scale

2 configurations.

**inputs**

| Mode | inputs |
|---|---|
| 0 `In(value) Out(return)` | Value:float3 |
| 1 `In(x,y,z) Out(return)` | X:float, Y:float, Z:float |

**outputs**

| outputs |
|---|
| (unnamed):float3x3 |

### sin

2 configurations.

**inputs**

| inputs |
|---|
| Radians:undefined |

**outputs**

| Mode | outputs |
|---|---|
| 0 `In(radians) Out(return)` | (unnamed):undefined |
| 1 `In(radians) Out(sin,cos)` | Sine:undefined, Cosine:undefined |

### translate

2 configurations.

**inputs**

| Mode | inputs |
|---|---|
| 0 `In(position) Out(return)` | Position:float3 |
| 1 `In(x,y,z) Out(return)` | X:float, Y:float, Z:float |

**outputs**

| outputs |
|---|
| (unnamed):float4x4 |

### vogelDisk

2 configurations.

**inputs**

| Mode | inputs |
|---|---|
| 0 `In(i,count) Out(return)` | I:uint, Count:uint |
| 1 `In(i,count,noise) Out(return)` | I:uint, Count:uint, Noise:float |

**outputs**

| outputs |
|---|
| (unnamed):float2 |

## Configurations that do not compile

One, and it is checked rather than assumed. `sin` in mode **`In(radians) Out(sin,cos)`** produces a material that fails to build in every pass:

```
hlsl.hlsl:7429:5: error: use of undeclared identifier 'sin'
                  sin(in0,out0,out1);
```

The declaration is in the SDK at `data/core/materials/shaders/render/graph/base.h:55-58`, under the comment `// sincos`:

```c
void sin(float radians, out float sin, out float cos) {}
```

That whole file sits inside `#ifdef UNIGINE_SKIP` - declarations only, mapped onto HLSL builtins, with the real bodies in `common.h` next to it. HLSL's two-output function is called `sincos`, and no `sin` taking three arguments exists, so the generated call resolves to nothing. Two of the four overloads also declare mismatched widths (`float3` in, `float2` out).

It is the only configuration of its kind: of every multi-output declaration in the graph headers, these four `sin` overloads are the only ones with an empty body. Everything else - `_bits_and`, `_decompose_float_by_exponent`, the matrix setters - carries a real implementation.

**Use `In(radians) Out(return)` and a separate `cos` node.**

## The Function node

`Function` has no fixed pins at all. It parses the UUSL you write into `props[0]` and builds its pins from the signature, so the row in the table above is the example it starts with rather than a description of the node.

One input pin per argument, one output pin per `out` argument, and one more output for the return value when the function returns something.

**Argument names become pin labels through `String::prettyFormat`**, and the rule matters because it is not the identity:

1. `_` becomes a space, and `PBR`, `UV`, `HCV`, `HLS`, `HSL`, `HSI` get spaces around them.
2. Words also split at a lowercase-to-uppercase boundary, at any of `` .,*-+/\|^%@#&`~!?[]{}()<> ``, and after `texture`, `2d`, `3d`.
3. Each word is looked up in a vocabulary of about a hundred entries. A hit is replaced: `dir` becomes **Direction**, `vec` **Vector**, `mat` **Matrix**, `tex` **Texture**, `coef` **Coefficient**, `min` **Minimum**, `max` **Maximum**, `pow` **Power**, `ifps` **IFps**, `ddx` **DDX**. A miss is capitalised.
4. The words are joined with single spaces.

| you write | the pin is called |
|---|---|
| `float a` | `A` |
| `float ray_origin` | `Ray Origin` |
| `float rayOrigin` | `Ray Origin` |
| `float RAY_ORIGIN` | `RAY ORIGIN` |
| `float tex_coord` | `Texture Coord` |
| `float min` | `Minimum` |
| `out float c` | `C` |
| `return` | named after the return type |

So an argument called `min` gives a pin labelled `Minimum`, and a link written against `"min"` is dropped. Avoid the vocabulary words above in argument names, or work the label out by the rule before you write the link.

Source: `String::prettyFormat` in `source/engine/api/UnigineString.cpp`, called from `MatNodeFunction::update`.

## The Expression node

`Expression` computes its output from its one input with the text in `props[0]`:

```json
"props": { "prop": { "label": "", "widget": "Code", "string": "x * 0.5, y" } }
```

- `x`, `y`, `z`, `w`, or a swizzle such as `xy`, stand for the input's channels. A channel the input does not have makes the node invalid.
- Commas separate the output's channels, four at most. `x * 0.5, y` on a `float2` gives a `float2`; `x,y,z` on a `float4` gives a `float3`.
- The rest of the text goes into the shader as written, so shader intrinsics (`frac`, `sin`, `dot`, `lerp`) and the functions of `core/materials/shaders/render/common.h` work in it. One of those is the hash `nrand(float2 seed)`, which returns a value in [0, 1).
- The output takes the input's scalar type (`bool` counts as `int`) and as many channels as the text produces.

One node does the work of a chain of math nodes. Three random values from one seed, on a `float2` input that carries (step, seed):

```
nrand(float2(x, y + 7.0)), nrand(float2(x, y + 8.0)), nrand(float2(x, y + 9.0))
```

A text that does not compile logs `Failed to call expression` when the graph is generated. The output label is the text, set only after the graph has loaded, so a link out of an `Expression` carries `output_id` (R5 in the README).

Source: `MatNodeExpression::validate` and `MatNodeExpression::generate` in `source/editor2/apps/editor/src/material_editor/MaterialGraphNodes.cpp`; `nrand` is in `data/core/materials/shaders/render/common.h`.

## Combobox choices

`props` are read by position, so the index below is the index to write. A combobox value is the position of the choice in this list.

**`Back`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Branch`**
  - prop[0] Mode: 0=Flatten, 1=Branch, 2=Auto

**`Camera Direction`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Camera Position`**
  - prop[0] Space: 0=Camera World, 1=Object, 2=View, 3=Absolute World

**`Decal Projected Normal`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Decal Projected Position`**
  - prop[0] Space: 0=Camera World, 1=Object, 2=View, 3=Absolute World

**`Decal Scene Normal`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Decal Scene Position`**
  - prop[0] Space: 0=Camera World, 1=Object, 2=View, 3=Absolute World

**`Down`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Forward`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Left`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`MaterialParameters`**
  - prop[0] Type: 0=Scene, 1=Opaque, 2=Transparent, 3=Decal, 4=Water

**`Moon Direction`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Object Position`**
  - prop[0] Space: 0=Camera World, 1=Object, 2=View, 3=Absolute World

**`Right`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`RotateSpace`**
  - prop[0] From: 0=World, 1=Object, 2=Tangent, 3=View
  - prop[1] To: 0=World, 1=Object, 2=Tangent, 3=View

**`SampleTexture`**
  - prop[0] Type: 0=Default, 1=Mip, 2=Mip offset, 3=Grad, 4=Fetch, 5=Point, 6=Catmull, 7=Cubic, 8=Cubic Mip, 9=Manual linear

**`Settings Sky Up`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Sun Direction`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`SurfaceParameters`**
  - prop[0] Type: 0=Scene, 1=Opaque, 2=Transparent, 3=Decal, 4=Water

**`Texture2D`**
  - prop[1] Wrap X: 0=Repeat, 1=Clamp, 2=Border
  - prop[2] Wrap Y: 0=Repeat, 1=Clamp, 2=Border
  - prop[3] Wrap Z: 0=Repeat, 1=Clamp, 2=Border

**`Texture2DArray`**
  - prop[1] Wrap X: 0=Repeat, 1=Clamp, 2=Border
  - prop[2] Wrap Y: 0=Repeat, 1=Clamp, 2=Border
  - prop[3] Wrap Z: 0=Repeat, 1=Clamp, 2=Border

**`Texture2DInt`**
  - prop[1] Wrap X: 0=Repeat, 1=Clamp, 2=Border
  - prop[2] Wrap Y: 0=Repeat, 1=Clamp, 2=Border
  - prop[3] Wrap Z: 0=Repeat, 1=Clamp, 2=Border

**`Texture3D`**
  - prop[1] Wrap X: 0=Repeat, 1=Clamp, 2=Border
  - prop[2] Wrap Y: 0=Repeat, 1=Clamp, 2=Border
  - prop[3] Wrap Z: 0=Repeat, 1=Clamp, 2=Border

**`TextureCube`**
  - prop[1] Wrap X: 0=Repeat, 1=Clamp, 2=Border
  - prop[2] Wrap Y: 0=Repeat, 1=Clamp, 2=Border
  - prop[3] Wrap Z: 0=Repeat, 1=Clamp, 2=Border

**`Time`**
  - prop[0] Mode: 0=Game, 1=Real
  - prop[1] Type: 0=Auto, 1=Current, 2=Old

**`TransformSpace`**
  - prop[0] From: 0=Camera World, 1=Object, 2=View, 3=Absolute World
  - prop[1] To: 0=Camera World, 1=Object, 2=View, 3=Absolute World

**`Up`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Vertex Binormal`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Vertex Normal`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`Vertex Position`**
  - prop[0] Space: 0=Camera World, 1=Object, 2=View, 3=Absolute World

**`Vertex Tangent`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`View Direction`**
  - prop[0] Space: 0=World, 1=Object, 2=Tangent, 3=View

**`_equal`**
  - prop[0] Mode: 0=In(a,b) Out(return), 1=In(a,b,epsilon) Out(return)

**`matrix4Col`**
  - prop[0] Mode: 0=In(coll_0,coll_1,coll_2) Out(return), 1=In(coll_0,coll_1,coll_2,coll_3) Out(return)

**`matrix4Row`**
  - prop[0] Mode: 0=In(row_0,row_1,row_2) Out(return), 1=In(row_0,row_1,row_2,row_3) Out(return)

**`orthonormalize`**
  - prop[0] Mode: 0=In(mat) Out(return), 1=In(x,y,z) Out(x,y,z)

**`scale`**
  - prop[0] Mode: 0=In(value) Out(return), 1=In(x,y,z) Out(return)

**`sin`**
  - prop[0] Mode: 0=In(radians) Out(return), 1=In(radians) Out(sin,cos)

**`translate`**
  - prop[0] Mode: 0=In(position) Out(return), 1=In(x,y,z) Out(return)

**`vogelDisk`**
  - prop[0] Mode: 0=In(i,count) Out(return), 1=In(i,count,noise) Out(return)


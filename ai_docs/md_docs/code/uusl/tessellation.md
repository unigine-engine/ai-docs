# UUSL Tessellation


Since UUSL supports tessellation, there are additional functions, semantics and parameters for tessellation shaders.


Tessellation requires new shader types: hull (also known as control) shader and evaluation (also known as domain). Hull shaders have a `*.hull` extension, evaluation shaders have a `*.eval` extension.


The essential thing of the tessellation is *SET_QUAD_DOMAIN* define. It defines the type of tessellator input: if you use it the tessellator will have quads input, otherwise triangles.

 Prior KnowledgeThis article assumes you have prior knowledge of the tessellation. Also, read the following topics before proceeding:
- *[UUSL Data Types and Common Intrinsic Functions](../../code/uusl/types.md)*
- *[UUSL Textures](../../code/uusl/textures.md)*
- *[UUSL Semantics](../../code/uusl/semantics.md)*
- *[UUSL Parameters](../../code/uusl/parameters.md)*


## Tessellation Attributes


You should specify the tessellation attributes in **both** tessellation shaders (hull and evaluation). These attributes defines the type of patches, and primitive topologies.


### Domain Patch Type


If you have used the *SET_QUAD_DOMAIN* define, the engine will use the quad patches:


```glsl
#define DOMAIN_PATCH [domain("quad")]
#define DOMAIN_PATCH_VERTICES 4

```


Otherwise, the engine will use triangle patches:


```glsl
#define DOMAIN_PATCH [domain("tri")]
#define DOMAIN_PATCH_VERTICES 3

```


### Partitioning Scheme


Partitioning scheme of the tessellator is defined by the *SET_PARTITIONING* function:


## SET_PARTITIONING ( value VALUE )

Specifies the partitioning scheme the tessellator should use for dividing patches.
### Arguments

- *value* **VALUE** - The partitioning attribute. The value can be one of the following:

  - *PARTITIONING_FRAC_ODD* - the tessellation factor is rounded to the next odd integer within the **[min;max]** range. **Equivalents** ```glsl [partitioning("fractional_odd")] ```
  - *PARTITIONING_FRAC_EVEN* - the tessellation factor is rounded to the next even integer within the **[min;max]** range. **Equivalents** ```glsl [partitioning("fractional_even")] ```
  - *PARTITIONING_POW2* - the tessellation is rounded to the next greatest power of 2, yielding the effective range [1, 2, 4, 8, 16, 32, 64]. **Equivalents** ```glsl [partitioning("pow2")] ```
  - *PARTITIONING_INTEGER* - the tessellation factor is always rounded up to the nearest integral value, in the range within the **[min;max]** range. **Equivalents** ```glsl [partitioning("Integer")] ```


### Tessellation Output Primitive Type


## SET_TOPOLOGY_PRIMITIVE ( value VALUE )

Defines the output primitive type for the tessellator.
### Arguments

- *value* **VALUE** - The output primitive type attribute. The value can be one of the following:

  - *TRIANGLE_CW* means clockwise-wound triangles (vertices rotate clockwise around the triangle's center). **Equivalents** ```glsl [outputtopology("triangle_cw")] ```
  - *TRIANGLE_CCW* triangle_cw means counter-clockwise-wound triangles (vertices rotate counter-clockwise around the triangle's center). **Equivalents** ```glsl [outputtopology("triangle_ccw")] ```


## Tessellation Semantics


Redefined UUSL semantics allows you to create unified input\output shader structures for both graphics APIs.


### Hull (Control) Shader Semantics


Initialization semantics for hull (control) shader:


| UUSL | Direct3D | Description |
|---|---|---|
| *INIT_CONTROL_IN(TYPE,NUM)* | *TYPE data_ ## NUM : TEXCOORD ## NUM;* | Adds (initializes) a control (hull) shader input semantic. |
| *INIT_CONTROL_OUT* | *TYPE data_ ## NUM : TEXCOORD ## NUM;* | Adds (initializes) a control shader output data semantic. |


Here is a usage example of hull shader input and output structure:


```glsl
STRUCT(CONTROL_IN)
	INIT_POSITION
	INIT_CONTROL_IN(float4,0)
	INIT_CONTROL_IN(float3,1)
END

STRUCT(CONTROL_OUT)
	INIT_POSITION
	INIT_CONTROL_OUT(float4,0)
END

// end of structures

```


Use the following pre-defined variables to use the input\output control shader semantics:


| UUSL | Direct3D | Description |
|---|---|---|
| *OUT_PATCH_EDGE(INDEX)* | *output.edges[INDEX]* | Defines the tessellation amount on each edge of a patch. |
| *OUT_CONTROL_DATA(NUM)* | *output.data_ ## NUM* | An output texture coordinates variable. |
| *IN_CONTROL_DATA(NUM,ID)* | *input[ ## ID ## ].data_ ## NUM* | An input texture coordinates variable. |
| *OUT_CONTROL_POSITION* | *output.position* | An output position system-value variable. |
| *IN_CONTROL_POSITION(ID)* | *input[ ## ID ## ].position* | An input position variable. |
| *CONTROL_POINT_ID* | *---* | Contains the coordinate of the vertex within the current patch. |


If you have used the *SET_QUAD_DOMAIN* define, you should specify the index for this output semantic:


| UUSL | Direct3D | Description |
|---|---|---|
| *OUT_PATCH_INSIDE(INDEX)* | *output.inside[INDEX]* | Defines the tessellation amount within a patch surface. |
| *OUT_PATCH_INSIDE* | *output.inside* | Defines the tessellation amount within a patch surface. |


### Evaluation (Domain) Shader Semantics


Initialization semantics:


| UUSL | Direct3D | Description |
|---|---|---|
| *INIT_EVALUATE_IN(TYPE,NUM)* | *TYPE data_ ## NUM : TEXCOORD ## NUM;* | Adds an input data semantic. |
| *INIT_EVALUATE_OUT(TYPE,NUM)* | *TYPE data_ ## NUM : TEXCOORD ## NUM;* | Adds an output data semantic. |


Here is a usage example of evaluation shader input and output structure:


```glsl
STRUCT(EVALUATE_IN)
	INIT_POSITION
	INIT_EVALUATE_IN(float4,0)
END

STRUCT(EVALUATE_OUT)
	INIT_POSITION
	INIT_EVALUATE_OUT(float2,0)
	INIT_EVALUATE_OUT(float3,1)
	INIT_EVALUATE_OUT(float3,2)
	INIT_EVALUATE_OUT(float3,3)
	INIT_EVALUATE_OUT(float,4)
END

// end of structures

```


Use the following pre-defined variables to use the input\output control shader semantics:


| UUSL | Direct3D | Description |
|---|---|---|
| *OUT_EVALUATE_DATA(NUM)* | *output.data_ ## NUM* | An output texture coordinates variable. |
| *IN_EVALUATE_PATCH_DATA(NUM,ID)* | *input[ ## ID ## ].data_ ## NUM* | An input patch data semantic. |
| *OUT_EVALUATE_POSITION(NUM,ID)* | *output.position* | An output position system-value variable. |
| *IN_EVALUATE_PATCH_POSITION(ID)* | *input[ ## ID ## ].position* | An input patch data position semantic value. |
| *DOMAIN_LOCATION* | *patch_constant.coords* | Contains the coordinate of the vertex within the current patch. Defines the location on the hull of the current domain point being evaluated. |


## Tessellation Main Functions


### Control Shader Main Function


Hull shader requires the main shader function and patch constant function.


#### Patch Constant Function


To start and end the main function of the control patch constant data, use the following instructions:


```glsl
MAIN_PATCH_CONSTANT_BEGIN(CONTROL_IN)

	<your code here>

END_PATCH_CONSTANT

//end

```


This code is equivalent to:


```glsl
CONTROL_CONSTANT_OUT patch_constant(InputPatch<CONTROL_IN,DOMAIN_PATCH_VERTICES> input) {
CONTROL_CONSTANT_OUT output = (CONTROL_CONSTANT_OUT)0;

	<your code here>

return output; }
//

```


#### Hull Shader Function


To start and end the main function of the hull shader, use the following instructions:


```glsl
MAIN_CONTROL_BEGIN(CONTROL_OUT, CONTROL_IN)

	<your code here>

MAIN_CONTROL_END

//end

```


This code is equivalent to:


```glsl
DOMAIN_PATCH
[maxtessfactor(64.0f)]
[outputcontrolpoints(DOMAIN_PATCH_VERTICES)]
[patchconstantfunc("patch_constant")]
CONTROL_PARTITIONING_TYPE
CONTROL_TOPOLOGY_PRIMITIVE_TYPE
CONTROL_OUT main(InputPatch<CONTROL_IN,DOMAIN_PATCH_VERTICES> input,uint CONTROL_POINT_ID : SV_OUTPUTCONTROLPOINTID) {
	CONTROL_OUT output;

	<your code here>

return output; }

```


### Evaluation Shader Main Function


To start and end the main function of the evaluation shader, use the following instructions:


```glsl
MAIN_EVALUATE_BEGIN(EVALUATE_OUT, EVALUTATE_IN)

	<your code here>

MAIN_EVALUATE_END

//end

```


This code is equivalent to:


```glsl
DOMAIN_PATCH
EVALUATE_OUT main(EVALUATE_CONSTANT_IN patch_constant,const OutputPatch<EVALUATE_IN,DOMAIN_PATCH_VERTICES> input) {
	EVALUATE_OUT output;

	<your code here>

return output; }
//

```

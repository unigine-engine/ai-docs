# UUSL Keywords and Types


This documentation article contains information about keywords, data types, pre-defined variables, constants and other features of the UUSL. This information can be used as the reference document for writing shaders.


To start using UUSL, include the `core/materials/shaders/render/common.h` file.


```glsl
#include <core/materials/shaders/render/common.h>
```


This header file is also used for fragment shader functions and scalar and double types and functions.


## Data Types


This articles contains different data types of UUSL.


| UUSL | Direct3D | Description |
|---|---|---|
| *int2* | *int2* | A vector with two 32-bit signed integer components. |
| *int3* | *int3* | A vector with three 32-bit signed integer components. |
| *int4* | *int4* | A vector with four 32-bit signed integer components. |
| *uint2* | *int2* | A vector with two 32-bit unsigned integer components. |
| *uint3* | *uint3* | A vector with three 32-bit unsigned integer components. |
| *uint4* | *uint4* | A vector with four 32-bit unsigned integer components. |
| *float* | *float* | A 32-bit floating point value. |
| *float2* | *float2* | A vector with two 32-bit floating point value components. |
| *float3* | *float3* | A vector with three 32-bit floating point value components. |
| *float4* | *float4* | A vector with four 32-bit floating point value components. |
| *float2x2* | *float2x2* | A matrix with 2 rows, 2 columns of 32-bit floating point value components. |
| *float3x3* | *float3x3* | A matrix with 3 rows, 3 columns of 32-bit floating point value components. |
| *float4x4* | *float4x4* | A matrix with 4 rows, 4 columns of 32-bit floating point value components. |
| *double2* | *double2* | A vector with two 64-bit double-precision floating point value components. |
| *double3* | *double3* | A vector with three 64-bit double-precision floating point value components. |
| *double4* | *double4* | A vector with four 64-bit double-precision floating point value components. |
| *double2x2* | *double2x2* | A matrix with 2 rows, 2 columns of 64-bit double-precision floating point value components. |
| *double3x3* | *double3x3* | A matrix with 3 rows, 3 columns of 64-bit double-precision floating point value components. |
| *double4x4* | *double4x4* | A matrix with 4 rows, 4 columns of 64-bit double-precision floating point value components. |
| *scalar* | *float / double* | A scalar value, which can be either *float* or *double* depending on precision (UNIGINE_DOUBLE flag). |
| *scalar2* | *float2 / double2* | A vector consisting of two scalar components, which can be either *float* or *double* depending on precision (UNIGINE_DOUBLE flag). |
| *scalar3* | *float3 / double3* | A vector consisting of three scalar components, which can be either *float* or *double* depending on precision (UNIGINE_DOUBLE flag). |
| *scalar4* | *float4 / double4* | A vector consisting of four scalar components, which can be either *double* or *float* depending on precision (UNIGINE_DOUBLE flag). |


Use these variable aliases when working with textures to make your shader's code readable:


| UUSL | Direct3D | Description |
|---|---|---|
| *TYPE_R* | *float* | A 32-bit floating point value. |
| *TYPE_RG* | *float2* | A vector with two 32-bit floating point value components. |
| *TYPE_RGB* | *float3* | A vector with three 32-bit floating point value components. |
| *TYPE_RGBA* | *float4* | A vector with four 32-bit floating point value components. |
| *TYPE_INT* | *int* | A 32-bit signed integer value. |
| *TYPE_UINT* | *uint* | A 32-bit unsigned integer value. |


Functions for type casting:


| Function | Description |
|---|---|
| int to_int(v) | Create an integer from the value. |
| int2 to_int2(v) | Create a two-component integer vector from the value. |
| int3 to_int3(v) | Create a three-component integer vector from the value. |
| int4 to_int4(v) | Create a four-component integer vector from the value. |
| uint to_uint(v) | Create an unsigned integer from the value. |
| uint2 to_uint2(v) | Create a two-component unsigned integer vector from the value. |
| uint3 to_uint3(v) | Create a three-component unsigned integer vector from the value. |
| uint4 to_uint4(v) | Create a four-component unsigned integer vector from the value. |
| float to_float(v) | Create a float from the value. |
| float2 to_float2(v) | Create a two-component floating-point vector from the value. |
| float3 to_float3(v) | Create a three-component floating-point vector from the value. |
| float4 to_float4(v) | Create a four-component floating-point vector from the value. |
| float4 to_gvec4(float v) | Create a four-component floating-point vector from the value. |
| float4 to_gvec4(float2 v) | Create a four-component floating-point vector from the two-component floating-point vector. |
| float4 to_gvec4(float3 v) | Create a four-component floating-point vector from the three-component floating-point vector. |
| float4 to_gvec4(float4 v) | Create a four-component floating-point vector from the four-component floating-point vector. |
| int4 to_gvec4(int v) | Create a four-component integer vector from the integer value. |
| int4 to_gvec4(int2 v) | Create a four-component integer vector from the two-component integer vector. |
| int4 to_gvec4(int3 v) | Create a four-component integer vector from the three-component integer vector. |
| int4 to_gvec4(int4 v) | Create a four-component integer vector from the four-component integer vector. |
| uint4 to_gvec4(uint v) | Create a four-component unsigned integer vector from the unsigned integer value. |
| uint4 to_gvec4(uint2 v) | Create a four-component unsigned integer vector from the two-component unsigned integer vector. |
| uint4 to_gvec4(uint3 v) | Create a four-component integer vector from the three-component unsigned integer vector. |
| uint4 to_gvec4(uint4 v) | Create a four-component unsigned integer vector from the four-component unsigned integer vector. |
| double to_double(v) | Create a double-precision value from the value. |
| double2 to_double2(v) | Create a two-component double-precision vector from the value. |
| double3 to_double3(v) | Create a three-component double-precision vector from the value. |
| double4 to_double4(v) | Create a four-component double-precision vector from the value. |
| scalar to_scalar(v) | Create a scalar value from the value. |
| scalar2 to_scalar2(v) | Create a two-component scalar value from the value. |
| scalar3 to_scalar3(v) | Create a three-component scalar value from the value. |
| scalar4 to_scalar4(v) | Create a four-component scalar value from the value. |


## Defined Values


| UUSL | Value |
|---|---|
| *float_isrgb* | 2.233333f |
| *float4_zero* | float4(0.0f,0.0f,0.0f,0.0f) |
| *float4_one* | float4(1.0f,1.0f,1.0f,1.0f) |
| *float4_half* | float4(0.5f,0.5f,0.5f,0.5f) |
| *float4_neg_one* | float4(-1.0f,-1.0f,-1.0f,-1.0f) |
| *float4_isrgb* | float4(float_isrgb,float_isrgb,float_isrgb,float_isrgb) |
| *float3_zero* | float3(0.0f,0.0f,0.0f) |
| *float3_one* | float3(1.0f,1.0f,1.0f) |
| *float3_half* | float3(0.5f,0.5f,0.5f) |
| *float3_neg_one* | float3(-1.0f,-1.0f,-1.0f) |
| *float3_up* | float3(0.0f,0.0f,1.0f) |
| *float3_isrgb* | float3(float_isrgb,float_isrgb,float_isrgb) |
| *float3_epsilon* | float3(EPSILON,EPSILON,EPSILON) |
| *float3_luma* | float3(0.299f,0.587f,0.114f) |
| *float2_zero* | float2(0.0f,0.0f) |
| *float2_one* | float2(1.0f,1.0f) |
| *float2_half* | float2(0.5f,0.5f) |
| *float2_neg_one* | float2(-1.0f,-1.0f) |
| *float2_isrgb* | float2(float_isrgb,float_isrgb) |
| *int4_zero* | int4(0,0,0,0) |
| *int4_one* | int4(1,1,1,1) |
| *int4_neg_one* | int4(-1,-1,-1,-1) |
| *int3_zero* | int3(0,0,0) |
| *int3_one* | int3(1,1,1) |
| *int3_neg_one* | int3(-1,-1,-1) |
| *int2_zero* | int2(0,0) |
| *int2_one* | int2(1,1) |
| *int2_neg_one* | int2(-1,-1) |
| *double3_zero* | double3(DF(0.0),DF(0.0),DF(0.0)) |
| *double3_one* | double3(DF(1.0),DF(1.0),DF(1.0)) |
| *float4x4_identity* | float4x4(1.0f,0.0f,0.0f,0.0f,0.0f,1.0f,0.0f,0.0f,0.0f,0.0f,1.0f,0.0f,0.0f,0.0f,0.0f,1.0f) |
| *PI* | 3.141592654f |
| *PI2* | 6.283185308f |
| *PI05* | 1.570796327f |
| *LOG2* | 0.693147181f |
| *LOG10* | 2.302585093f |
| *SQRT2* | 1.414213562f |
| *EPSILON* | 1e-6f |
| *INT_MAX* | 4294967294 |
| *INFINITY* | 1e+9f |
| *DEG2RAD* | PI / 180.0f |
| *RAD2DEG* | 180.0f / PI |
| *BYTE_UNORM_STEP* | 1.0f / 255.0f |
| *WIREFRAME_DEPTH_BIAS* | -0.001f - if *s_taa* is 1.0f; otherwise, -0.0001f |
| *[STATICARRAY](#static_arrays) (float2,halton16,16)* | Array containing Halton sequence. |
| *[STATICARRAY](#static_arrays) (float2,halton8,8)* | Array containing Halton sequence. |
| *[STATICARRAY](#static_arrays) (uint,dither_pattern,16)* | Array containing disperced dither pattern. |
| *[STATICARRAY](#static_arrays) (float4,blue_noise_16x16,256)* | Array containing blue noise texture. |


Use the following defined values in [double-precision functions](../../code/uusl/common.md#double_functions).


| *PI_D* | DF(3.14159265358979323846) |
|---|---|
| *PI2_D* | DF(6.28318530717958647693) |
| *IPI2_D* | DF(0.15915494309189533576) |
| *PI05_D* | DF(1.57079632679489661923) |
| *DEG2RAD_D* | DF(0.01745329251994329577) |
| *RAD2DEG_D* | DF(57.29577951308232087685) |
| *EPSILON_D* | 1e-7 |


## Bit masking defined values

The following defined values are reserved bits of the [*Material* mask](../../principles/bit_masking/index.md).


| *SSAO_BIT* | 1<<31 |
|---|---|
| *SSR_BIT* | 1<<30 |
| *SSS_BIT* | 1<<29 |
| *DOF_BIT* | 1<<28 |
| *MOTION_BLUR_BIT* | 1<<27 |
| *SHADOW_SHAFTS_BIT* | 1<<26 |
| *LIGHTMAP_WITH_AMBIENT_BIT* | 1<<25 |
| *SHORELINE_WETNESS_BIT* | 1<<24 |
| *FREE_MATERIAL_MASK* | 0x00FFFFFF |
| *RESERVED_MATERIAL_MASK* | 0xFF000000 |


## Main Function


### Void Main Function


To start and end the void Main function of the fragment shader (when you don't need to provide the output color value but depth), use the following instructions:


```glsl
STRUCT_FRAG_BEGIN
STRUCT_FRAG_END

MAIN_FRAG_BEGIN(FRAGMENT_IN)
	<your code here>
MAIN_FRAG_END

```


This code is equivalent to:


```glsl
void main(FRAGMENT_IN IN) {
	<your code here>
}

```


### Main Function with Return Value


To start and end the *Main* function with return value, use the following instructions:


```glsl
STRUCT_FRAG_BEGIN
    INIT_COLOR(float4)
STRUCT_FRAG_END

MAIN_FRAG_BEGIN(FRAGMENT_IN)
	<your code here>
MAIN_FRAG_END

```


This code is equivalent to:


```glsl
FRAGMENT_OUT main(FRAGMENT_IN IN) {
	FRAGMENT_OUT OUT;
	<your code here>
return OUT; }

```


### Geometry Shader Main Function


To start and end the *Main* function of the geometry shader, use the following instructions:


```glsl
STRUCT(GEOMETRY_IN)
	INIT_POSITION
	<input members>
END

STRUCT(GEOMETRY_OUT)
	INIT_POSITION
	<output members>
END

MAIN_GEOM_BEGIN(GEOMETRY_OUT, GEOMETRY_IN)
	<your code here>
MAIN_GEOM_END

```


This code is equivalent to:


```glsl
[maxvertexcount(MAX_VERTICES_GEOM)]
void main(TYPE_GEOM_IN GEOMETRY_IN IN[COUNT_GEOM_IN],inout TYPE_GEOM_OUT<GEOMETRY_OUT> stream) {
	GEOMETRY_OUT OUT;
	<your code here>
}

```


## Global Variables


To define a global variable, use the following syntax:


```glsl
GLOBAL <your var>
```


This is equal to the following HLSL command:


```glsl
uniform <your var>
```


## Static Variables and Arrays


### Static Variables


To define a static variable, use the following syntax:


```glsl
STATICVAR <your var>
```


This is equal to the following HLSL command:


```glsl
static const <your var>
```


### Static Arrays


To work with static arrays by using UUSL, use the following instructions:


```glsl
STATICARRAY(TYPE,NAME,SIZE)
	<your array members>
ENDARRAY

```


- ***TYPE*** - the type of the array (float, etc.).
- ***NAME*** - the name of the array.
- ***SIZE*** - the size of the array.


This code block is equivalent to:


```glsl
static const TYPE NAME [SIZE] = {<your array members>};
```


## Blending Presets


UUSL contains blending presets. When you specify the type of blending in material, the UUSL wrapper automatically defines a new definition, that you can use in your shader:


| Blending type | UUSL |
|---|---|
| *BLEND_SRC_FUNC_SRC_ALPHA && BLEND_DEST_FUNC_ONE_MINUS_SRC_ALPHA* | *BLEND_ALPHABLEND* |
| *BLEND_SRC_FUNC_ONE && BLEND_DEST_FUNC_ONE* | *BLEND_ADDITIVE* |
| *BLEND_SRC_FUNC_DEST_COLOR && BLEND_DEST_FUNC_ZERO* | *BLEND_MULTIPLICATIVE* |
| *BLEND_SRC_FUNC_NONE && BLEND_DEST_FUNC_NONE* | *BLEND_NONE* |


## HLSL features


### HLSL Flow Control Attributes


| UUSL | Direct3D | Description |
|---|---|---|
| *branch* | *[branch]* | Performs branching using control flow instructions. |
| *call* | *[call]* | Prevents inlining of a function. |
| *flatten* | *[flatten]* | Performs branching using conditional move instructions. |
| *ifAll* | *[ifAll]* | Executes the conditional part of an **if** statement when the condition is true for all threads on which the current shader is running. |
| *ifAny* | *[ifAny]* | Executes the conditional part of an **if** statement when the condition is true for any thread on which the current shader is running. |
| *isolate* | *[isolate]* | Optimizes the specified HLSL code independently of the surrounding code. |
| *loop* | *[loop]* | Gives preference to flow control constructs. |
| *maxexports* | *[maxexports]* | Specifies the maximum number of export instructions that will execute along any path from the entry point to an exit. |
| *maxInstructionCount* | *[maxInstructionCount]* | Sets the maximum number of instructions available to a shader. |
| *maxtempreg* | *[maxtempreg]* | Restricts temporary register usage to the number of registers specified. Generates a compiler error if unsuccessful. |
| *noExpressionOptimizations* | *[noExpressionOptimizations]* | Avoids optimization of expressions. |
| *predicate* | *[predicate]* | Performs branching by using predication. |
| *predicateBlock* | *[predicateBlock]* | Performs branching by using predicated **exec** blocks. |
| *reduceTempRegUsage* | *[reduceTempRegUsage]* | Restricts temporary register usage to the number of registers specified. Generates a compiler warning if unsuccessful. |
| *removeUnusedInputs* | *[removeUnusedInputs]* | Removes unused interpolator inputs from pixel shaders. |
| *sampreg* | *[sampreg]* | Sets the ranges of pixel sampler and vertex sampler registers used by the compiler. |
| *unroll* | *[unroll]* | Avoids flow control constructs. |
| *unused* | *[unused]* | Suppresses warnings about unused shader parameters. |
| *xps* | *[xps]* | Specifies that all vertex fetch operations are done after the last vfetch instruction. This instruction is used to reduce the latency back to the command processor to free the vertex buffer. |
| *earlydepthstencil* | *[earlydepthstencil]* | Forces [depth-stencil testing](https://msdn.microsoft.com/en-us/library/windows/desktop/ff471439(v=vs.85).aspx) before a shader executes. **Doesn't work with custom depth.** |


### Interpolation Modifiers


| UUSL | Direct3D | Description |
|---|---|---|
| *MODIFER_LINEAR* | *linear* | Interpolate between shader inputs; linear is the default value if no interpolation modifier is specified. |
| *MODIFER_CENTROID* | *centroid* | Interpolate between samples that are somewhere within the covered area of the pixel (this may require extrapolating end points from a pixel center). Centroid sampling may improve antialiasing if a pixel is partially covered (even if the pixel center is not covered). The centroid modifier must be combined with either the linear or noperspective modifier. |
| *MODIFER_NOINTERPOLATION* | *nointerpolation* | Do not interpolate. |
| *MODIFER_NOPERSPECTIVE* | *noperspective* | Do not perform perspective-correction during interpolation. The noperspective modifier can be combined with the centroid modifier. |
| *MODIFER_SAMPLE* | *sample* | Interpolate at sample location rather than at the pixel center. This causes the pixel shader to execute per-sample rather than per-pixel. |


#### See Also


See also the [article](https://msdn.microsoft.com/en-us/library/windows/desktop/bb509668(v=vs.85).aspx) on Interpolation Modifiers.


## Constants and Structs


### Structs


In UUSL structs is the way to organize the bunch of input and output data.


To start using structs in your shader code, use the following instructions:


```glsl
STRUCT(NAME)
	<your data>
END

```


- ***NAME*** - the name of the struct.


Here is an example of vertex shader input struct:


```glsl
// Input vertex data
STRUCT(VERTEX_IN)
	INIT_ATTRIBUTE(float4,0,POSITION)	// Vertex position
	INIT_ATTRIBUTE(float4,1,TEXCOORD0)	// Vertex texcoord (uv)
	INIT_ATTRIBUTE(float4,2,TEXCOORD1)	// Vertex basis tangent
	INIT_ATTRIBUTE(float4,3,TEXCOORD2)	// Vertex color
END

```


After that, you should pass the `VERTEX_IN` struct to the main function of the vertex shader.


### Constants


For using constant buffer in your shader code, use the following instructions:


```glsl
CBUFFER(NAME)
	<your data>
END

```


- ***NAME*** - the name of the cbuffer.


Here is an example of using constant buffer:


```glsl
CBUFFER(parameters)
	UNIFORM float grayscale_power;
END

```


If you defined this parameter in the material, you'll be able to specify this value.


### See Also


- How to use the *CBUFFER* instruction in the [tutorial](../../code/uusl/create_post.md) on shaders for post-process pass.


## For Loop


There is a for loop implemented in UUSL:


```glsl
forloop(NAME,BEGIN,END)
```


```glsl
for(int NAME = (BEGIN); NAME < (END); NAME++)
```


The keyword for is used to describe a loop that is controlled by a counter (**NAME**). The parentheses enclose three expressions that initialize, check and update the variable used as counter. The body defined by curly braces encloses the statements that are executed at each pass of the loop.


Here is an example of a for loop:


```glsl
forloop(i, 0, 99)
{
	aFunction();
}

```


## Shader Export


To export shader, use the following command:


```glsl
EXPORT_SHADER(FILE)
```


- ***FILE*** - The name of the file.


This command exports the shader program into a file: for Direct3D the file will have an `.hlsl` extension.


The command expands all of the predefined UUSL syntax and creates shader files in native languages for both graphic APIs.

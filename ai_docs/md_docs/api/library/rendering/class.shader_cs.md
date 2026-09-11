# Unigine.Shader Class (CS)


Interface for shader manipulation. Here, *shader* is a shader program that can contain several subshaders - vertex, fragment, geometry, etc.


This class allows compiling these shader programs, setting parameter values, and binding graphic context.


You can also set parameters (or arrays of parameters) to shader programs.


### Usage Example


This example demonstrates how to use your custom subshaders (UUSL, HLSL) to render a post-effect.


Create a new *ShaderTest* component, double-click it to open in the default IDE and paste the following code to `ShaderTest.cs` file.


```csharp
public partial class ShaderTest : Component
{
	Shader shader;

	//// implementing the event handler to render the result
	void endscreen_event_handler()
	{
		// Getting a post RenderTarget to render to
		RenderTarget rt = Renderer.PostRenderTarget;
		rt.UnbindAll();
		rt.BindColorTexture(0, Renderer.TextureColor);
		rt.Enable();

		// Binding our shader and rendering the screen via FFP
		shader.Bind();
		// setting the fill color to magenta
		shader.SetParameterFloat4("color", new vec4(1.0f, 0.0f, 1.0f, 1.0f));
		shader.FlushParameters();
		Ffp.RenderScreen();

		// Unbinding the shader and disabling the target
		shader.Unbind();

		rt.Disable();
	}

	void Init()
	{

		// String containing the source code of the vertex shader (HLSL, UUSL)
		string vertex_shader = @"
float4 main(float2 pos : POSITION) : SV_POSITION
{
	return float4(pos, 0.0f, 1.0f);
}
";

		// String containing the source code of the fragment shader (HLSL, UUSL)
		string fragment_shader = @"
cbuffer vars : register(b0)
{
	float4 color;
};

float4 main(float4 fragCoord : SV_POSITION) : SV_TARGET
{
	return color;
}
";

		shader = new Shader();

		// Compiling a shader with the vertex and fragment subshaders
		shader.CompileVertFrag(vertex_shader, fragment_shader,"");

		// Or you can call the "compile()" function as follows - the result will be the same
		// shader.Compile(vertex_shader,null,fragment_shader,null,null,null,"");

		// Adding a render EndScreen event to render the result as a post-effect
		Render.EventEndScreen.Connect(endscreen_event_handler);
	}
}

```


## Shader Class

### Enums

## WARNING_MODE

Warning mode for the shader compiler.
| Name | Description |
|---|---|
| **DISABLE** = 0 | All shader compilation warnings are ignored. Using this mode is not recommended as it may result in driver and OS crashes, so you use it at your own risk. |
| **SOFT** = 1 | All shader compilation warnings are printed to log, but ignored. You can use this mode if you have checked and you're absolutely sure that the warnings do not cause driver or OS crashes. |
| **HARD** = 2 | All warnings are treated as errors. This level is used by default. |

## SUB_SHADER

| Name | Description |
|---|---|
| **VERTEX** = 0 | Vertex subshader. |
| **CONTROL** = 1 | Control subshader. |
| **EVALUATE** = 2 | Evaluation subshader. |
| **GEOMETRY** = 3 | Geometry subshader. |
| **FRAGMENT** = 4 | Fragment subshader. |
| **COMPUTE** = 5 | Compute subshader. |

### Properties

## bool IEEEStrictness

The value indicating if the shader compiler forces the IEEE strict compilation.
> **Notice:** Available for DirectX only.

## bool DisableExport

The value indicating if shader [export to a file](../../../code/uusl/index.md#uusl_debug) is disabled. By default UNIGINE enables exporting a shader program to a file (e.g. for debug purposes). Shader files are created in a native language for the graphic API (*Direct3D* - `.hlsl` extension).
## bool DisableCompileError

The value indicating if the shader compile error output is disabled.
## Shader.WARNING_MODE WarningMode

The warning mode for the shader compiler.
You can choose modes from the lowest (all shader compilation warnings are ignored) up to the highest level, when warnings are treated as errors. By default the *highest* level is used, setting *lower* levels may result in driver and OS crashes, so you use them at your own risk. The *[soft](#WARNING_MODE_SOFT)* level can be used if you have checked and you're absolutely sure that the warnings do not cause crashes.

> **Notice:** Available for DirectX only.

## int OptimizationLevel

The optimization level for the shader compiler.
One of the following values:


- 0 - Directs the compiler to skip optimization steps during code generation.
- 1 - Directs the compiler to use the lowest optimization level. At this level the compiler might produce slower code but produces the code quicker.
- 2 - Directs the compiler to use the second lowest optimization level.
- 3 - Directs the compiler to use the second highest optimization level.
- 4 - Directs the compiler to use the highest optimization level. At this level the compiler produces the best possible code but might take significantly longer to do so.


> **Notice:** Available for DirectX only.


## bool DisableCompileCache

The value indicating if compilation cache for the shader is disabled.
### Members

---

## Shader ( )

Default shader constructor.
## Shader ( string name )

Shader constructor. Loads all existing shaders with the given name.
### Arguments

- *string* **name** - Shader name.

## Shader ( string name , string defines )

Shader constructor. Loads all existing shaders with the given name.
### Arguments

- *string* **name** - Shader name.
- *string* **defines** - User defines.

## Shader ( string vertex , string fragment , string defines )

Shader constructor. Loads only vertex and fragment subshaders with the given names.
### Arguments

- *string* **vertex** - Vertex subshader name or source.
- *string* **fragment** - Fragment subshader name or source.
- *string* **defines** - User defines.

## void Bind ( )

Binds shader.
## void Clear ( )

Clears shader.
## bool Compile ( string vertex , string geometry , string fragment , string compute , string control , string evaluate , string defines = "" , ulong key_cache = 0 )

Compiles the shader with the specified subshaders. To skip a subshader, pass nullptr instead of an argument. Depending on the subshaders types, additional values are added automatically to the *defines* argument: *VERTEX, CONTROL, EVALUATE, GEOMETRY, FRAGMENT*.
### Arguments

- *string* **vertex** - Vertex subshader path.
- *string* **geometry** - Geometry subshader path.
- *string* **fragment** - Fragment subshader path.
- *string* **compute** - Compute subshader path.
- *string* **control** - Control subshader path.
- *string* **evaluate** - Evaluation subshader path.
- *string* **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *ulong* **key_cache** - Key cache.

### Return value

**true** if the shader is compiled successfully; otherwise, **false**.
## void Destroy ( )

Destroys shader.
## int FindParameter ( string name )

Finds shader parameter.
### Arguments

- *string* **name** - Fast identifier.

### Return value

Parameter identifier, if found; otherwise, **-1**.
## void FlushParameters ( )

Flushes shader parameters.
## void Unbind ( )

Unbinds shader.
## void SetParameterFloat ( int id , float value )

Sets shader float parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *float* **value** - Parameter value to be set.

## void SetParameterFloat ( string name , float value )

Sets shader float parameter value by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *float* **value** - Parameter value to be set.

## void SetParameterFloat2 ( int id , vec2 value )

Sets a shader parameter value for the float2 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *vec2* **value** - Parameter value to be set.

## void SetParameterFloat2 ( string name , vec2 value )

Sets a shader parameter value for the float2 variable.
### Arguments

- *string* **name** - Parameter name.
- *vec2* **value** - Parameter value to be set.

## void SetParameterFloat3 ( int id , vec3 value )

Sets a shader parameter value for the float3 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *vec3* **value** - Parameter value to be set.

## void SetParameterFloat3 ( string name , vec3 value )

Sets a shader parameter value for the float3 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec3* **value** - Parameter value to be set.

## void SetParameterFloat4 ( int id , vec4 value )

Sets a shader parameter value for the float4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *vec4* **value** - Parameter value to be set.

## void SetParameterFloat4 ( string name , vec4 value )

Sets a shader parameter value for the float4 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec4* **value** - Parameter value to be set.

## void SetParameterFloat3x3 ( int id , mat3 value )

Sets a shader parameter value for the float3x3 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *mat3* **value** - Parameter value to be set.

## void SetParameterFloat3x3 ( string name , mat3 value )

Sets a shader parameter value for the float3x3 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *mat3* **value** - Parameter value to be set.

## void SetParameterFloat4x4 ( int id , mat4 value )

Sets a shader parameter value for the float4x4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *mat4* **value** - Parameter value to be set.

## void SetParameterFloat4x4 ( string name , mat4 value )

Sets a shader parameter value for the float4x4 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *mat4* **value** - Parameter value to be set.

## void SetParameterInt ( int id , int value )

Sets a shader parameter value for the int variable.
### Arguments

- *int* **id** - Parameter identifier.
- *int* **value** - Parameter value to be set.

## void SetParameterInt ( string name , int value )

Sets a shader parameter value for the int variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *int* **value** - Parameter value to be set.

## void SetParameterInt2 ( int id , ivec2 value )

Sets a shader parameter value for the int2 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *ivec2* **value** - Parameter value to be set.

## void SetParameterInt2 ( string name , ivec2 value )

Sets a shader parameter value for the int2 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *ivec2* **value** - Parameter value to be set.

## void SetParameterInt3 ( int id , ivec3 value )

Sets a shader parameter value for the int3 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *ivec3* **value** - Parameter value to be set.

## void SetParameterInt3 ( string name , ivec3 value )

Sets a shader parameter value for the int3 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *ivec3* **value** - Parameter value to be set.

## void SetParameterInt4 ( int id , ivec4 value )

Sets a shader parameter value for the int4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *ivec4* **value** - Parameter value to be set.

## void SetParameterInt4 ( string name , ivec4 value )

Sets a shader parameter value for the int4 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *ivec4* **value** - Parameter value to be set.

## void SetParameterDouble ( int id , double value )

Sets a shader parameter value for the double variable.
### Arguments

- *int* **id** - Parameter identifier.
- *double* **value** - Parameter value to be set.

## void SetParameterDouble ( string name , double value )

Sets a shader parameter value for the double variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *double* **value** - Parameter value to be set.

## void SetParameterDouble2 ( int id , dvec2 value )

Sets a shader parameter value for the double2 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *dvec2* **value** - Parameter value to be set.

## void SetParameterDouble2 ( string name , dvec2 value )

Sets a shader parameter value for the double2 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *dvec2* **value** - Parameter value to be set.

## void SetParameterDouble3 ( int id , dvec3 value )

Sets a shader parameter value for the double3 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *dvec3* **value** - Parameter value to be set.

## void SetParameterDouble3 ( string name , dvec3 value )

Sets a shader parameter value for the double3 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *dvec3* **value** - Parameter value to be set.

## void SetParameterDouble4 ( int id , dvec4 value )

Sets a shader parameter value for the double4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *dvec4* **value** - Parameter value to be set.

## void SetParameterDouble4 ( string name , dvec4 value )

Sets a shader parameter value for the double4 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *dvec4* **value** - Parameter value to be set.

## void SetParameterDouble4x4 ( int id , dmat4 value )

Sets a shader parameter value for the double4x4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *dmat4* **value** - Parameter value to be set.

## void SetParameterDouble4x4 ( string name , dmat4 value )

Sets a shader parameter value for the double4x4 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *dmat4* **value** - Parameter value to be set.

## void SetParameterScalar ( int id , Scalar value )

Sets a shader parameter value for the scalar variable using the parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *Scalar* **value** - Parameter value to be set.

## void SetParameterScalar ( string name , Scalar value )

Sets a shader parameter value for the scalar variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *Scalar* **value** - Parameter value to be set.

## void SetParameterScalar2 ( int id , vec2 value )

Sets a shader parameter value for the scalar2 variable using the parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *vec2* **value** - Parameter value to be set.

## void SetParameterScalar2 ( string name , vec2 value )

Sets a shader parameter value for the scalar2 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec2* **value** - Parameter value to be set.

## void SetParameterScalar3 ( int id , vec3 value )

Sets a shader parameter value for the scalar3 variable using the parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *vec3* **value** - Parameter value to be set.

## void SetParameterScalar3 ( string name , vec3 value )

Sets a shader parameter value for the scalar3 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec3* **value** - Parameter value to be set.

## void SetParameterScalar4 ( int id , vec4 value )

Sets a shader parameter value for the scalar4 variable using the parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *vec4* **value** - Parameter value to be set.

## void SetParameterScalar4 ( string name , vec4 value )

Sets a shader parameter value for the scalar4 variable using the parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec4* **value** - Parameter value to be set.

## void SetParameterArrayFloat ( int id , float[] value , int num_elements )

Sets shader float array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *float[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayFloat ( string name , float[] value , int num_elements )

Sets shader float array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *float[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayFloat ( int id , float[] value )

Sets shader float array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *float[]* **value** - Parameter value to be set.

## void SetParameterArrayFloat ( string name , float[] value )

Sets shader float array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *float[]* **value** - Parameter value to be set.

## void SetParameterArrayFloat2 ( int id , vec2[] value , int num_elements )

Sets shader float2 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *vec2[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayFloat2 ( string name , vec2[] value , int num_elements )

Sets shader float2 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec2[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayFloat2 ( int id , vec2[] value )

Sets shader float2 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *vec2[]* **value** - Parameter value to be set.

## void SetParameterArrayFloat2 ( string name , vec2[] value )

Sets shader float2 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec2[]* **value** - Parameter value to be set.

## void SetParameterArrayFloat4 ( int id , vec4[] value , int num_elements )

Sets shader float4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *vec4[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayFloat4 ( string name , vec4[] value , int num_elements )

Sets shader float4 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec4[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayFloat4 ( int id , vec4[] value )

Sets shader float4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *vec4[]* **value** - Parameter value to be set.

## void SetParameterArrayFloat4 ( string name , vec4[] value )

Sets shader float4 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *vec4[]* **value** - Parameter value to be set.

## void SetParameterArrayFloat4x4 ( int id , mat4[] value , int num_elements )

Sets shader float4x4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *mat4[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayFloat4x4 ( string name , mat4[] value , int num_elements )

Sets shader float4x4 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *mat4[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayFloat4x4 ( int id , mat4[] value )

Sets shader float4x4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *mat4[]* **value** - Parameter value to be set.

## void SetParameterArrayFloat4x4 ( string name , mat4[] value )

Sets shader float4x4 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *mat4[]* **value** - Parameter value to be set.

## void SetParameterArrayInt ( int id , int[] value , int num_elements )

Sets shader integer array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *int[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayInt ( string name , int[] value , int num_elements )

Sets shader integer array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *int[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayInt ( int id , int[] value )

Sets shader integer array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *int[]* **value** - Parameter value to be set.

## void SetParameterArrayInt ( string name , int[] value )

Sets shader integer array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *int[]* **value** - Parameter value to be set.

## void SetParameterArrayInt2 ( int id , ivec2[] value , int num_elements )

Sets shader int2 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *ivec2[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayInt2 ( string name , ivec2[] value , int num_elements )

Sets shader int2 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *ivec2[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayInt2 ( int id , ivec2[] value )

Sets shader int2 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *ivec2[]* **value** - Parameter value to be set.

## void SetParameterArrayInt2 ( string name , ivec2[] value )

Sets shader int2 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *ivec2[]* **value** - Parameter value to be set.

## void SetParameterArrayInt4 ( int id , ivec4[] value , int num_elements )

Sets shader int4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *ivec4[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayInt4 ( string name , ivec4[] value , int num_elements )

Sets shader int4 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *ivec4[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayInt4 ( int id , ivec4[] value )

Sets shader int4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *ivec4[]* **value** - Parameter value to be set.

## void SetParameterArrayInt4 ( string name , ivec4[] value )

Sets shader int4 array parameter values by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *ivec4[]* **value** - Parameter value to be set.

## void SetParameterArrayDouble ( int id , double[] value , int num_elements )

Sets shader double parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *double[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayDouble ( string name , double[] value , int num_elements )

Sets shader double parameter value by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *double[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayDouble ( int id , double[] value )

Sets shader double parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *double[]* **value** - Parameter value to be set.

## void SetParameterArrayDouble ( string name , double[] value )

Sets shader double parameter value by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *double[]* **value** - Parameter value to be set.

## void SetParameterArrayDouble2 ( int id , dvec2[] value , int num_elements )

Sets shader double2 parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *dvec2[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayDouble2 ( string name , dvec2[] value , int num_elements )

Sets shader double2 parameter value by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *dvec2[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayDouble2 ( int id , dvec2[] value )

Sets shader double2 parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *dvec2[]* **value** - Parameter value to be set.

## void SetParameterArrayDouble2 ( string name , dvec2[] value )

Sets shader double2 parameter value by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *dvec2[]* **value** - Parameter value to be set.

## void SetParameterArrayDouble4 ( int id , dvec4[] value , int num_elements )

Sets shader double4 parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *dvec4[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayDouble4 ( string name , dvec4[] value , int num_elements )

Sets shader double4 parameter value by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *dvec4[]* **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void SetParameterArrayDouble4 ( int id , dvec4[] value )

Sets shader double4 parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *dvec4[]* **value** - Parameter value to be set.

## void SetParameterArrayDouble4 ( string name , dvec4[] value )

Sets shader double4 parameter value by using given parameter name.
### Arguments

- *string* **name** - Parameter name.
- *dvec4[]* **value** - Parameter value to be set.

## bool CompileCompute ( string compute , string defines = "" , ulong key_cache = 0 )

Compiles the shader with the specified compute subshader. The additional *COMPUTE* value is added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *compute* argument.
### Arguments

- *string* **compute** - Compute subshader path.
- *string* **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *ulong* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## bool CompileVertFrag ( string vertex , string fragment , string defines = "" , ulong key_cache = 0 )

Compiles the shader with the specified vertex and fragment subshaders. The additional *VERTEX* and *FRAGMENT* values are added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *vertex* and *fragment* arguments.
### Arguments

- *string* **vertex** - Vertex subshader path.
- *string* **fragment** - Fragment subshader path.
- *string* **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *ulong* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## bool CompileVertGeomFrag ( string vertex , string geometry , string fragment , string defines = "" , ulong key_cache = 0 )

Compiles the shader with the specified vertex, geometry, and fragment subshaders. The additional *VERTEX*, *GEOMETRY*, and *FRAGMENT* values are added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *vertex*, *fragment*, and *geometry* arguments.
### Arguments

- *string* **vertex** - Vertex subshader path.
- *string* **geometry** - Geometry subshader path.
- *string* **fragment** - Fragment subshader path.
- *string* **defines** - User defines (for example, "DIRECT3D12", or any other).
- *ulong* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## bool CompileShader ( string shader , string defines = "" , ulong key_cache = 0 )

Compiles the shader that includes subshaders. Depending on the types of the subshaders defined in the shader file, additional values are added to the *defines* argument automatically: *VERTEX, CONTROL, EVALUATE, GEOMETRY, FRAGMENT*.
### Arguments

- *string* **shader** - Shader path.
- *string* **defines** - User defines (for example, "DIRECT3D12", or any other).
- *ulong* **key_cache** - Key cache.

### Return value

trueif the shader with all the subshaders compiled successfully; otherwise, false.
## bool ValidateShader ( Shader.SUB_SHADER type , string shader , string defines = "" )

Validates the shader (whether it can be compiled or not).
### Arguments

- *[Shader.SUB_SHADER](../../../api/library/rendering/class.shader_cs.md#SUB_SHADER)* **type** - Subshader type.
- *string* **shader** - Shader path.
- *string* **defines** - User defines (for example, "DIRECT3D12", or any other).

### Return value

true if the shader can be compiled; otherwise, false.

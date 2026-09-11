# Unigine.Shader Class (CPP)

**Header:** #include <UnigineShader.h>


Interface for shader manipulation. Here, *shader* is a shader program that can contain several subshaders - vertex, fragment, geometry, etc.


This class allows compiling these shader programs, setting parameter values, and binding graphic context.


You can also set parameters (or arrays of parameters) to shader programs.


### Usage Example


This example demonstrates how to use your custom subshaders (UUSL, HLSL) to render a post-effect.


Add the following code to the `AppWorldLogic.cpp` file.


```cpp
#include <UnigineFfp.h>

using namespace Unigine;

ShaderPtr shader;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

//// implementing the event handler to render the result
void endscreen_event_handler()
{
	// Getting a post RenderTarget to render to
	const auto rt = Renderer::getPostRenderTarget();
	rt->unbindAll();
	rt->bindColorTexture(0, Renderer::getTextureColor());
	rt->enable();

	// Binding our shader and rendering the screen via FFP
	shader->bind();
	// setting the fill color to magenta
	shader->setParameterFloat4("color", Math::vec4(1.0f, 0.0f, 1.0f, 1.0f));
	shader->flushParameters();
	Ffp::renderScreen();

	// Unbinding the shader and disabling the target
	shader->unbind();

	rt->disable();
}

int AppWorldLogic::init()
{

	// String containing the source code of the vertex shader (HLSL, UUSL)
	const auto vertex_shader = R"foo(
	float4 main(float2 pos : POSITION) : SV_POSITION
	{
		return float4(pos, 0.0f, 1.0f);
	}
	)foo";

	// String containing the source code of the fragment shader (HLSL, UUSL)
	const auto fragment_shader = R"foo(
	cbuffer vars : register(b0)
	{
		float4 color;
	};

	float4 main(float4 fragCoord : SV_POSITION) : SV_TARGET
	{
		return color;
	}
	)foo";

	shader = Shader::create();

	// Compiling a shader with the vertex and fragment subshaders
	shader->compileVertFrag(vertex_shader, fragment_shader, "");

	// Or you can call the "compile()" function as follows - the result will be the same
	// shader->compile(vertex_shader,nullptr,fragment_shader,nullptr,nullptr,nullptr,"");

	// Adding a render EndScreen event to render the result as a post-effect
	Render::getEventEndScreen().connect(econnections, endscreen_event_handler);

	return 1;
}

int AppWorldLogic::shutdown()
{
	// removing all event subscriptions somewhere on shutdown
	econnections.disconnectAll();

	return 1;
}


```


## Shader Class

### Enums

## WARNING_MODE

Warning mode for the shader compiler.
| Name | Description |
|---|---|
| **WARNING_MODE_DISABLE** = 0 | All shader compilation warnings are ignored. Using this mode is not recommended as it may result in driver and OS crashes, so you use it at your own risk. |
| **WARNING_MODE_SOFT** = 1 | All shader compilation warnings are printed to log, but ignored. You can use this mode if you have checked and you're absolutely sure that the warnings do not cause driver or OS crashes. |
| **WARNING_MODE_HARD** = 2 | All warnings are treated as errors. This level is used by default. |

## SUB_SHADER

| Name | Description |
|---|---|
| **SUB_SHADER_VERTEX** = 0 | Vertex subshader. |
| **SUB_SHADER_CONTROL** = 1 | Control subshader. |
| **SUB_SHADER_EVALUATE** = 2 | Evaluation subshader. |
| **SUB_SHADER_GEOMETRY** = 3 | Geometry subshader. |
| **SUB_SHADER_FRAGMENT** = 4 | Fragment subshader. |
| **SUB_SHADER_COMPUTE** = 5 | Compute subshader. |

### Members

## void setIEEEStrictness ( bool ieeestrictness )

Sets a new value indicating if the shader compiler forces the IEEE strict compilation.
> **Notice:** Available for DirectX only.

### Arguments

- *bool* **ieeestrictness** - Set **true** to enable forcing of IEEE strict compilation by the shader compiler; **false** - to disable it.

## bool isIEEEStrictness () const

Returns the current value indicating if the shader compiler forces the IEEE strict compilation.
> **Notice:** Available for DirectX only.

### Return value

**true** if forcing of IEEE strict compilation by the shader compiler is enabled ; otherwise **false**.
## void setDisableExport ( bool export )

Sets a new value indicating if shader [export to a file](../../../code/uusl/index.md#uusl_debug) is disabled. By default UNIGINE enables exporting a shader program to a file (e.g. for debug purposes). Shader files are created in a native language for the graphic API (*Direct3D* - `.hlsl` extension).
### Arguments

- *bool* **export** - Set **true** to enable disabling of shader export to a file; **false** - to disable it.

## bool isDisableExport () const

Returns the current value indicating if shader [export to a file](../../../code/uusl/index.md#uusl_debug) is disabled. By default UNIGINE enables exporting a shader program to a file (e.g. for debug purposes). Shader files are created in a native language for the graphic API (*Direct3D* - `.hlsl` extension).
### Return value

**true** if disabling of shader export to a file is enabled ; otherwise **false**.
## void setDisableCompileError ( bool error )

Sets a new value indicating if the shader compile error output is disabled.
### Arguments

- *bool* **error** - Set **true** to enable disabling of shader compile errors output; **false** - to disable it.

## bool isDisableCompileError () const

Returns the current value indicating if the shader compile error output is disabled.
### Return value

**true** if disabling of shader compile errors output is enabled ; otherwise **false**.
## void setWarningMode ( Shader::WARNING_MODE mode )

Sets a new warning mode for the shader compiler.
You can choose modes from the lowest (all shader compilation warnings are ignored) up to the highest level, when warnings are treated as errors. By default the *highest* level is used, setting *lower* levels may result in driver and OS crashes, so you use them at your own risk. The *[soft](#WARNING_MODE_SOFT)* level can be used if you have checked and you're absolutely sure that the warnings do not cause crashes.

> **Notice:** Available for DirectX only.

### Arguments

- *[Shader::WARNING_MODE](../../../api/library/rendering/class.shader_cpp.md#WARNING_MODE)* **mode** - The warning mode.

## Shader::WARNING_MODE getWarningMode () const

Returns the current warning mode for the shader compiler.
You can choose modes from the lowest (all shader compilation warnings are ignored) up to the highest level, when warnings are treated as errors. By default the *highest* level is used, setting *lower* levels may result in driver and OS crashes, so you use them at your own risk. The *[soft](#WARNING_MODE_SOFT)* level can be used if you have checked and you're absolutely sure that the warnings do not cause crashes.

> **Notice:** Available for DirectX only.

### Return value

Current warning mode.
## void setOptimizationLevel ( int level )

Sets a new optimization level for the shader compiler.
One of the following values:


- 0 - Directs the compiler to skip optimization steps during code generation.
- 1 - Directs the compiler to use the lowest optimization level. At this level the compiler might produce slower code but produces the code quicker.
- 2 - Directs the compiler to use the second lowest optimization level.
- 3 - Directs the compiler to use the second highest optimization level.
- 4 - Directs the compiler to use the highest optimization level. At this level the compiler produces the best possible code but might take significantly longer to do so.


> **Notice:** Available for DirectX only.


### Arguments

- *int* **level** - The optimization level.

## int getOptimizationLevel () const

Returns the current optimization level for the shader compiler.
One of the following values:


- 0 - Directs the compiler to skip optimization steps during code generation.
- 1 - Directs the compiler to use the lowest optimization level. At this level the compiler might produce slower code but produces the code quicker.
- 2 - Directs the compiler to use the second lowest optimization level.
- 3 - Directs the compiler to use the second highest optimization level.
- 4 - Directs the compiler to use the highest optimization level. At this level the compiler produces the best possible code but might take significantly longer to do so.


> **Notice:** Available for DirectX only.


### Return value

Current optimization level.
## void setDisableCompileCache ( bool cache )

Sets a new value indicating if compilation cache for the shader is disabled.
### Arguments

- *bool* **cache** - Set **true** to enable disabling of compilation cache for the shader; **false** - to disable it.

## bool isDisableCompileCache () const

Returns the current value indicating if compilation cache for the shader is disabled.
### Return value

**true** if disabling of compilation cache for the shader is enabled ; otherwise **false**.
---

## static ShaderPtr create ( )

Default shader constructor.
## static ShaderPtr create ( const char * name )

Shader constructor. Loads all existing shaders with the given name.
### Arguments

- *const char ** **name** - Shader name.

## static ShaderPtr create ( const char * name , const char * defines )

Shader constructor. Loads all existing shaders with the given name.
### Arguments

- *const char ** **name** - Shader name.
- *const char ** **defines** - User defines.

## static ShaderPtr create ( const char * vertex , const char * fragment , const char * defines )

Shader constructor. Loads only vertex and fragment subshaders with the given names.
### Arguments

- *const char ** **vertex** - Vertex subshader name or source.
- *const char ** **fragment** - Fragment subshader name or source.
- *const char ** **defines** - User defines.

## void bind ( ) const

Binds shader.
## void clear ( ) const

Clears shader.
## bool compile ( const char * vertex , const char * geometry , const char * fragment , const char * compute , const char * control , const char * evaluate , const char * defines = "" , unsigned long long key_cache = 0 )

Compiles the shader with the specified subshaders. To skip a subshader, pass nullptr instead of an argument. Depending on the subshaders types, additional values are added automatically to the *defines* argument: *VERTEX, CONTROL, EVALUATE, GEOMETRY, FRAGMENT*.
### Arguments

- *const char ** **vertex** - Vertex subshader path.
- *const char ** **geometry** - Geometry subshader path.
- *const char ** **fragment** - Fragment subshader path.
- *const char ** **compute** - Compute subshader path.
- *const char ** **control** - Control subshader path.
- *const char ** **evaluate** - Evaluation subshader path.
- *const char ** **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *unsigned long long* **key_cache** - Key cache.

### Return value

**true** if the shader is compiled successfully; otherwise, **false**.
## void destroy ( ) const

Destroys shader.
## int findParameter ( const char * name )

Finds shader parameter.
### Arguments

- *const char ** **name** - Fast identifier.

### Return value

Parameter identifier, if found; otherwise, **-1**.
## void flushParameters ( ) const

Flushes shader parameters.
## void unbind ( ) const

Unbinds shader.
## void setParameterFloat ( int id , float value )

Sets shader float parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *float* **value** - Parameter value to be set.

## void setParameterFloat ( const char * name , float value )

Sets shader float parameter value by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *float* **value** - Parameter value to be set.

## void setParameterFloat2 ( int id , const Math:: vec2 & value )

Sets a shader parameter value for the float2 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat2 ( const char * name , const Math:: vec2 & value )

Sets a shader parameter value for the float2 variable.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat3 ( int id , const Math:: vec3 & value )

Sets a shader parameter value for the float3 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat3 ( const char * name , const Math:: vec3 & value )

Sets a shader parameter value for the float3 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat4 ( int id , const Math:: vec4 & value )

Sets a shader parameter value for the float4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat4 ( const char * name , const Math:: vec4 & value )

Sets a shader parameter value for the float4 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat3x3 ( int id , const Math:: mat3 & value )

Sets a shader parameter value for the float3x3 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[mat3](../../../api/library/math/class.mat3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat3x3 ( const char * name , const Math:: mat3 & value )

Sets a shader parameter value for the float3x3 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[mat3](../../../api/library/math/class.mat3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat4x4 ( int id , const Math:: mat4 & value )

Sets a shader parameter value for the float4x4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterFloat4x4 ( const char * name , const Math:: mat4 & value )

Sets a shader parameter value for the float4x4 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterInt ( int id , int value )

Sets a shader parameter value for the int variable.
### Arguments

- *int* **id** - Parameter identifier.
- *int* **value** - Parameter value to be set.

## void setParameterInt ( const char * name , int value )

Sets a shader parameter value for the int variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **value** - Parameter value to be set.

## void setParameterInt2 ( int id , const Math:: ivec2 & value )

Sets a shader parameter value for the int2 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Parameter value to be set.

## void setParameterInt2 ( const char * name , const Math:: ivec2 & value )

Sets a shader parameter value for the int2 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Parameter value to be set.

## void setParameterInt3 ( int id , const Math:: ivec3 & value )

Sets a shader parameter value for the int3 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterInt3 ( const char * name , const Math:: ivec3 & value )

Sets a shader parameter value for the int3 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterInt4 ( int id , const Math:: ivec4 & value )

Sets a shader parameter value for the int4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterInt4 ( const char * name , const Math:: ivec4 & value )

Sets a shader parameter value for the int4 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterDouble ( int id , double value )

Sets a shader parameter value for the double variable.
### Arguments

- *int* **id** - Parameter identifier.
- *double* **value** - Parameter value to be set.

## void setParameterDouble ( const char * name , double value )

Sets a shader parameter value for the double variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *double* **value** - Parameter value to be set.

## void setParameterDouble2 ( int id , const Math:: dvec2 & value )

Sets a shader parameter value for the double2 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Parameter value to be set.

## void setParameterDouble2 ( const char * name , const Math:: dvec2 & value )

Sets a shader parameter value for the double2 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Parameter value to be set.

## void setParameterDouble3 ( int id , const Math:: dvec3 & value )

Sets a shader parameter value for the double3 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterDouble3 ( const char * name , const Math:: dvec3 & value )

Sets a shader parameter value for the double3 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterDouble4 ( int id , const Math:: dvec4 & value )

Sets a shader parameter value for the double4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterDouble4 ( const char * name , const Math:: dvec4 & value )

Sets a shader parameter value for the double4 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterDouble4x4 ( int id , const Math:: dmat4 & value )

Sets a shader parameter value for the double4x4 variable.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterDouble4x4 ( const char * name , const Math:: dmat4 & value )

Sets a shader parameter value for the double4x4 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterScalar ( int id , Math::Scalar value )

Sets a shader parameter value for the scalar variable using the parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *Math::Scalar* **value** - Parameter value to be set.

## void setParameterScalar ( const char * name , Math::Scalar value )

Sets a shader parameter value for the scalar variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *Math::Scalar* **value** - Parameter value to be set.

## void setParameterScalar2 ( int id , const Math:: Vec2 & value )

Sets a shader parameter value for the scalar2 variable using the parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[Vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Parameter value to be set.

## void setParameterScalar2 ( const char * name , const Math:: Vec2 & value )

Sets a shader parameter value for the scalar2 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[Vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Parameter value to be set.

## void setParameterScalar3 ( int id , const Math:: Vec3 & value )

Sets a shader parameter value for the scalar3 variable using the parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterScalar3 ( const char * name , const Math:: Vec3 & value )

Sets a shader parameter value for the scalar3 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Parameter value to be set.

## void setParameterScalar4 ( int id , const Math:: Vec4 & value )

Sets a shader parameter value for the scalar4 variable using the parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[Vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterScalar4 ( const char * name , const Math:: Vec4 & value )

Sets a shader parameter value for the scalar4 variable using the parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[Vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Parameter value to be set.

## void setParameterArrayFloat ( int id , const float * value , int num_elements )

Sets shader float array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const float ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayFloat ( const char * name , const float * value , int num_elements )

Sets shader float array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const float ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayFloat ( int id , const Vector <float> & value )

Sets shader float array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **value** - Parameter value to be set.

## void setParameterArrayFloat ( const char * name , const Vector <float> & value )

Sets shader float array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **value** - Parameter value to be set.

## void setParameterArrayFloat2 ( int id , const Math:: vec2 * value , int num_elements )

Sets shader float2 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayFloat2 ( const char * name , const Math:: vec2 * value , int num_elements )

Sets shader float2 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayFloat2 ( int id , const Vector < Math:: vec2 > & value )

Sets shader float2 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayFloat2 ( const char * name , const Vector < Math:: vec2 > & value )

Sets shader float2 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayFloat4 ( int id , const Math:: vec4 * value , int num_elements )

Sets shader float4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayFloat4 ( const char * name , const Math:: vec4 * value , int num_elements )

Sets shader float4 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayFloat4 ( int id , const Vector < Math:: vec4 > & value )

Sets shader float4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec4](../../../api/library/math/class.vec4_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayFloat4 ( const char * name , const Vector < Math:: vec4 > & value )

Sets shader float4 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec4](../../../api/library/math/class.vec4_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayFloat4x4 ( int id , const Math:: mat4 * value , int num_elements )

Sets shader float4x4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayFloat4x4 ( const char * name , const Math:: mat4 * value , int num_elements )

Sets shader float4x4 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayFloat4x4 ( int id , const Vector < Math:: mat4 > & value )

Sets shader float4x4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../api/library/math/class.mat4_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayFloat4x4 ( const char * name , const Vector < Math:: mat4 > & value )

Sets shader float4x4 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../api/library/math/class.mat4_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayInt ( int id , const int * value , int num_elements )

Sets shader integer array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const int ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayInt ( const char * name , const int * value , int num_elements )

Sets shader integer array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const int ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayInt ( int id , const Vector <int> & value )

Sets shader integer array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **value** - Parameter value to be set.

## void setParameterArrayInt ( const char * name , const Vector <int> & value )

Sets shader integer array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **value** - Parameter value to be set.

## void setParameterArrayInt2 ( int id , const Math:: ivec2 * value , int num_elements )

Sets shader int2 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayInt2 ( const char * name , const Math:: ivec2 * value , int num_elements )

Sets shader int2 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayInt2 ( int id , const Vector < Math:: ivec2 > & value )

Sets shader int2 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayInt2 ( const char * name , const Vector < Math:: ivec2 > & value )

Sets shader int2 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayInt4 ( int id , const Math:: ivec4 * value , int num_elements )

Sets shader int4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayInt4 ( const char * name , const Math:: ivec4 * value , int num_elements )

Sets shader int4 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayInt4 ( int id , const Vector < Math:: ivec4 > & value )

Sets shader int4 array parameter values by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayInt4 ( const char * name , const Vector < Math:: ivec4 > & value )

Sets shader int4 array parameter values by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayDouble ( int id , const double * value , int num_elements )

Sets shader double parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const double ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayDouble ( const char * name , const double * value , int num_elements )

Sets shader double parameter value by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const double ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayDouble ( int id , const Vector <double> & value )

Sets shader double parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<double> &* **value** - Parameter value to be set.

## void setParameterArrayDouble ( const char * name , const Vector <double> & value )

Sets shader double parameter value by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<double> &* **value** - Parameter value to be set.

## void setParameterArrayDouble2 ( int id , const Math:: dvec2 * value , int num_elements )

Sets shader double2 parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayDouble2 ( const char * name , const Math:: dvec2 * value , int num_elements )

Sets shader double2 parameter value by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayDouble2 ( int id , const Vector < Math:: dvec2 > & value )

Sets shader double2 parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayDouble2 ( const char * name , const Vector < Math:: dvec2 > & value )

Sets shader double2 parameter value by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayDouble4 ( int id , const Math:: dvec4 * value , int num_elements )

Sets shader double4 parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayDouble4 ( const char * name , const Math:: dvec4 * value , int num_elements )

Sets shader double4 parameter value by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) ** **value** - Parameter value to be set.
- *int* **num_elements** - The number of array elements.

## void setParameterArrayDouble4 ( int id , const Vector < Math:: dvec4 > & value )

Sets shader double4 parameter value by using given parameter id.
### Arguments

- *int* **id** - Parameter identifier.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md)> &* **value** - Parameter value to be set.

## void setParameterArrayDouble4 ( const char * name , const Vector < Math:: dvec4 > & value )

Sets shader double4 parameter value by using given parameter name.
### Arguments

- *const char ** **name** - Parameter name.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md)> &* **value** - Parameter value to be set.

## bool compileCompute ( const char * compute , const char * defines = "" , unsigned long long key_cache = 0 )

Compiles the shader with the specified compute subshader. The additional *COMPUTE* value is added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *compute* argument.
### Arguments

- *const char ** **compute** - Compute subshader path.
- *const char ** **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *unsigned long long* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## bool compileVertFrag ( const char * vertex , const char * fragment , const char * defines = "" , unsigned long long key_cache = 0 )

Compiles the shader with the specified vertex and fragment subshaders. The additional *VERTEX* and *FRAGMENT* values are added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *vertex* and *fragment* arguments.
### Arguments

- *const char ** **vertex** - Vertex subshader path.
- *const char ** **fragment** - Fragment subshader path.
- *const char ** **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *unsigned long long* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## bool compileVertGeomFrag ( const char * vertex , const char * geometry , const char * fragment , const char * defines = "" , unsigned long long key_cache = 0 )

Compiles the shader with the specified vertex, geometry, and fragment subshaders. The additional *VERTEX*, *GEOMETRY*, and *FRAGMENT* values are added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *vertex*, *fragment*, and *geometry* arguments.
### Arguments

- *const char ** **vertex** - Vertex subshader path.
- *const char ** **geometry** - Geometry subshader path.
- *const char ** **fragment** - Fragment subshader path.
- *const char ** **defines** - User defines (for example, "DIRECT3D12", or any other).
- *unsigned long long* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## bool compileShader ( const char * shader , const char * defines = "" , unsigned long long key_cache = 0 )

Compiles the shader that includes subshaders. Depending on the types of the subshaders defined in the shader file, additional values are added to the *defines* argument automatically: *VERTEX, CONTROL, EVALUATE, GEOMETRY, FRAGMENT*.
### Arguments

- *const char ** **shader** - Shader path.
- *const char ** **defines** - User defines (for example, "DIRECT3D12", or any other).
- *unsigned long long* **key_cache** - Key cache.

### Return value

trueif the shader with all the subshaders compiled successfully; otherwise, false.
## bool validateShader ( Shader::SUB_SHADER type , const char * shader , const char * defines = "" )

Validates the shader (whether it can be compiled or not).
### Arguments

- *[Shader::SUB_SHADER](../../../api/library/rendering/class.shader_cpp.md#SUB_SHADER)* **type** - Subshader type.
- *const char ** **shader** - Shader path.
- *const char ** **defines** - User defines (for example, "DIRECT3D12", or any other).

### Return value

true if the shader can be compiled; otherwise, false.

# Unigine.Shader Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Interface for shader manipulation. Here, *shader* is a shader program that can contain several subshaders - vertex, fragment, geometry, etc.


This class allows compiling these shader programs, setting parameter values, and binding graphic context.


You can also set parameters (or arrays of parameters) to shader programs.


### Usage Example


This example demonstrates how to use your custom subshaders (UUSL, HLSL) to render a post-effect.


## Shader Class

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
## void setWarningMode ( )

Sets a new warning mode for the shader compiler.
You can choose modes from the lowest (all shader compilation warnings are ignored) up to the highest level, when warnings are treated as errors. By default the *highest* level is used, setting *lower* levels may result in driver and OS crashes, so you use them at your own risk. The *[soft](#WARNING_MODE_SOFT)* level can be used if you have checked and you're absolutely sure that the warnings do not cause crashes.

> **Notice:** Available for DirectX only.

### Arguments

- **mode** - The warning mode.

## getWarningMode () const

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

## static Shader ( )

Default shader constructor.
## static Shader ( string name )

Shader constructor. Loads all existing shaders with the given name.
### Arguments

- *string* **name** - Shader name.

## static Shader ( string name , string defines )

Shader constructor. Loads all existing shaders with the given name.
### Arguments

- *string* **name** - Shader name.
- *string* **defines** - User defines.

## static Shader ( string vertex , string fragment , string defines )

Shader constructor. Loads only vertex and fragment subshaders with the given names.
### Arguments

- *string* **vertex** - Vertex subshader name or source.
- *string* **fragment** - Fragment subshader name or source.
- *string* **defines** - User defines.

## void bind ( )

Binds shader.
## void clear ( )

Clears shader.
## int compile ( string vertex , string geometry , string fragment , string compute , string control , string evaluate , string defines = "" , long key_cache = 0 )

Compiles the shader with the specified subshaders. To skip a subshader, pass nullptr instead of an argument. Depending on the subshaders types, additional values are added automatically to the *defines* argument: *VERTEX, CONTROL, EVALUATE, GEOMETRY, FRAGMENT*.
### Arguments

- *string* **vertex** - Vertex subshader path.
- *string* **geometry** - Geometry subshader path.
- *string* **fragment** - Fragment subshader path.
- *string* **compute** - Compute subshader path.
- *string* **control** - Control subshader path.
- *string* **evaluate** - Evaluation subshader path.
- *string* **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *long* **key_cache** - Key cache.

### Return value

**true** if the shader is compiled successfully; otherwise, **false**.
## void destroy ( )

Destroys shader.
## int findParameter ( string name )

Finds shader parameter.
### Arguments

- *string* **name** - Fast identifier.

### Return value

Parameter identifier, if found; otherwise, **-1**.
## void flushParameters ( )

Flushes shader parameters.
## void unbind ( )

Unbinds shader.
## int compileCompute ( string compute , string defines = "" , long key_cache = 0 )

Compiles the shader with the specified compute subshader. The additional *COMPUTE* value is added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *compute* argument.
### Arguments

- *string* **compute** - Compute subshader path.
- *string* **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *long* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## int compileVertFrag ( string vertex , string fragment , string defines = "" , long key_cache = 0 )

Compiles the shader with the specified vertex and fragment subshaders. The additional *VERTEX* and *FRAGMENT* values are added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *vertex* and *fragment* arguments.
### Arguments

- *string* **vertex** - Vertex subshader path.
- *string* **fragment** - Fragment subshader path.
- *string* **defines** - User defines (for example, "OPENGL", "DIRECT3D11", or any other).
- *long* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## int compileVertGeomFrag ( string vertex , string geometry , string fragment , string defines = "" , long key_cache = 0 )

Compiles the shader with the specified vertex, geometry, and fragment subshaders. The additional *VERTEX*, *GEOMETRY*, and *FRAGMENT* values are added automatically to the *defines* argument. This function is the same as the *[compile](#compile_cstr_cstr_cstr_cstr_cstr_cstr_cstr_ullong_int)()* function called only with the *vertex*, *fragment*, and *geometry* arguments.
### Arguments

- *string* **vertex** - Vertex subshader path.
- *string* **geometry** - Geometry subshader path.
- *string* **fragment** - Fragment subshader path.
- *string* **defines** - User defines (for example, "DIRECT3D12", or any other).
- *long* **key_cache** - Key cache.

### Return value

true if the shader compiled successfully; otherwise, false.
## int compileShader ( string shader , string defines = "" , long key_cache = 0 )

Compiles the shader that includes subshaders. Depending on the types of the subshaders defined in the shader file, additional values are added to the *defines* argument automatically: *VERTEX, CONTROL, EVALUATE, GEOMETRY, FRAGMENT*.
### Arguments

- *string* **shader** - Shader path.
- *string* **defines** - User defines (for example, "DIRECT3D12", or any other).
- *long* **key_cache** - Key cache.

### Return value

trueif the shader with all the subshaders compiled successfully; otherwise, false.
## int validateShader ( int type , string shader , string defines = "" )

Validates the shader (whether it can be compiled or not).
### Arguments

- *int* **type** - Subshader type.
- *string* **shader** - Shader path.
- *string* **defines** - User defines (for example, "DIRECT3D12", or any other).

### Return value

true if the shader can be compiled; otherwise, false.

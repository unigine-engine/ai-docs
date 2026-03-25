# Shaders


This type of node is used to describe a *[UUSL](../../../../code/uusl/index.md)* shader in an ULON-based material file. Currently, the engine supports *Vertex, Control, Evaluate, Geometry, Fragment*, and *Compute* shaders.


The syntax is the following:


```cpp
Shader name =
#{
	// UUSL code
#}

```


As a node's value you must specify a [UUSL](../../../../code/uusl/index.md)-based code enclosed in **"#{"** and **"#}"**.


See the `SDK/data/core/materials/shaders/render/` directory for the list of headers implementing common shaders' functions which can be included and used in custom shaders. To start writing UUSL shaders, include the common header:


```glsl
	#include <core/materials/shaders/render/common.h>

```


## Types of Shaders


The following types of shaders corresponding to their counterparts in different graphic APIs are available:


| **Unigine** | **[DirectX](https://docs.microsoft.com/en-us/windows/win32/direct3d11/overviews-direct3d-11-graphics-pipeline)** | **[OpenGL](https://www.khronos.org/opengl/wiki/Rendering_Pipeline_Overview)** |
|---|---|---|
| Vertex | Vertex | Vertex |
| Control | Hull | Control |
| Evaluate | Domain | Evaluate |
| Geometry | Geometry | Geometry |
| Fragment | Pixel | Fragment |
| Compute | Compute | Compute |


## Usage Examples


The shader node is usually used as a shader value for the *[Pass](../../../../code/formats/materials_formats/ulon_materials/passes.md)* node.


```cpp
Shader shader_a =
#{
	// some UUSL code
#}

Pass ambient
{
	Vertex = shader_a
	Fragment = shader_a
}

```


The advantages of this shader setup method are:


- It reduces the amount of identical code.
- One shader code can be used in different render passes.


On the other hand, it is not the best approach for large shaders. Use *includes* for these cases:


1. Write different shaders in separate files and then specify their paths as shader values in the pass: ```cpp // some UUSL code ``` ```cpp // some UUSL code ``` ```cpp Pass deferred { Vertex = "shaders/a.vert" Fragment = "shaders/b.frag" } ```
2. Include the code of a different shader by using the marker: **#shader shader_name**. ```cpp Shader a = #{ // shader code A #} Shader b = #{ // shader code B #shader a #} // the result shader b will look like this: Shader b = #{ // shader code B // shader code A #} ```

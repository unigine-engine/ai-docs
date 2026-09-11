# Unified Unigine Shader Language


The Unified UNIGINE shader language (UUSL) allows you to create a single shader file for all supported 3D graphics APIs: Direct3D 11, Direct3D 12, Vulkan and PS5. The language brings pre-defined data types and implemented functions that simplifies and unifies shaders writing process.


This section of the Unigine documentation contains information about the UUSL syntax (unified data types, intrinsic functions, parameters, textures, semantics, etc.) and tutorials on creating shaders.


## Frequently Asked Questions


### What is UUSL?


The Unified UNIGINE shader language (UUSL) is a wrapper, which wraps HLSL syntax and uses custom parsers for #ifdef constructs. You can use the UUSL instructions to write shader code without graphic API defining: it will work on all APIs.


### Should I write shaders by using UUSL only?


Definitely not. UUSL is just a wrapper which facilitates the shader-writing process. You can also use an old-school approach by writing separately part of the shader for corresponding graphic API with *HLSL* and PS5's shading languages.


### Which shader stages does the Unigine engine have?


Unigine engine has the standard shaders pipeline: *Vertex-Shader stage* → *Geometry-Shader stage* → *Fragment-Shader stage*. If you want to use tessellation, the pipeline will have 3 additional stages between vertex-shader and geometry-shader stages: *Control-Shader stage*, *tessellation stage*, *Evaluation-Shader stage*.


### How are materials and shaders interrelated?


Material specifies which shaders for defined [rendering pass](../../principles/render/sequence/index.md) it will use to render. You can define *vertex*, *geometry* and *fragment* shaders for a material. When you assign the material, the engine starts using its shaders to render the image. A piece of cake!


> **Notice:** Vertex and fragment shaders are mandatory for a material.


We have a neat article about the [materials files formats](../../code/formats/materials_formats/index.md), check it out.


### How to start using UUSL?


When you start writing shaders, include the UUSL headers and start coding!


Use the following commands to include the necessary headers:


```glsl
// Include Unified Unigine Shader Language (UUSL) common header
#include <core/materials/shaders/api/common.h>

```


### Do shaders need compilation?


Yes, they do. But the engine does the job: just use the *[`materials_reload`](../../code/console/index.md#materials_reload)* console command if you made some changes in shader files. It is really handy: you don't need to compile the shader every time you made any changes, you see the result of the changes in runtime without engine restart!


> **Notice:** If you made changes in the material `.mat` file, you should reload the engine.


### Can I debug the UUSL shader code?


Sure. If there is a shader error, the engine shows it in the [console](../../code/console/index.md):


[![](shader_error_sm.png)](shader_error.png)


The message contains information about which file has errors and their description (including the number of line).


[Export the shader file](../../code/uusl/types.md#shader_export) to the file and find this code line to figure out what's happen. Shader will be exported in a file with the graphic API shader format (`.hlsl`) located relatively to the `data` folder.


### How to create custom shader?


You can check the following articles:


- [Creating of Custom Shader for Post-Processing](../../code/uusl/create_post.md)
- [Abstract material � Mesh](../../code/materials_shaders/abstract_materials/mesh.md)
- [Abstract material � Decal](../../code/materials_shaders/abstract_materials/decal.md)

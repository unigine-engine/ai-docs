# Preserving Thin Details with Antialiasing


## Introduction


**[TAA (Temporal Antialiasing)](../../principles/render/antialiasing/taa.md)** is a widely adopted technique in 3D graphics for improving overall image quality by smoothing jagged edges and, in some cases, even boosting performance.


![](spp_original.png) ![](spp_taa.png)


However, while being a powerful tool for enhancing both static and dynamic images, TAA has a well-known **weak spot** - it often **fails to handle aliasing artifacts on thin geometry** like wires, road markings, lampposts, or other narrow objects, causing them to flicker, ghost, or disappear entirely.


These issues stem from core limitations of how TAA operates. By design, TAA blends data from previous and current frames to smooth out jagged edges - slightly shifting the camera (typically by half a pixel) each frame, accumulating results over time. This becomes critical for objects that are only a pixel wide, since if they become thinner than one pixel, they are simply no longer rendered. On the other hand, TAA may occasionally reveal lines that weren't previously visible, when a jittered sample happens to capture a subpixel detail - creating a ghosting or flickering effect.


| ![](thin_geometry_0.png) | ![](thin_geometry_1.png) |
|---|---|
| *Geometry Loss (TAA Sharp Mode)* | *Reconstructed Geometry (DLAA)* |


Disabling TAA might seem like a reasonable solution, but it actually results in even more line loss, especially for geometry farther from the camera - only nearby wires would remain consistently visible.


In essence, the core problem is a **lack of sufficient pixel coverage**. For traditional TAA-based pipelines, the most effective solution is to increase pixel density - either by rendering at higher resolutions or using supersampling techniques, which make thin lines thick enough to be consistently captured across frames. That said, simply using the TAA preset settings is unlikely to resolve the issue in a meaningful way. Instead, let's walk through a few practical ways you can use in UNIGINE to improve the visibility of fine details.


## TAA Settings Optimization


Most available presets are already tuned to provide the best balance of quality and performance, but for improved thin-line stability, we recommend switching to a custom TAA configuration. In *Settings -> Runtime -> Render -> Antialiasing*, select the *Custom* preset and tweak the parameters (such as the number of *Samples* or *Frame Count*) in the TAA section to achieve the best compromise between antialiasing quality and thin-object visibility.


![](taa_custom_parameters.png)


Additionally, enabling ***SRAA (Subpixel Reconstruction Antialiasing)*** and ***FXAA (Fast Approximate Antialiasing)*** can help mitigate some of the TAA-related artifacts by improving how subpixel details are handled.


Increasing the ***Supersampling*** parameter should also significantly improve the final image clarity. However, these improvements come at a cost and may introduce a noticeable GPU load - particularly on older or mid-range hardware. On GPUs like the **RTX 3060** or **3070**, or older, you might consider keeping this value at its default (1) to maintain a good balance between quality and performance.


![](taa_original.png) ![](taa_custom.png)


If TAA artifacts appear on thin geometry or other objects in motion - for example with **cameras locked onto a specific target** (*[Player Persecutor](../../objects/players/persecutor/index.md)*), try disabling the ***Antialiasing In Motion*** option. While it may not eliminate ghosting entirely, it can noticeably reduce the effect in many cases.


![](taa_persecutor_settings_big.png)

*Dynamic camera TAA recommended settings*


Another important factor influencing ghosting is the **frame rate**: lower FPS (e.g., around 30) will generally result in longer and more noticeable ghost trails.


## Geometry Inflation


> **Notice:** Out-of-the-box, this method is currently limited to materials inherited from the **[mesh_base](../../content/materials/library/mesh_base/index.md)** material.


As the root issue is that distant line geometry becomes thinner than a pixel, making it nearly invisible and easily discarded by TAA, one practical solution is to **inflate the geometry based on camera distance** - a method known as ***Geometry Inflation***. It helps preserve visibility even for very thin elements. In the case of 3D objects (e.g. lampposts, pipes, ropes, cables, antennas, etc.), the technique works by offsetting vertices along their normal vectors to make them appear slightly thicker as they move farther from the camera. To use *Geometry Inflation* in your scene, follow these steps:


- In the *Editor*, select the material assigned to the problem objects.
- In the *Parameters* tab, click *States*, and in the *Options* section select the ***Wire*** mode for distance-dependent *Geometry Inflation*. This makes the geometry expand more as distance increases while keeping it unaffected close to the camera. The ***Balloon*** mode inflates the geometry by a constant value, which is useful for mesh-based decals and Z-fighting surfaces.
- Control the intensity of the effect via the dedicated parameter ***Vertex Balloon*** slider in the *Material -> Parameters* tab. ![](geom_inflation_param.png)


Watch our [Geometry Inflation video tutorial](../../videotutorials/how_to/how_to_rendering/geometry_inflation.md) to see this technique in action.


![](taa_original.png) ![](taa_original_inflated.png)


### Graph-Based Material and Mesh Decal Antialiasing


#### Graph-Based Materials


If your objects affected by TAA use **[graph-based materials](../../content/materials/graph/index.md)** (i.e not inherited from **mesh_base**), you can still apply ***Geometry Inflation*** by using a dedicated **[custom subgraph](https://documentation-api.unigine.com/en/docs/future/content/thin_geometry/geometry_inflation.zip)**:


1. [Import](../../editor2/assets_workflow/assets_create_import.md#import) the custom subgraph - `*.msubgraph` - into your project.
2. Add the subgraph to the [material graph](../../content/materials/graph/index.md#graph_compose) assigned to the object that requires inflation by dragging it into the *[Material Editor](../../content/materials/graph/index.md)* window.
3. Connect the subgraph output to the ***Vertex Offset [Tangent Space](../../content/materials/graph/index.md#vertex_space)*** input of the *[Material](../../content/materials/graph/node_library/misc/material.md)* node.
4. Adjust the ***Inflation Start Distance*** (in meters), ***Inflation Scale*** and ***Maximum Inflation*** sliders in the material *Parameters* tab as needed.


[![](graph_mat_inflation_sm.png)](graph_mat_inflation.png)


#### Mesh Decals Antialiasing


Another common use case for ***Geometry Inflation*** is road markings. These are typically projected onto a surface as ***[Mesh Decals](../../objects/decals/mesh/index.md)***, which, by their nature, lack conventional normals. In this particular case, inflation must be applied **along the tangent or binormal direction**, rather than the normals.


![](../../objects/decals/mesh/index_sm.jpg)

 Best PracticeIf you are creating **road markings** (or similar elements), we recommend using ***Mesh Decals*** instead of **meshes**. This approach ensures that the decal naturally conforms to the underlying road surface, avoiding issues like geometry misalignment or z-fighting. Unlike regular *[decals](../../objects/decals/ortho/index.md)*, they don't rely on high-resolution textures to represent thin lines, which makes them a more practical solution.
That said, this approach requires **careful content preparation**. To define the inflation direction of a *Mesh Decal*, unwrap the mesh in a third-party application (such as Blender, Maya, or 3ds Max) with UVs encoding the desired axis - for example, a gradient in **UV.x** for road markings, since this axis will be used for inflation. This setup tells the shader in which direction to offset vertices. The gradient must span the full **[0,1]** range, as the shader internally remaps it to **[-1,1]**, shifting 0.5 to 0 so geometry inflates evenly in both directions. Proper UV setup is absolutely critical here - without it, *Geometry Inflation* may not function as intended - or not at all.


To implement this solution, use the dedicated **[custom subgraph](https://documentation-api.unigine.com/en/docs/future/content/thin_geometry/mesh_decal_inflation.zip)** explicitly designed for road markings:


1. [Import](../../editor2/assets_workflow/assets_create_import.md#import) the custom subgraph - `*.msubgraph` - into your project.
2. Add the subgraph to the [material graph](../../content/materials/graph/index.md#graph_compose) assigned to the object that requires inflation by dragging it into the *[Material Editor](../../content/materials/graph/index.md)* window.
3. Connect the subgraph output to the ***Vertex Offset [Tangent Space](../../content/materials/graph/index.md#vertex_space)*** input of the *[Material](../../content/materials/graph/node_library/misc/material.md)* node.
4. Adjust the *Geometry Inflation* parameters in the material *Parameters* tab.


[![](mdecal_subgraph_sm.png)](mdecal_subgraph.png)


#### Other Approaches for Mesh Decals


While *Geometry Inflation* works well in many cases, it's not the only viable method. For example, for *Mesh Decals* like **road markings**, there's an alternative solution that can help improve visual clarity. The pipeline for this method is as follows:


1. Create a mesh with the line width set to approximately **2x the original geometry**: ![](mesh_decal_mesh.png)
2. Create a **UV channel**: ![](mesh_decal_uv.png)
3. Apply a texture that includes an **alpha channel**: ![](mesh_decal_alpha.png)


By adjusting the UV coordinates, you can control the line width, while anisotropic filtering and mipmaps ensure optimal rendering quality at runtime.

 Best PracticeA similar method can be applied to **3D objects** like, for example, antennas. With this approach they're typically constructed as one or two crossed **planes with textures instead of actual geometry**. The alpha channel will blur at distance based on mipmaps within the mesh bounds, ensuring the object remains visible at longer ranges by maintaining sufficient screen pixel coverage and avoiding aggressive TAA filtering.
## Utilizing Upscaling Techniques


All the methods described above offer decent workarounds, but the real game-changer comes from modern upscaling technologies like ***DLSS*** and ***FSR***.


> **Notice:** The TAA effect is automatically disabled for the final image rendering when **DLSS** or **FSR** upscaling is applied.


### DLSS


**[Deep Learning Super Sampling (DLSS)](../../principles/render/upscaling/index.md#dlss_use)** is a real-time deep learning technology from NVIDIA that boosts performance and enhances image quality using AI. And if you're after maximum clarity, the standout here is ***DLAA (DLSS Antialiasing)*** - a variant of *DLSS* focused purely on image quality. Unlike regular *DLSS*, which upscales a lower-resolution frame, ***DLAA*** runs at native resolution and applies deep learning to reconstruct sharp, stable edges. The result is significantly reduced shimmer and much better handling of thin geometry.


> **Notice:** **DLAA** is only supported on **NVIDIA RTX-series GPUs**.


***DLAA*** differs from conventional methods like *MSAA, FXAA,* or *TAA* by going far beyond edge smoothing. It combines AI-powered deep learning with real-time rendering to not just smooth edges, but to intelligently recover subtle details that traditional techniques often miss.


![](taa_original.png) ![](dlaa.png)


> **Warning:** While **DLSS** can be exceptionally effective for static content, it may introduce ghosting artifacts on moving objects.


### FSR


**[AMD FidelityFX Super Resolution (FSR)](../../principles/render/upscaling/index.md#fsr2_use)** is an open-source, high-quality upscaling solution by AMD. It creates higher-resolution frames from lower-resolution inputs, using advanced edge detection to reconstruct fine features. While unlike *TAA*, it doesn't rely on motion vectors and frame history, or deep learning like *DLSS*, it still delivers noticeable improvements in image stability and thin-line visibility.


![](taa_original.png) ![](fsr.png)


> **Notice:** **DLSS** and **FSR** are fully supported on both Windows and Linux. UNIGINE provides support for **DLSS up to version 4** and **FSR up to version 3.1.3**.


## Rendering Text


Text rendering is another area where thin lines can introduce problems, especially when the text is small, distant, or viewed at sharp angles, like distant labels, signs, or road markings. If you're using the ***Text*** object (***[ObjectText](../../objects/objects/text/index.md)***) for in-world text, you might notice that the characters - due to how they are rendered - blur, flicker or even vanish as the camera moves.


For best results, avoid using ***ObjectText*** for permanent scene elements. Instead, bake the text into high-resolution textures and apply them to mesh surfaces.

   Sorry, your browser does not support embedded videos.
If you still prefer to use ***ObjectText*** in your project, try the following adjustments:


- Select *TAA [Custom](#taa_settings)* mode and disable the ***Fix Flicker*** parameter as it may cause small text to appear blurred.
- Tweak the ***[Mip Bias](#mip_bias)*** parameter to use a mip level with higher mip resolution.


![](with_fix.png) ![](without_fix.png)


## MIP Offset


In some cases, improving how thin lines appear is simply a matter of controlling which mipmap level is used during texture sampling. The ***Mip Bias*** (or Mip Offset) parameter of the texture lets you shift the mipmap level selected when sampling, giving finer control over texture sharpness at different distances, and reducing unwanted artifacts.


![](mip_bias_param.png)


For **graph-based materials** mip offset can be enabled by double-clicking the *[Sample Texture](../../content/materials/graph/node_library/textures/sample_texture.md)* node in the *[Material Editor](../../content/materials/graph/index.md)* and selecting the [**dedicated mode**](../../content/materials/graph/node_library/textures/sample_texture.md#sample_type) from the *Type* dropdown.


![](graph_mip.png)


While *Mip Bias* may not be the most reliable tool for recreating lost geometry, forcing higher-resolution mipmaps to be used farther from the camera can help preserve sharpness. However, keep in mind that if pushed too far, it may introduce **shimmering or flickering**, especially when the camera moves. This happens because higher-res mipmaps contain more detail than the screen can reliably display at a distance, leading to unstable pixel selection during rendering.


![](taa_original.png) ![](mip_bias.png)


## Content Adjustment


If the techniques above don't fully resolve the issue and the problem persists, here are a few additional strategies that can help:


- Use ***[LODs](../../principles/world_management/index.md#lods)*** to simplify or remove problematic geometry at a distance or based on the camera FOV.
- **Bake small geometry details into textures**where possible.
- **Adjust the material settings** of the affected object:

  - For instance, when viewed through transparent surfaces (such as car windows), thin geometry can appear blurred by TAA because the ***[Velocity Buffer](../../principles/render/sequence/index.md#velocity)*** isn't written for objects behind the transparency. To avoid this, disable velocity writing in *Parameters -> States* for the transparent object so motion behind it is captured correctly. ![](alpha_test_buffers.png)
  - Another example of material adjustment for fine details is enabling ***Write Opacity Depth*** on transparent materials assigned to objects like wires. With this option enabled, TAA has less impact on such elements, reducing visual distortions. ![](opacity_depth.png)


Ultimately, the best approach is to mix and match these strategies, tailoring them to your specific content and hardware to ensure both clarity of thin details and stable performance.

# Rendering Sequence


UNIGINE has a combination of a full deferred renderer with forward rendering techniques:


- All opaque (non-transparent) geometry is rendered in the deferred pass.
- Transparent geometry is rendered in the forward pass.


Before the deferred rendering pass, the engine performs all necessary calculations. It specifies what nodes should be rendered, the order of rendering, how many lights there are in the scene, and so on.


This article introduces the detailed UNIGINE rendering pipeline including all auxiliary stages, which can be skipped by the user.


## Rendering Pipeline Overview


A frame is a complex structure including a lot of different calculations and textures rendering.


Here is the rendering pipeline, all stages are performed during one frame composition. Some stages can be switched off, if necessary: decals rendering stage, auxiliary pass, post-materials, etc.


During rendering, the engine initializes necessary texture buffers and most of them are not cleared completely (the engine cuts out sky areas). Some passes just re-use these already created buffers. Such optimizations help to increase the rendering performance.


The schematic representation of the rendering pipeline displays the main stages of the rendering sequence.


[![](rendering_sequence_sm.png)](rendering_sequence.png)

*Schematic representation of the rendering pipeline*


The frame rendering process will be illustrated by screenshots from a simple test scene with a variety of materials (transparent and opaque), environment probes, decals, planar reflections, different light sources.


## Common Pass


The Common pass is the very first step of the rendering sequence. In this pass, [environment LUTs](../../../editor2/settings/render_settings/environment/index.md#lut_settings) and the [Environment cubemap](../../../editor2/settings/render_settings/environment/index.md#environment_settings) are rendered. These textures are rendered only once before all the geometry in the scene and will be used further for the final screen composition: for scattering rendering and [non-dynamic reflections](#deferred_reflection).


| [![](environment_cubemap_sm.png)](environment_cubemap.png) | Environment cubemap is composed of six pieces (256x256 px each). |
|---|---|
| ![](luts.png) | LUT textures are represented as 1x256 px textures taken from the current state of the loaded [LUT textures for scattering](../../../editor2/settings/render_settings/environment/index.md#lut_settings). |


## Calculations


During this step, nothing is rendered at all. This stage prepares the scene before geometry rendering: the engine analyzes the visible part of the scene to know which objects should be drawn and which shouldn't. The engine does the following:


- Checks intersections of objects with the frustum (frustum culling) and finds the objects that are present in the frame.
- Finds all light sources in the scene.
- Finds all surfaces that should be rendered (taking into account *[Occluder](../../../objects/worlds/world_occluders/index.md)* objects).
- Sorts Lights and *Environment Probe* by size (from large to small).
- Sorts Decal objects by their rendering order.
- Sets the [Occlusion Query](#occlusion_query) flags to objects that shouldn't be rendered.
- Surfaces Batching. All opaque surfaces are grouped and rendered in batches according to materials assigned, thus decreasing the number of DIP calls and, therefore, increasing the performance.


Occlusion Query works with a delay: it is a very performance-hit operation that requires much time. The optimization is the following: the engine checks the scene asynchronously and sets the "should not be rendered" flag during the [Occlusion Query](#occlusion_query) stage. That's why occlusion query runs at least 1 frame late. But the object will be hidden without "hard switching" when the FPS value is high.


## Shadow Maps


After calculations, shadow maps are rendered. The way of rendering these maps depends on the type of a light source. Generated shadow maps are used in the following rendering stages.


### World Light


For the [world lights](../../../objects/lights/world/index.md), the engine creates [cascaded shadow maps](https://msdn.microsoft.com/en-us/library/windows/desktop/ee416307(v=vs.85).aspx). World Light's shadow map is rendered into the orthographic projection.


The shadow map of the world light source is rendered into texture divided into four parts (since the 4 is the maximum quantity of shadow cascades).


| [![](world_shadow_map_sm.jpg)](world_shadow_map.jpg) | Shadow map of the *Light World* source |
|---|---|


Shadows near the camera have higher resolutions, while shadows that are far away from the camera have fewer details.


| [![](cascades_rectangular_sm.jpg)](cascades_rectangular.jpg) | Rectangular shadow cascades on the final scene |
|---|---|


> **Notice:** You can specify the number of cascades of the *Light World* source in the *[Parameters](../../../editor2/node_parameters/index.md)* window.


### Omni Light


*[Light Omni](../../../objects/lights/omni/index.md)* sources use perspective projection for shadow maps. Each of these light sources uses 6 cameras that generate shadow maps.


Keep in mind that using a lot of *Light Omni* nodes can sufficiently decrease the performance.


### Proj Light


Shadow maps for *[Light Proj](../../../objects/lights/proj/index.md)* sources are rendered only once because only 1 camera is used.


> **Notice:** It is better to use *Light Proj* instead of *Light Omni* for better performance.


## Dynamic Reflections


During this stage, the engine renders necessary textures for **dynamic reflections** (i.e. changed each frame): cubemaps for [environment probes](../../../objects/lights/envprobe/index.md) and 2D textures for [planar reflections](../../../objects/lights/planar/index.md). To render these textures, the engine goes through all rendering pipeline (but misses some passes described below).


Cubemaps are generated by using 6 cameras, planar reflections use only 1 camera. Both render the final image (one more rendering cycle) with some hooks:


- Textures use shadow maps that were already generated in the previous [shadow maps rendering](#shadow_maps) pass.
- All post effects are ignored.
- Final image for dynamic reflections is rendered missing *[TAA](../../../principles/render/antialiasing/taa.md)*.


| [![](reflections_dynamic_sm.jpg)](reflections_dynamic_sm.jpg) | The final texture of dynamic reflections |
|---|---|


## Deferred Pass for Opaque Objects


This pass is one of the key passes of rendering: all opaque geometry is rendered during this pass one by one.


In the end of this pass, the engine has the texture (color texture) with all opaque geometry and scattering.


### Native Depth Pre-Pass


In this pre-pass, the GPU performs a depth-test for surface culling. The pre-pass is performed only for alpha test and complex materials(for example, with a lot of layers).


The depth buffer stores native depth values **z/w**.


| [![](depth_sm.jpg)](depth_sm.jpg) | The depth data stored in a depth buffer texture format **D32F** |
|---|---|


During this pass, the GPU can discard a pixel (shading for this pixel won't be calculated).


### Filling the GBuffer


During this step of rendering, the engine fills the *Gbuffer* (Geometry buffer) for shading.


#### Depth


The depth buffer contains scene objects in the current field of view (found between the near and far clipping planes). Objects are rendered as pure geometric models and stored into this buffer.


The engine also uses native depth.


| [![](depth_sm.jpg)](depth_sm.jpg) | The depth data stored in a depth buffer texture format **D32F** |
|---|---|


#### Albedo


The albedo colors buffer stores pure albedo colors of all material textures:


| [![](albedo_sm.jpg)](albedo_sm.jpg) | The texture format is ***RGBA8** (RT0)*: - **RGB** channels store albedo color values - **A** channel stores the occlusion value. This channel is optional |
|---|---|


#### Shading


The shading buffer stores shading information on objects in the scene.


| [![](shading_sm.jpg)](shading_sm.jpg) | The texture format is ***RGBA8** (RT1)*: - **R** channel stores the metalness value - **G** channel stores the f0 (specular) value - **B** channel stores the translucent value - **A** channel stores the microfiber value |
|---|---|


Translucency is used to simulate light shine through objects (leaves, for example).


#### Normal


The normal buffer stores normal vectors for each vertex of geometry which are required for calculation of the proper lighting.


| [![](normal_sm.jpg)](normal_sm.jpg) | The texture format is ***RGBA8** (RT2)*: - **RGB** channels store compressed normal values (in view space) - **A** channel stores the roughness value |
|---|---|


#### Velocity


The velocity buffer stores information about the displacement of pixels per frame. When the image is still, the buffer is filled with zero (black) values. These values are necessary to make the [temporal anti-aliasing (*TAA*)](../../../principles/render/antialiasing/taa.md) and motion blur work correctly.


| [![](d_velocity_sm.jpg)](d_velocity.jpg) | The texture format is ***RG16F** (RT3)*: - **RG** channels store pixel displacement values (XY coordinates) |
|---|---|


You can disable the buffer, if you don't need velocity-related effects: motion blur, *TAA*, etc.


#### Material Mask


The material mask texture. The first 8 bits are reserved for post effects, other bits can be used for materials.


| [![](d_decal_mask_sm.jpg)](d_decal_mask.jpg) | The texture format is ***R32U** (RT4)*: - **R** channel stores the material mask value |
|---|---|


#### Lightmap


The lightmap buffer is used to add baked light to the scene.


| The texture format is ***RG11B10F** (RT5)*: - **RGB** channels store lightmap values |
|---|


### Occlusion Query


During the **Occlusion query** step, the engine excludes objects (geometry, lights, and decals) that have the *[Culled by occlusion query](../../../editor2/node_parameters/transformation_common/index.md#query)* flag enabled, from the rendering sequence.


> **Notice:** If the `render_occlusion_queries` console command value is set to 2, the flag is not taken into account and all objects are excluded from the rendering sequence.


Occlusion query is an operation with a lot of calculations (i.e. significantly affects performance) and is executed asynchronously. The engine checks object bounds and sets the flag to the renderer, if necessary. In the next frame, during the **[Calculation](#calculations)** stage, the renderer excludes the object from the rendering sequence.


> **Notice:** Occlusion Query doesn't work, when the camera is inside the object.


### Decals


During this step of the deferred pass for opaque objects, the engine renders [decals](../../../objects/decals/index.md). Decals have been already sorted on the [Calculations](#calculations) stage, and during this stage, the engine performs rendering by using this order.


Decals are rendered by using [alpha blending](../../../principles/render/blending/index.md), but since **A** channels of the normal and shading textures are occupied by microfiber and roughness values, the engine copies necessary values into new textures and performs alpha blending.


| [![](decals_normal_sm.jpg)](decals_normal_sm.jpg) | New **Normal** texture (uncompressed) that is used for alpha blending |
|---|---|
| [![](decals_roughness_sm.jpg)](decals_roughness_sm.jpg) | New **Roughness** texture to store *Roughness* value in **R** channel, and *Microfiber* value in **G** channel |


> **Notice:** If the value of `render_decals` console variable is set to 0, the engine will skip this rendering stage.


### Shoreline Wetness


This rendering stage is responsible for shoreline wetness effect of the *[Global Water](../../../objects/objects/water/water_object.md)* object. The behavior of this step is like in the previous [Decals rendering](#decals) step. So we can call this step Post-Decal Rendering.


The effect is performed by using [Compute Shaders](../../../code/uusl/compute.md) and Unordered Access Textures techniques.


### Linear Depth, Color Old Reprojection and Unpacked Normals


To perform screen-space effects, the engine renders *Linear Depth, Color Old Reprojection* (previous frame), and *Normal Unpack (screen-space normals)* textures.


These textures are used in subsequent *[Screen-Space Reflections](#ssr)* and *[Screen-Space Global Illumination](#ssgi)* stages.


The linear depth texture is generated by using [G-buffer depth](#depth). Mips of *Linear Depth, Color Old*, and *Normal Unpack* textures are also created.


### SSRTGI


During this stage, **Screen-Space Ray-Traced Global Illumination** post-effect is rendered, during which the engine fills the following textures:


- **[SSAO](#ssao)**, if the value of `render_ssao` console variable is set to 1, defining whether SSAO and SSAO Ray Tracing should be performed.
- **[SSGI](#ssgi)**, if the value of `render_ssgi` console variable is set to 1, defining whether SSGI should be performed.
- **Bent Normal**, if the value of `render_bent_normal` console variable is set to 1, defining whether Bent Normal should be performed.


*Bent Normal* is rendered in the **RGBA8** texture.


*Bent Normal* also may have own *[TAA](../../../principles/render/antialiasing/taa.md)* depending on:


- If noise is enabled and *SSRTGI* is rendered in **full resolution**, *TAA* is not applied during this stage.
- If noise is enabled and *SSRTGI* is rendered in **half resolution** or **quarter resolution**, *TAA* is applied.


| [![](ssrtgi_sm.jpg)](ssrtgi.jpg) | New **Ray-Traced SSAO** texture |
|---|---|
| [![](bent_normal_sm.jpg)](bent_normal.jpg) | New **Bent Normal** texture |


> **Notice:** If the value of the `render_ssrtgi_preset` console variable is set to 0, the engine will skip this rendering stage.


### Deferred Light Pass


In the deferred light pass, the engine creates a buffer (Deferred Light Map), which is a 2D array of **RG11B10F** textures. The first layer of the array is for **diffuse** light, the second is for **specular** (which can be switched off for VR).


Light sources use already generated [shadow maps](#shadow_maps).


All lights sources are rendered one by one in a single 2D array to be applied during the [Deferred Composite](#deferred_composite).


> **Notice:** For optimization reasons, **one world light** source is always calculated during the [Deferred Composite](#deferred_composite) step.
>
>
> If you have two or more world light sources, **one world light** source is always rendered during the deferred composite, and other light sources are rendered during this step.


| [![](lights_diffuse_sm.jpg)](lights_diffuse_sm.jpg) | **Light sources diffuse** layer |
|---|---|
| [![](lights_specular_sm.jpg)](lights_specular_sm.jpg) | **Light sources specular** layer |


The engine uses tile rendering technique for *Light Omni* sources without shadows. With this optimization, *Light Omni* sources are grouped and rendered in batches, decreasing the number of *DIP* calls and, therefore, improving the performance.


### Deferred Reflections


During this stage of rendering, the engine renders all *[Environment Probes](../../../objects/lights/envprobe/index.md)* that have been already sorted on the [**calculations**](#calculations) stage.


*Environment Probes* are rendered into the 2D array of **RGBA16F** textures: the first layer contains reflections, the second layer contains ambient light.


The renderer doesn't clear the deferred reflection textures if at least one environment probe has infinite size.


> **Notice:** If there is no [environment](../../../editor2/settings/render_settings/environment/index.md#environment_settings), the **RG11B10F** 2D array is used.


| [![](probe_reflection_sm.jpg)](probe_reflection_sm.jpg) | Reflection texture of **Environment Probe** |
|---|---|
| [![](probe_ambient_sm.jpg)](probe_ambient_sm.jpg) | Ambient texture of **Environment Probe** |


### Reflection Pass


In the reflection pass, planar dynamic reflections (that [have already been rendered](#dynamic_reflections)) are applied. Dynamic reflections are rendered in the same texture that was used for [Deferred Reflections](#deferred_reflection).


| [![](reflection_pass_sm.jpg)](reflection_pass_sm.jpg) | **Planar dynamic** reflection is applied |
|---|---|


### Auxiliary Pass


The auxiliary pass is a type of custom pass. Materials with the *Auxiliary pass* enabled are rendered in the auxiliary **RGBA8** texture.


The auxiliary texture is often used for different post effects. This texture has its own *[TAA](#taa)* stage.


> **Notice:** The engine skips this pass if there are no materials with the enabled *Auxiliary pass* and during the [Dynamic Reflections](#dynamic_reflections) pass.


| [![](auxiliary_sm.jpg)](auxiliary_sm.jpg) | **Auxiliary** buffer texture |
|---|---|


### Refractions


During this stage of the pipeline, refractions are rendered. They are rendered in the refraction texture and applied during the [transparent object](#refraction_apply) stage.


Refraction is the **RGBA8** texture. The texture contains distortion values.


> **Notice:** This pass is skipped during the [Dynamic Reflections](#dynamic_reflections) pass.


| [![](refractions_sm.jpg)](refractions_sm.jpg) | **Refractions** buffer texture |
|---|---|


### Transparent Blur Surfaces


During this stage, the transparent surfaces used in the *[Transparent Blur](../../../content/materials/library/mesh_base/index.md#option_transparent_blur)* effect are rendered. They are rendered in the transparent blur texture and applied during the [post effects](#transparent_blur_apply) stage.


*Transparent Blur* is the **R16F** texture that contains blurriness values.


> **Notice:** This pass is skipped during the [Dynamic Reflections](#dynamic_reflections) pass.


| [![](transparent_blur_sm.jpg)](transparent_blur_sm.jpg) | **Transparent Blur** buffer texture |
|---|---|


### SSR


Screen-Space Reflections are rendered in **RGBA16F** textures. They are applied to the deferred composite stage.


| [![](ssr_sm.jpg)](ssr_sm.jpg) | **SSR** buffer texture |
|---|---|


There are two different types of *SSR* � with importance sampling and without it:


#### Importance Sampling is On


If the importance sampling is enabled, the renderer doesn't use linear depth texture.


In this case, the *SSR* color texture and *SSR* velocity texture are rendered. Velocity is used for avoiding artifacts whilst the camera or objects are moving.


*SSR* has its own *[TAA](#taa)* stage.


#### Importance Sampling is Off


In this case, three textures are rendered: *SSR* velocity, *SSR* color texture, and ray-length texture. After that, the renderer applies *[TAA](../../../principles/render/antialiasing/taa.md)* for the *SSR*.


The three textures mentioned above are used to perform blurring to provide realistic reflection behavior.


### SSAO


Screen-Space Ambient Occlusion is rendered in its own **R8** texture. It is applied in the deferred composite stage.


*SSAO* can be rendered with or without noise. This option has influence on *[TAA](../../../principles/render/antialiasing/taa.md)*:


- If noise is enabled and *SSAO* is rendered in **full resolution**, there is no *TAA* during this stage.
- If noise is enabled and *SSAO* is rendered in **half resolution**, this stage has its own *TAA*.


| [![](ssao_sm.jpg)](ssao_sm.jpg) | **SSAO** texture |
|---|---|


> **Notice:** If the value of the `render_ssrtgi_preset` console variable is set to 1 and the **SSAO** texture has been already filled during the [*SSRTGI* stage](#ssrtgi), the engine skips this step.


### SSGI


Screen-Space Global Illumination is rendered in one **RG11B10F** texture.


*SSGI* stage also has its own *[TAA](#taa)*.


> **Notice:** If the value of `render_ssrtgi_preset` console variable is set to 1 and the **SSGI** texture has been already filled during the [*SSRTGI* stage](#ssrtgi), the engine skips this step.


### Underwater Fog


During this step, the [Underwater Fog texture](#wbuffer_underwater_fog) is initialized and cleared by the renderer to perform the underwater world lighting correctly.


### Deferred Composite


During this stage, the engine uses all necessary textures from the previous stages and passes to create the final texture with opaque geometry. The engine combines buffers and calculates shading for the final texture of this pass.


During this stage, the renderer calculates the light of one world light and applies it. Environment reflections, ambient, and haze (scattering) are also rendered here.


| [![](deferred_composite_sm.jpg)](deferred_composite_sm.jpg) | **The final image** of the deferred pass for opaque geometry (excluding the Emission pass and *SSS*) |
|---|---|


> **Notice:** The final deferred composite texture can be **RGBA16F** or **RG11B10F**, depending on the corresponding option enabled.


### Emission


The emission pass follows creation of the deferred composite image and applies the emission effect over this image.


| [![](emission_sm.jpg)](emission_sm.jpg) | **Emission** applied |
|---|---|


### SSS


Subsurface Scattering changes the final deferred texture by applying the exponential blur.


| [![](emission_sm.jpg)](sss_sm.jpg) | **SSS** applied |
|---|---|


## Transparent Objects Rendering


Almost all transparent objects are rendered in the forward rendering pass.


During the forward pass, the renderer fills deferred buffers to let forward transparent objects participate in post-effects.


### Refraction


During this stage of the rendering sequence, the refraction texture (which has been [already rendered](#refraction)) is applied.


| [![](refractions_applied_sm.jpg)](refractions_applied_sm.jpg) | **Refraction** applied |
|---|---|


### Volumetric Clouds


During this step, all [layers](../../../objects/objects/cloud_layer/index.md) of procedural Volumetric Clouds are rendered into the **RGBA16F** texture using parameters of the **[clouds_base](../../../content/materials/library/clouds_base/index.md)** material.


| [![](clouds.png)](clouds.png) | Example of the **Clouds** texture content |
|---|---|


Due to optimization, Volumetric Clouds are rendered in a certain order depending on the following conditions:


- **Before Water and Transparent Objects** � if the value of the `render_clouds_transparent_order` console command is set to 0, and the current camera is below the water highest point or under the surface.
- **Between Water and Transparent Objects** � if the value of the `render_clouds_transparent_order` console command is set to 0 and the current camera is above the water highest point.
- **After Water and Transparent Objects** � if the value of the `render_clouds_transparent_order` console command is set to 1.


### Water


Water rendering in UNIGINE is really complex: it has its own deferred buffer (called *WBuffer*) with light and environment probes passes.


#### FieldHeight and FieldShoreline


First, the *Field Height* and *Field Shoreline* textures are rendered.


##### Height


The *Field Height* textures are rendered in a 2D array of **R16F** or **R32F** textures (depending on settings). All *Field Height* textures are packed into a 2D array to pass the data to the shader.


> **Notice:** You can specify the texture format in the array by using the `render_field_precision` console command.


##### Shoreline


All *Field Shoreline* textures are also are packed into a 2D array (of **RGBA8**) to pass the data to the shader.


#### WBuffer


The renderer initializes *WBuffer*.


> **Notice:** The [Underwater Fog texture](#underwater_fog) has been already initialized.


##### Diffuse


The diffuse color of water is black, and diffuse texture is necessary for decals that will be displayed over the water surface.


| The texture format is **RGBA8**: - **RGB** channels store decal diffuse values - **A** channel stores foam values |
|---|


##### Normal


The Normal texture stores normals for lighting, and alpha channel stores mesh transparency values (it can be used for soft intersections with water geometry).


| The texture format is **RGBA8**: - **RGB** channels store compressed normal values - **A** channel stores water fade values |
|---|


##### Water


The Water texture is used to create the procedural foam mask. The mask shows where foam will be depicted.


| The texture format is **RG8**: - **R** channel stores procedural foam mask - **G** channel stores caustics values |
|---|


##### Constants


We use a Deferred Constant Transferring approach for water meshes. **R** channel of this texture stores the ID value of the water mesh, which is used to load corresponding textures and parameters for the mesh.


| The texture format is **R32U**: - **R** channel stores constant id value for the water mesh |
|---|


##### Underwater Mask


The Underwater mask is used only for Global Water, since the water mesh doesn't have an underwater mode.


| The texture format is **RGB8**: - **R** channel stores underwater mask (where the underwater should be rendered and where it shouldn't) - **G** channel stores height distance (distance from the separating waterline) - **B** channel stores shaft samples value (location of sun shafts) |
|---|


##### Underwater Fog


| The texture format is **RGBA16**: - **RGB** channels store bottom coloring values - **A** channel stores fog exponent values (transparency of the fog) |
|---|


#### Copy Opacity Screen


During this step, the renderer copies the opacity screen that has been rendered before, into a new texture.


#### Clear Buffers Textures


During this stage, the renderer clears buffer textures to prepare for water rendering. It clears [reflection texture](#deferred_reflection) (both specular and diffuse), [Water buffer texture](#wbuffer_water), and, if there is the water mesh in the scene, [Constants](#wbuffer_constant) and [Underwater Fog](#wbuffer_underwater_fog) textures.


#### Select the Water Mode


The renderer checks the camera position to know what part of water should be rendered. There are three modes:


- `UNDERWATER`. Only underwater is rendered.
- `OVERWATER`. Only the upper surface of the water is rendered.
- `BOTH`. Both underwater and overwater is rendered including the separating waterline.


#### Filling the WBuffer


During this step, the *[WBuffer](#wbuffer)* textures are filled with the corresponding data.


In case of the [water mesh](../../../objects/objects/water/water_mesh.md), WBuffer is rendered like *[GBuffer](#gbuffer)* because it doesn't have an underwater mode.


Global water is rendered differently: most buffers are rendered as deferred buffers but *caustics* of [water](#wbuffer_water), [fog](#wbuffer_underwater_fog), and [underwater mask](#wbuffer_underwater_mask) are rendered as post effects.


#### Water Decals


During this stage, water decals are rendered. Decals are rendered (normal and diffuse) by using alpha-blending.


#### Water Lights and Environment Probes


After decals, [Deferred Light Map](#lights) and [Environment Probes textures](#deferred_reflection) are rendered.


#### Underwater Shafts


During this stage, underwater shafts are rendered by using [underwater mask](#wbuffer_underwater_mask) shaft samples values (stored in **B** channel). They are rendered only if the camera has `UNDERWATER` mode or `BOTH`.


#### Water Composite


After all water stages, the renderer writes **two** composite textures for the water pass:


- For underwater
- For above-water


Then the waterline (a black separating line) is rendered.


#### Water DOF


After the composite texture is rendered, the depth-of-field effect for water is rendered. It performs blurring over the whole texture.


If Global *DOF* is enabled, it uses depth of water (water is rendered to the depth texture which already contains rendered opaque objects) to perform *DOF* blurring correctly.


### Sorting Transparent Objects


Transparent objects are sorted from the farthest to the nearest and are rendered one by one.


### Transparent Objects Rendering


Transparent objects rendering has two modes: **Multiple Environment Probes** enabled/disabled, depending on the value of the *[Multiple Environment Probes](../../../content/materials/library/mesh_base/index.md#multiple_env_probes)* parameter of the mesh_base material.


#### Multiple Environment Probes Enabled


First, the Depth Buffer is rendered and the *Environment Probe* texture is cleaned.


> **Notice:** If the `render_transparent_multiple_env_probes` console command is set to 0, the engine skips this stage for all surfaces having assigned the transparent material with the **Material Environment Probes** parameter enabled, so they are not rendered.


##### Environment Probe Rendering


During this stage, environment probe ambient and reflection are rendered into Environment Probes texture.


##### Ambient Pass


By using the Environment Probe texture, the renderer lerps sky ambient and reflection with the Environment Probe texture.


> **Notice:** In the Ambient pass **one World Light** is always rendered.


##### Light Passes


The renderer adds all the lights to the texture.


#### Multiple Environment Probes Disabled


##### Ambient Pass


During the ambient pass, the environment, lightmaps, and emission for transparent objects are calculated.


> **Notice:** In the Ambient pass, **one *World Light*** and **one *Environment Probe*** (if a transparent object is affected by either of them) are always rendered. If there are no environment probes, the sky will be rendered.


##### Light Passes


During the Light passes for transparent objects, the light is calculated. Renderer goes only through the passes that are specified in the material states.


Ultimately, all lights for transparent objects are added one by one.


| [![](transparent_sm.jpg)](transparent_sm.jpg) | After the **transparent objects** rendering |
|---|---|


### Filling Deferred Buffers


Transparent objects also write information into deferred buffers to let them participate into post-effects.


The following buffers are modified during this stage:


- Albedo
- Normal
- Shading
- Opacity Depth
- Material Mask


## Color Texture Copy


Current screen (color) texture is copied during this stage. The texture is used for *[TAA](../../../principles/render/antialiasing/taa.md)* and for *[SSR](#ssr)* and *[SSGI](#ssgi)* screen-space effects.


## SRGB Correction and Static Exposure


In this pass, the engine performs *SRGB* correction and static exposure (if enabled). If static exposure is off, the engine goes to the [Adaptive Exposure](#adaptive_exposure) stage.


SRGB Correction is applied before applying Anti-Aliasing (TAA), as it improves TAA efficiency, while gamma-compression makes it possible to improve accuracy for subsequent passes especially for low-bitness buffers.


| [![](srgb_correction_sm.jpg)](srgb_correction_sm.jpg) | After the ***SRGB* correction** |
|---|---|


## Adaptive Exposure


During this step, the engine renders luminance texture and applies it to the screen by using the corresponding exposure: logarithmic or quadratic.


| [![](adaptive_exposure_sm.jpg)](adaptive_exposure_sm.jpg) | After the **Adaptive Exposure** |
|---|---|


## Temporal Anti-Aliasing (TAA)


This pass is used when *[TAA](../../../principles/render/antialiasing/taa.md)* is enabled. Otherwise, the engine skips this pass and goes to the next one.


| [![](taa_sm.jpg)](taa_sm.jpg) | After the **TAA** |
|---|---|


*TAA* uses previous frames to improve the current frame by using linear interpolation.


![](taa_dif.jpg)


## Transparent Blur


During this stage, blurriness behind transparent objects is applied. The renderer uses the texture from the [Transparent Blur Surfaces](#transparent_blur) stage.


| [![](transparent_blur_apply_sm.jpg)](transparent_blur_apply_sm.jpg) | The frame with the **Transparent Blurriness** applied |
|---|---|


## Render Post Materials


In this pass, the engine generates procedural textures for Render Post Materials that should be affected by the Camera Effects.


## Camera Effects


Almost all camera effects are rendered in their own textures to be used in the [final screen composition](#composite) stage to create the final image.


### Motion Blur


**Motion blur** uses Velocity buffer for texture blurring. It doesn't have its own buffer and changes the screen.


### Depth of Field (DOF)


For the **Depth of Field** effect, the engine generates a *DOF* **RG8** mask.


- **R** channel stores the farthest blurring values (that are behind in-focus objects).
- **G** channel stores the nearest blurring values (that are in front of in-focus objects).


*DOF* works with the **RG11B10F** texture for better performance, therefore, if the screen texture has **RGB16F**, it would be converted into **RG11B10F** during this step. Additionally, the renderer performs some accuracy operations to improve the texture within the boundary areas of objects that are in focus.


Chromatic aberrations are also rendered here.


### Bright Texture


The renderer generates a new texture, pixels of which are brighter than the specified [threshold](../../../editor2/settings/render_settings/camera_effects/index.md#glare_effects). This texture determines the areas that will be illuminated with other camera effects mentioned below:


- Bloom
- Cross
- Lens


### Bloom


If bloom is enabled, the engine generates up to 8 bloom textures: each texture has a lower resolution (original size, original size /2, original size /4, and so on) with the bloom effect. After being generated, all bloom textures with different resolutions compose the final bloom texture.


The Cross and Lens textures use a bloom texture (not the final one) which has 1/4 screen resolution even if bloom is not rendered.


### Cross


The Cross texture uses the **original size /4** bloom texture to create the cross-camera effect even if bloom is disabled.


### Lens


The Lens texture also uses the **original size /4** bloom texture to create the bloom effect even if bloom is disabled. Dirt on the lens is also applied here.


### Shadow Shafts


During this step, the engine renders the texture with shadow shafts. This texture is used during the [Final Screen Composition](#composite) stage.


Shadow shafts have their own mask (which specifies where shadow shafts should be applied) and *[TAA](#taa)* for this mask.


## Final Screen Composition


During this stage, the engine assembles the final texture by using all textures that were rendered during the previous steps. Filmic tone mapping, dithering, and the *LUT* texture are applied here during the final screen composition.


| [![](composite_sm.jpg)](composite_sm.jpg) | **Final screen** composition |
|---|---|


## Post Materials


After the final screen composition, all post effects are applied.


If a procedural texture is necessary for a post material, it is calculated during this step and then the post effect is applied to the final composed screen.


## Post Engine Materials


### Border


With this engine post effect, the engine cuts out the edges of the screen that are outside the main window.


### FXAA


If *FXAA* is enabled, the engine doesn't perform the *[TAA](#taa)* pass and performs anti-aliasing here by using *FXAA* algorithm.


### Sharpen


If the Sharpen effect is enabled, the engine applies it to the final screen during this step.


## Post Debug Materials


During this step, [Debug Materials](../../../content/materials/library/debug/index.md) are applied to the composed image.


## Transparent Overlap


During this step, transparent surfaces with enabled **Overlapping** are rendered. This is the very last rendering stage for surfaces that allows creating nodes that are not affected by post effects, such as tooltips.


> **Notice:** **[TAA](../../../principles/render/antialiasing/taa.md)** is not applied during this stage.


## Visualizer


During this stage, the engine [visualizer](../../../api/library/engine/class.visualizer_cpp.md) is rendered: mesh wireframes, bounding boxes, nodes culled with occlusion query, etc.


## Fade Material


Fade material is used to create smooth screen blacking. It is usually used for beginnings and endings of tracks for *[Tracker](../../../editor2/tools/tracker/index.md)*.


## GUI


GUI is rendered last after all stages and passes are rendered.


| [![](gui_sm.jpg)](gui_sm.jpg) | After **GUI** rendering |
|---|---|


Finally, the engine has rendered a single frame!

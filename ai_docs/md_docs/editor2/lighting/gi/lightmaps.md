# Lightmapping


Lightmapping is a static global illumination technique using precalculated textures that store brightness and reflected color of lit surfaces. By using lightmapping you can avoid heavy computations of lighting in primarily static scenes.


[![](lightmapping_sm.jpg)](lightmapping.jpg)


Lightmapping is the most efficient solution enabling to achieve realistic diffuse lighting and keep the high performance. It is capable of giving high-detailed global illumination combined with simulation of many light bounces. The number of bounces is the key aspect of creating realistic lighting in bright scenes. When you use lightmapping it doesn�t matter how many rays, bounces, or light sources are there, as everything is calculated once and then baked in textures.


UNIGINE provides an integrated GPU-accelerated Lightmapper tool available in the *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md)* window.


Current limitations:


- Lightmapping is available only for surfaces of *[Static Mesh](../../../objects/objects/mesh/index.md)* objects.
- Only Non-Directional lightmaps are supported at the moment (normal maps are not taken into account).
- Only global illumination is baked, direct lighting is to be provided by light sources.


> **Notice:** Lightmapping eliminates rendering of surfaces in batches, thus increasing the number of DIP calls.


### See Also


- Quick video guide: [How To Bake Global Illumination to Lightmaps](../../../videotutorials/how_to/how_to_rendering/lightmaps.md).
- Quick video guide: [How To Reuse Lightmaps for Levels of Detail](../../../videotutorials/how_to/how_to_rendering/lightmap_lods.md).
- Quick video guide: [How To Tweak Baked Lighting Dynamically via the Lightmap Color](../../../videotutorials/how_to/how_to_rendering/lightmap_color.md).
- Lightmaps baking is also available via code by using the *[BakeLighting](../../../api/library/lights/class.bakelighting_cpp.md)* Class.


## Preparing The Content


Proper and non-overlapping UV-coordinates of scenery are required for correct lightmapping. In the case your assets do not have these, automatic UV unwrapping on import is provided. The overall workflow is the following:


1. In the [Import Settings](../../../editor2/fbx/index.md#import_fbx) for FBX, CAD models and UNIGINE `.mesh` assets, select the **UV Channel** and **Target Resolution** to be used for lightmaps and, if needed, check UV channels to unwrap. Traditionally, the **0** UV channel is used for texturing and the **1** channel is for lightmapping. The **Lightmap Target Resolution** parameter has the direct influence on the baking time and the final quality. ![](import_unwrap_uv.png) > **Notice:** Unwrapping thin polygon meshes intended to be used with double-sided materials applied, such as pieces of paper, banners or fabrics, may lead to visual artifacts when lightmapping. It is recommended to consider re-modeling such meshes by adding polygons for the other side of the model.
2. For all surfaces intended to be lightmapped, the [Lightmaps Parameters](../../../editor2/node_parameters/visual_representation/index.md#surface_lightmaps) are needed to be adjusted: ![](../../node_parameters/visual_representation/surface_lightmaps.png)

  1. Select the [**Static Lighting Mode**](../../../editor2/lighting/gi/index.md#lighting_modes) for the surfaces (or the *Advanced* lighting mode).
  2. Check **Enabled** to enable the feature.
  3. Select the **Bake Unique Texture**, if you intend to use the [integrated lightmapper](#bake).
  4. Also, you can specify the lightmap **Texture** generated in a third-party software. Select the **Use Custom Texture** mode for this purpose.
3. For a surface to contribute to static GI, it must have the [*Lighting Mode*](../../../editor2/lighting/gi/index.md#lighting_modes) set to **Static** or have the [**Cast Global Illumination**](../../../editor2/node_parameters/visual_representation/index.md#cast_gi) option enabled in the *Advanced Lighting Mode*. ![](lighting_mode_static.png) ![](cast_gi.png) For selective group-based shading when baking lightmaps, adjust the *[Viewport Masks](../../../principles/bit_masking/index.md#viewport)*. A surface will be visible for the lightmapper only if its *Viewport Mask* matches the *[Baking Viewport Masks](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps)* of the *Bake Lighting* window.
4. Finally, set up light sources in the scene:

  - For [light sources](../../../editor2/lighting/lights/index.md#lights) that should contribute to lightmapping, select the **Static** [mode](../../../editor2/lighting/gi/index.md#bake_modes), *Dynamic* lights will be ignored. Only indirect lighting from lights is baked into lightmaps, so light sources are to be kept enabled to provide direct lighting and specular highlights.
  - For [emissive](../../../editor2/lighting/lights/index.md#emissive) surfaces (having *Emission* state in the material parameters enabled) also enable the *Emission Bake GI* option. Both direct and indirect (bounced) lighting from emissive materials is baked into lightmaps.
  - Lighting from Voxel and Environment Probes is not considered.
5. Proceed to light [baking](#bake).


### Levels of Detail


There is no need to bake a separate lightmap for each [level of detail](../../../principles/world_management/index.md#lods). You can save space and time by sharing already baked lightmaps between different LODs (works for LODs having the same UV maps):


1. Prepare a matching UV mapping in your modeling software to ensure that the lightmap is consistently mapped to similar parts of geometry. ![](lightmaps_lods.png)
2. Make sure to uncheck [automatic unwrapping](../../../editor2/fbx/index.md#options_lightmaps) in the import settings of the model to keep the prepared UVs.
3. Select the [**Bake Unique Texture**](../../../editor2/node_parameters/visual_representation/index.md#lightmaps_mode) mode for LOD 0.
4. Select the [**Reuse Texture From Other Surface**](../../../editor2/node_parameters/visual_representation/index.md#lightmaps_mode) mode for all other LODs that will share its lightmap. Specify the LOD 0 in their **Surface** parameter. ![](lightmaps_reuse.png)
5. Proceed to light baking to bake the lightmap for the LOD 0.
6. The lightmap texture baked for LOD 0 will be automatically used for the other LODs.


## Baking


![](bake_lightmaps.png)


1. Enable the *Lightmap* buffer: **Rendering -> Buffers -> Lightmap**.
2. Open the *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md)* window.
3. Enable **Bake Lightmaps for Surfaces**. Adjust the baking settings:

  - Set up the *Baking Viewport Masks*.
  - Select the desired baking **Quality**. The *Draft* option provides the shortest baking time and is suitable for development iterations, while the *Ultra* quality engages the biggest possible number of light rays to be simulated and the best sampling resolution.
  - Adjust the *Far Clipping Distance* for simulated light rays.
4. Adjust the *Common Settings*:

  - Select the **number of light ray bounces**. Higher values will result in a brighter lighting since each surface receives more photons.
  - Set the **number of samples calculated per frame**. This parameter is available for adjustment during baking process.
5. Start baking process by clicking *Bake All Lighting* and wait for it to finish. Live preview is available. Several iterations (one per bounce) will be simulated for each affected surface. You can stop the process at any moment by using the **Stop** button and you will be prompted to keep the achieved result or restore the previous textures.
6. Upon completion, generated lightmaps will be saved in the `bake_lighting/lightmaps` folder and applied to the corresponding surfaces.
7. In the materials settings of lightmapped surfaces, consider enabling the ***[Lightmap Cubic Filtering](../../../content/materials/library/mesh_base/index.md#option_light_map_cubic_filtering)*** option for better quality.
8. As a matter of fine-adjustment, tweak the ***[Lightmap Color](../../../editor2/settings/render_settings/global_illumination/index.md)*** parameter.


You can check the result by selecting the **Baked Lightmap** mode in the *Rendering Debug*.


![](lightmaps_0.png) ![](lightmaps_1.png)


If you are not satisfied with results on certain objects, you can select surfaces and/or nodes and perform partial re-bake using different settings by clicking ***Bake Selected*** in the *Bake Lighting* window.


![](partial_0.jpg) ![](partial_1.jpg)


*The lightmap texture of a single object was re-baked to get proper color reflection from floor.*


Objects with lightmaps assigned are free to be transformed and cloned (even though it is going to break consistency of lighting). The **Bake Unique Texture** mode ensures that re-baking lighting for several clones that have the same lightmap assigned will generate a separate lightmap texture for each surface.

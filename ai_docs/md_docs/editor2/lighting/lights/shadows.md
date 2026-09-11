# Shadows


UNIGINE provides realtime and precomputed shadows from light sources.


Shadows are cast using a commonly used technique called **Shadow Mapping**: a depth texture (or a cubemap for omni lights) is grabbed from the position of the light source and used to define lit and shaded areas.


**World** light sources use an advanced shadow mapping technique called [Parallel-Split Shadow Mapping](../../../principles/render/lights_shadows/shadows/pssm.md) to handle shadows at large distances. The [shadow settings](../../../objects/lights/world/index.md#shadow_settings) are available per each world light source.


To enable shadow casting from a light source, check the **Enabled** option in its [*Shadow* Settings](../../../objects/lights/parameters/index.md#shadow_settings):


![](shadows_enabled.png)


All light sources can be either in *[Dynamic or Static](../../../objects/lights/parameters/index.md#common_settings)* mode according to which it is decided if shadow maps are computed in real time or saved in an asset once, thus significantly reducing the number of polygons rendered each frame.


Each surface has the shadows-related [Rendering Parameters](../../../editor2/node_parameters/visual_representation/index.md#surface_rendering). For a surface to cast shadows, it should have the **Cast Proj and Omni Shadows** and **Cast World Shadows** options enabled, the [same options](../../../editor2/materials_settings/index.md#options) are available per material.


![The Shadow Mode parameter is set per surface](../../node_parameters/visual_representation/surface_rendering_advanced.png)


The surface's **Shadow Mode** is responsible for the type of shadows cast by the surface:


- **Static**. The surface casts both types of shadows: cached (from *static* lights) and dynamic (from *dynamic* lights).
- **Dynamic**. The surface casts shadow only if lit by a dynamic light or a static light with *Mixed* shadow mode. No shadows baked.


You can control shadow-related interactions between surfaces/materials and light sources by using the [Shadow Mask](../../../principles/bit_masking/index.md#shadow_mask).


### See Also


- Common [Shadow Settings](../../../objects/lights/parameters/index.md#shadow_settings) of light sources.
- Global [Shadow Settings](../../../editor2/settings/render_settings/shadows/index.md).
- Video tutorial: [Cached Shadows](../../../videotutorials/essentials/cached_shadows.md)
- Quick video guide: [Using Cached Shadows](../../../videotutorials/how_to/how_to_rendering/cached_shadows.md).


## Dynamic Shadows


![](shadows_dynamic.gif)


Dynamic or realtime shadows are useful in changing scenes: when a light source or objects lit by it move. In this case all affected geometry is rendered into shadow buffer one more time, which might affect the performance.


> **Notice:** You can estimate the number of polygons rendered into shadows by using the **Triangles Shadows** counter of the *[Performance Profiler](../../../tools/profiling/profiler/index.md#rtriangles_shadows)*.


To make a light source provide dynamic shadows, set the **[Mode](../../../objects/lights/parameters/index.md#common_settings)** to *Dynamic* and adjust the [Shadow Settings](../../../objects/lights/parameters/index.md#shadow_settings).


![](light_mode_dynamic.png)


## Cached Shadows


Mostly, virtual environments tend to be static. That is why it makes sense to drop the shadows computation each frame to gain the performance.


The idea behind precomputed Cached Shadows is to grab the shadow map of a light source and save it in an asset to be rendered later at run time.


To get shadows from a light source cached:


1. Select Static [*Shadow Mode*](../../../editor2/node_parameters/visual_representation/index.md#shadow_mode) for all stationary surfaces. This is the default mode for surfaces of [Mesh Static](../../../objects/objects/mesh/index.md) objects.
2. Open *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md)* window and check **Bake Static Shadows For Lights**. ![](bake_shadows.png) > **Notice:** Enable the *Automatic Rebake* option to make shadows for static light sources be automatically rebaked every time you make changes to their transformation and shadows-related settings.
3. Choose **Static** Mode for the light source. ![](light_mode_static.png)
4. In the *Shadow Settings*, select the **Static** shadow mode and Resolution of the shadow map. ![](shadows_settings_cached.png)
5. Click **Bake Selected** in the *Bake Lighting* window. The shadow map of the light source will be saved at the `bake_lighting/shadows` folder and assigned to the *Depth Texture* asset field.


After that, the light source will provide static cached shadows only. After changing light's position, rotation or parameters, it should be rebaked for proper shadow casting.


> **Notice:** It is not recommended to bake shadows for lights stored in multiple *[Node References](../../../objects/nodes/reference/index.md)* that refer to the same `.node` asset � the assigned textures will be lost. However, you can save a light source to a *Node Reference* after baking its shadows and clone, if needed. Make sure the *Automatic Rebake* option is disabled; otherwise, the shadow map will be re-baked.


World light sources require additional adjustments. For more details refer to the [Shadow Settings](../../../objects/lights/world/index.md#shadow_settings) of the World light.


## Mixing Dynamic and Cached Shadows


By using the *Mixed* shadow mode you can combine baked shadows from static geometry and realtime shadows cast by certain dynamic meshes:


1. Select Static [*Shadow Mode*](../../../editor2/node_parameters/visual_representation/index.md#shadow_mode) for all stationary surfaces.
2. Select Dynamic [*Shadow Mode*](../../../editor2/node_parameters/visual_representation/index.md#shadow_mode) for all moving or changing surfaces.
3. Open [Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md) window and check **Bake Static Shadows For Lights**. ![](bake_shadows.png)
4. Choose **Static** Mode for the light source. ![](light_mode_static.png)
5. In the Shadow Settings, select the **Mixed** shadow mode and Resolution of the shadow map. ![](shadows_settings_mixed.png)
6. Click **Bake Selected** in the *Bake Lighting* window to bake static shadows. The shadow map containing shadows cast by static geometry will be saved at the `bake_lighting/shadows` folder and assigned to the *Depth Texture* asset field.


After that, the light source will provide both cached and dynamic shadows. After changing light's position, rotation or parameters, it should be rebaked for proper shadow casting.


## Area Shadows


Soft shadows from area lights can be simulated for both static and dynamic light sources by using the [Penumbra Settings](../../../objects/lights/parameters/index.md#penumbra_mode).


![](../../../objects/lights/parameters/shadow_filter_on.jpg) ![](../../../objects/lights/parameters/shadow_penumbra_on.jpg)


## Screen-Space Shadows


[Screen-Space Shadows](../../../objects/lights/parameters/index.md#ss_shadow_settings) are raytraced shadows calculated in screen space. This effect does not depend on the polygon count, that is why it may be a great solution for small contact shadows or shadows at a high distance from the camera.


![](sss_0.png) ![](sss_1.png)

# Visual Representation


Visual representation of nodes can be changed by adjusting parameters of its *[surfaces](../../../principles/world_structure/index.md#surfaces_hierarchy)* on the *Node* tab of the *Parameters* window.


> **Notice:** Only nodes of the [object-related](../../../objects/objects/index.md) types can have surfaces.


Surfaces are organized in a hierarchy that displayed in the following section:


![](surfaces.png)

*Surfaces Hierarchy*


Surfaces can be filtered by name:


![](surface_filter.gif)

*Filtering Surfaces*


To change the surface parameters, select the required surface in the hierarchy and tweak its parameters. For each surface, the parameters listed below are available for editing.


## Rendering Parameters


![](surface_rendering_static.png) ![](surface_rendering_advanced.png)

*Rendering Settings*


This section provides parameters for setting up rendering of the surface and its shadows.


| Viewport Mask | *[Viewport](../../../principles/bit_masking/index.md#viewport)* mask of the surface. |
|---|---|
| Shadow Mask | *[Shadow](../../../principles/bit_masking/index.md#shadow_mask)* mask of the surface. |
| Lighting Mode | Preset defining the contribution of the surface to lighting: - **Static** mode is optimized for use in [static GI](../../../editor2/lighting/gi/index.md#static_gi), [static reflections](../../../editor2/lighting/gi/env_probes.md#static) and [cached shadows](../../../editor2/lighting/lights/shadows.md#cached). It affects the lighting-related parameters as follows: - [*Shadow Mode*](#shadow_mode) is set to **Static**. - [*Cast Global Illumination*](#cast_gi) is enabled. - [*Bake to Environment Probes*](#bake_to_environment_probes) is enabled. - [*Lightmaps Parameters*](#surface_lightmaps) are available. - **Dynamic** mode excludes the surface from use in static GI and static reflections and is suitable for dynamic shadows. It affects the lighting-related parameters as follows: - [*Shadow Mode*](#shadow_mode) is set to **Dynamic**. - [*Cast Global Illumination*](#cast_gi) is disabled. - [*Bake to Environment Probes*](#bake_to_environment_probes) is disabled. - [*Lightmaps Parameters*](#surface_lightmaps) are not available. - **Advanced** mode enables manual adjustment of all lighting-related settings. |
| Shadow Mode | Considering the concept of static and dynamic light, a surface can cast [static](../../../editor2/lighting/lights/shadows.md#cached) (using precomputed shadow texture) or [dynamic](../../../editor2/lighting/lights/shadows.md#dynamic) (geometry-based) shadow depending on the [light source mode](../../../objects/lights/parameters/index.md#light_mode). Two shadow modes are available: - **Static**. The surface casts both types of shadows: cached (from *static* lights) and dynamic (from *dynamic* lights). > **Notice:** In this mode, the *[Min Visibility](#min_visibility)* parameter of a surface should not be greater than 0. Otherwise, a shadow from a static light source wouldn't be baked. - **Dynamic**. The surface casts shadow only if lit by a dynamic light or a static light with *Mixed* shadow mode. No shadows are baked. |
| Cast Proj and Omni Shadows | Flag indicating if the surface casts shadows from *[projected](../../../objects/lights/proj/index.md)* and *[omni](../../../objects/lights/omni/index.md)* light sources. |
| Cast World Shadows | Flag indicating if the surface casts shadows from *[world](../../../objects/lights/world/index.md)* light sources. |
| Cast Global Illumination | Flag indicating if the surface is to be baked to [static GI](../../../editor2/lighting/gi/index.md#static_gi). |
| Bake to Environment Probes | Flag indicating if the surface is to be baked to *[environment probes](../../../objects/lights/envprobe/index.md)*. |
| Cast Environment Probe Shadows | Flag indicating if the surface casts shadows from *[environment probes](../../../objects/lights/envprobe/index.md)*. This option is required for the *[Cutout by Shadow](../../../objects/lights/envprobe/index.md#cutout_by_shadow)* feature. |


## Lightmaps Parameters


![](surface_lightmaps.png)

*Lightmaps Settings*


> **Notice:** Lightmap Parameters are available only for surfaces of [Static Mesh](../../../objects/objects/mesh/index.md) objects in the **Static** or **Advanced** [**Lighting Mode**](#lighting_mode).


This section provides [lightmapping](../../../editor2/lighting/gi/lightmaps.md)-related parameters for the surface.


| Enabled | Flag indicating if lightmapping and related parameters are enabled for the surface. |
|---|---|
| Mode | Option indicating the lightmapping mode for the surface: - **Bake Unique Texture** � bake lighting into a new texture. - **Use Custom Texture** � specify a lightmap texture from assets. - **Reuse Texture From Other Surface** � use the lightmap texture from another surface. This option is intended for use with LODs having the same UV maps. |
| Bake To | Target asset for baking and storing the lightmap texture in the *[Bake Unique Texture](#lightmaps_mode)* mode. If the value is empty, a new lightmap texture will be created and assigned to this parameter upon light baking. |
| Texture | Lightmap texture assigned to the surface in the *[Use Custom Texture](#lightmaps_mode)* mode. |
| Quality | Lightmap baking quality preset: - **Global** � the global quality preset set in the *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps)* settings. - **Draft** option provides the highest iterativity with the lowest sampling quality and number of rays simulated. - **Low** option provides low sampling quality and number of light rays simulated. - **Medium** option corresponds to stable quality level which is good for most cases. - **High** option corresponds to high sampling quality and number of light rays simulated intended for release production. - **Ultra** baking quality might be useful to get rid of small inconsistencies on the release production. |
| Compression | Flag indicating if the baked lightmap texture should be compressed. > **Notice:** Compressed lightmaps are lightweight but can be subject to compression artifacts. |
| Surface | The surface providing the lightmap texture when the *[Reuse Texture From Other Surface](#lightmaps_mode)* mode is selected. |


## LOD Parameters


![](surface_lod.png)

*LOD Settings*


This section provides parameters for setting up surface [LODs](../../../principles/world_management/index.md#lods).


> **Notice:** All distances listed below are measured from the camera to the object's pivot point. Make sure that all pivots are set properly, otherwise wrong LOD management is imminent.


| Min Visibility | Minimum visibility distance from the camera when a surface starts to appear on the screen. By default it is -inf. |
|---|---|
| Max Visibility | Maximum visibility distance when a surface is no longer fully visible: it can either disappear completely or start to fade out. By default it is inf. |
| Min Fade | Minimum fade distance, over which the surface fades in until it is completely visible. Along this distance the engine will automatically interpolate the level of detail from alpha of 0.0 (completely invisible) to 1.0 (completely visible). Fading in starts when the camera has reached the [minimum distance of surface visibility](#min_visibility) and is in the full visibility range. |
| Max Fade | Maximum fade distance, over which the surface fades out until it is completely invisible. Fading out starts when the camera has reached the [maximum distance of surface visibility](#max_visibility) and is out of the full visibility range. |
| Min Parent | [Reference object](../../../principles/world_management/index.md#reference_object), from which the [minimum visibility distance](#min_visibility) of the surface is measured. - If 0 is set, the minimum visibility distance is measured from the current surface. - If 1 is set, the distance is measured from the surface one level up in the surfaces hierarchy. If there is no parent surfaces, the distance will be measured from the node it belongs to. - For higher numbers, the reference object is found **n** levels up in the surfaces hierarchy. If the number of parent surfaces is less than the specified value, the node or its parent will be used as the reference object. The reference object is used to ensure simultaneous LOD switching for all surfaces. |
| Max Parent | [Reference object](../../../principles/world_management/index.md#reference_object), from which the [maximum visibility distance](#max_visibility) of the surface is measured. The same principle as for the [minimum parent](#min_parent) is used to count it. The reference object is used to ensure simultaneous LOD switching for all surfaces. |


## Surface Custom Texture Parameters


![](surface_custom_texture.png)

*Custom Texture Settings*


> **Notice:** Custom texture parameters are available only for surfaces of [Static Mesh](../../../objects/objects/mesh/index.md) objects.


This texture gives you a wide range of opportunities for customization, and enables you to optimize the number of materials while extending visual diversity. For example, instead of tweaking a set of similar materials for different surfaces, you can assign a unique custom texture to each surface and use a single material with the final look depending on the custom texture.


> **Notice:** In the [Material Editor](../../../content/materials/graph/index.md) you can refer to this texture via the **[Surface Custom Texture](../../../content/materials/graph/node_library/textures/surface_custom_texture.md)** node.


| Enabled | Flag indicating if surface custom texture and related parameters are enabled for the surface. |
|---|---|
| Mode | Defines the source of the custom texture for the surface: - **Unique Texture** � use a unique custom texture for this surface. You can specify an existing texture from your assets or create a new one and edit in the *[Texture Paint Mode](../../../editor2/texture_editor/index.md)*. - **Reuse Texture From Other Surface** � use the custom texture from another surface. This option is intended for use with LODs having the same UV maps. |
| Texture | Custom texture asset assigned to the surface. Click ![](../../settings/render_settings/color/plus.png) to create a new one. |
| Surface | The source surface providing the custom texture to be reused for this surface when the *[Reuse Texture From Other Surface](#surface_custom_texture_mode)* mode is selected. |


## Material Parameters


![](surface_material.png)

*Material Settings*


In this section, a material can be assigned to the surface and then material's parameters can be tweaked (if the material is [editable](../../../content/materials/index.md#user_materials)). Here you can also inherit a new material from the material assigned to the surface: it will be assigned automatically. To inherit the material, click ![](material_inherit.png) right to the field with the material name.  To set the default material, click ![](../default_value.png) right to the field with the material name.


The material parameters can also be changed on the *[Material](../../../editor2/materials_settings/index.md)* tab of the *Parameters* window: it becomes available when the target material is selected in the *[Material Hierarchy](../../../editor2/materials_settings/organizing_materials/index.md)* window.


## Quick Copy and Paste Operations


You can copy and paste all parameters from one surface to another using the following context menu displayed by clicking ![](../copy_paste.png) in the top-right corner of the *Surfaces* section.


![](copy_paste_params.png)

*Context menu for copying and pasting surface parameters*


The copy/paste option supports multi-selection. This can be especially useful, when [setting up LODs](../../../content/optimization/geometry/lods/index.md#setup) for several models, for example. Suppose you have 3 LODs in each model as separate surfaces, you just set up parent, visibility and fade distances for the three surfaces of one model, then select these surfaces and click **Copy Parameters** in the context menu shown above, then select three corresponding surfaces of another model and select one of the following options:


- **Paste Parameters Sequentially** � in this case the parameters copied from source surfaces will be simply pasted to destination surfaces in the order they appear in the hierarchy.
- **Paste Parameters By Surface Names** � in this case the parameters copied from source surfaces will be pasted to destination surfaces with matching names.


![](surface_copypaste.gif)

*Setting up LODs with multi-selection copy/paste of surface parameters*


The **Copy Surface Name** option is also available in the context menu. It allows copying the name of the selected surface.

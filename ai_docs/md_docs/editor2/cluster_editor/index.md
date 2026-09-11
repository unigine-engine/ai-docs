# Brush-Based Placement of Meshes


*Cluster Editor* is a convenient tool for brush-based placement of meshes baked into *Mesh Clusters* directly in the scene. It allows editing the existing *Mesh Clusters* and creating new ones.


![](cluster_editor.gif)


Cluster Editor is available when the *Cluster Paint Mode* is selected on the [toolbar](../../editor2/interface/index.md#tools_panel).


> **Notice:** To learn how to use the tool, watch [this video tutorial](#video).


![](cluster_editor_mode.png)


Switching to Cluster Paint Mode opens the *Active Tool* window:


![](active_tool.png)


In the *Objects* section, there is a list of all *Mesh Cluster* objects available in the world. Similarly to the *[World Hierarchy](../../editor2/organizing_nodes/index.md)* window, you can organize the nodes:


- Select one or several nodes.
- Toggle the nodes on and off.
- Filter nodes by name.
- Rename a node by double-clicking on it.
- Toggle the ![](edit.png) **[Spawn When Drawing](#spawn_when_drawing)** flag.


To edit the required *Mesh Clusters* (one or many), select them either in the *Objects* section or in the *World Hierarchy* window and specify the [Objects settings](#objects_settings).


For convenience, the **Create New Cluster** button, a shortcut to [manual creation of Mesh Clusters](../../objects/objects/mesh_cluster/index.md#creating), is available right in the *Active Tool* window.


### See Also


- Article on *[Mesh Cluster](../../objects/objects/mesh_cluster/index.md)*
- Using [Cluster Editor for Vegetation](../../content/tutorials/vegetation/index.md#cluster)


## Editing Mesh Clusters with Cluster Editor


As soon as you have at least one *Mesh Cluster* with the **Spawn When Drawing** flag enabled, brush painting is available in the *Editor Viewport*. Select the required tool and start editing the cluster directly in the scene:


![](brush_viewport.png)


Available tools:


- ![](brush_replace.png) **Replace Density** � replace meshes within the *Brush Radius* with new ones spawned in accordance with the current density values.
- ![](brush_single.png) **Single Object** � place a single mesh at the desired point.
- ![](brush_erase.png) **Erase** � remove meshes.


### Brush Settings


| Radius | Size of the brush. The size change is non-linear - the standard increment changes depending on the current brush value: - 0.01 for values in range from 0.1 to 1.0 - 0.1 for values in range from 1.0 to 10.0 - 1.0 for values in range from 10.0 to 100.0 - etc. You can also control the current step by holding hotkeys while scrolling the mouse wheel: the ***Shift*** key increases the step 10 times, while the ***Ctrl*** key enables a 10-fold decrease. |
|---|---|
| Density Multiplier | Global multiplier for [density](#density). The value can be increased above 1. |
| Filter | Allows specifying the type of object on which you can paint. You can select multiple values, but some of them cannot be combined (see details below). The following values are available: - **Mesh Static** - **Mesh Skinned** - **Mesh Dynamic** - **Mesh Cluster** > **Notice:** Painting over a Mesh Cluster object is available only if the [**Spawn When Drawing**](#spawn_when_drawing) flag is disabled for it. - **Mesh Clutter** - **Terrain** - **Water** - **Clouds** In addition, there are 2 filters that can only be used in combination with one or more object type filters listed above: - **Draw Only On Immovable Nodes**, i.e. on nodes that have the [*Immovable*](../../editor2/node_parameters/transformation_common/index.md#clutter) flag enabled. This filter can be used only with the **Mesh Static** and/or **Mesh Cluster** filters. - **Draw Only On Surfaces With Intersection**, i.e. on surfaces that have the [*Intersection*](../../editor2/node_parameters/physics/index.md#intersection_enabled) flag and any bit of the [Intersection Mask](../../principles/bit_masking/index.md#intersection_mask) enabled. > **Notice:** The filters aren't applied for the Erase tool. |


### Controls


- To draw with a brush, click ***LMB*** and drag the mouse.
- To change the brush [radius](#radius), use the ***mouse wheel***.
- To switch to the *Replace Density* tool, press **B**.
- To switch to the *Erase* tool, press **E**.


> **Notice:** You can adjust the controls in the *Cluster Paint Mode* tab of the *[Editor Hotkeys](../../editor2/settings/hotkeys/index.md)* settings.


## Objects Settings


The following settings are saved for each *Mesh Cluster* in the scene:


| Spawn When Drawing | Flag indicating if the *Mesh Cluster* is editable. > **Notice:** You should disable this flag to paint over the Mesh Cluster object. |
|---|---|
| Seed | Pseudo-random seed that defines the distribution of spawned meshes. Click the ![](dice.png) *Randomize* button to generate a new *Seed*. > **Notice:** If the same *Seed* value is set for several *Mesh Clusters*, their new meshes will spawn at the same points during one stroke. |
| Density | The target density of meshes of the *Mesh Cluster*. |
| Normal Orientation | Flag indicating whether new meshes should orient along the normals of surfaces under the brush. |
| Local Offset | Minimum and maximum offset values for new meshes with regard to normal orientation. |
| World Offset | Minimum and maximum offset for new meshes in world coordinates. |
| Local Rotation | Minimum and maximum rotation values for new meshes with regard to normal orientation. |
| World Rotation | Minimum and maximum rotation values for new meshes in world coordinates. |
| Scale | Minimum and maximum scale values for new meshes. Click the ![](scale_gear.png) gear icon to choose the scale mode: - **Uniform** � meshes are scaled uniformly along all axes. - **Nonuniform** � scale is random along each axis. |


## Video Tutorial


Watch the video below to learn the basics of mesh placement with the Cluster Brush Editor.

# Mesh Decal


A **Mesh Decal** is a [decal](../../../objects/decals/index.md) based on the arbitrary `.mesh` file and projected onto a surface by means of the [orthographic projection](../../../objects/decals/ortho/index.md#orthographic).


> **Notice:** The decals are always of the same size regardless of the projection box location relatively to the projection surface.


[![](index_sm.jpg)](index.jpg)

*Roads Based on theMesh Decal*


### See Also


- The *[DecalMesh](../../../api/library/decals/class.decal_cpp.md)* class to manage mesh decals via API


## Mesh Requirements


The mesh used for projection onto a decal comply with the following requirements:


- The mesh shouldn't be two-sided or have any overlapping parts � this causes sorting artifacts. The mesh, however, may be curved in order to be applied to the sides of the object onto which it is projected by enabling the *[Screen Projection](../../../content/materials/library/decal_base/index.md#option_screen_proj)* option. | ![](incorrect_mesh_projected.jpg) | ![](correct_mesh_projected.jpg) | |---|---| | *Mesh used for projection has overlapping parts of surface that cause artifacts* | *Any unnecessary surfaces are cut off the mesh to have it projected correctly* |
- The mesh triangles should be as close to regular as possible � don't use triangles with one side significantly less than the other two sides.
- A source mesh should have less than 10,000 polygons.
- The mesh that is used for projection should contain a single surface. If the mesh contains several surfaces, only the one with the 0 index will be used. Thus, the area of the decal will differ from the initial mesh.


## Creating a Mesh Decal


To create a *Mesh Decal*:


1. On the Menu bar, choose *Create -> Decal -> Mesh*. ![](create_decal_mesh.png)
2. In the file dialog window that opens, choose a mesh for the decal that is in line with the [mesh requirements](#requirements): ![](path.png)
3. Press the *OK* button and place the decal somewhere in the world (for the decal to be projected, the mesh should intersect the surface). ![](place_decal_mesh.png)


## Editing a Mesh Decal


In the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the *Mesh Decal*:


![](settings_decal_mesh.png)

*Nodetab*


### Decal Mesh


Projection parameters of the *Mesh Decal*:


| Radius | The height of the projection box along the *Z* axis, in units. \| ![](radius_1.png) \| ![](radius_0.png) \| \|---\|---\| \| *Radius = 10* \| *Radius = 20* \| | ![](radius_1.png) | ![](radius_0.png) | *Radius = 10* | *Radius = 20* |
|---|---|---|---|---|---|
| ![](radius_1.png) | ![](radius_0.png) |  |  |  |  |
| *Radius = 10* | *Radius = 20* |  |  |  |  |
| Mesh | Path to the `.mesh` file on which the decal is based. |  |  |  |  |


### Decal Common


Parameters common for all types of decals:


#### Bit Masks


| Viewport Mask | A [*Viewport* mask](../../../principles/bit_masking/index.md#viewport), specifying if the decal can be seen in the camera's viewport. |
|---|---|
| Intersection Mask | The decal's [*Intersection* mask](../../../principles/bit_masking/index.md#intersection_mask) is used paired with the cutout intersection mask of [clutters](../../../objects/objects/mesh_clutter/index.md#cutout_intersection) and [grass](../../../objects/objects/grass/settings.md#cutout_intersection) to cut out the clutter or grass in the areas of intersection with the decal (e.g. can be used to remove grass from the surface of a road projected using decal). |


> **Notice:** You can specify a *Shadow* mask and a *Material* mask in the [decal_base](../../../content/materials/library/decal_base/index.md) material.


#### Visibility Parameters


Parameters controlling decal's visibility:


| Min Visibility | A minimum visibility distance, starting at which the decal begins to fade in and then becomes completely visible, in units. |
|---|---|
| Min Fade | A minimum fade-in distance, across which the decal smoothly becomes visible due to the alpha fading. It is counted starting from the minimum visibility distance value, in units. |
| Max Visibility | A maximum visibility distance, starting at which the decal begins to fade out until becomes completely invisible, in units. |
| Max Fade | A maximum fade-out distance, across which the decal smoothly becomes invisible due to the alpha fading. It is counted starting from the maximum visibility distance value, in units. |
| Opacity | Opacity of the decal. This parameter enables you to control whether the decal should be semi-transparent or fully opaque (by the value of 1). |


### Setting a Material


The [material](../../../content/materials/index.md) selection:


| Material | A new material for the decal. |
|---|---|

# Orthographic Decal


An **Orthographic Decal** is a [decal](../../../objects/decals/index.md) projected onto a surface by means of orthographic projection.


![](decal_ortho.png)

*Orthographic decals*


> **Notice:** These decals are always of the same size regardless of the projection box location relatively to the projection surface.


Orthographic projection is a form of parallel projection, where all the projection lines are orthogonal to the projection plane, resulting in every plane of the scene appearing in affine transformation on the viewing surface.


![](projection.png)

*Orthographic Projection*


Orthographic decals are the most reliable ones as projected from a surface and cannot cause unexpected artifacts (as may [perspective projected decals](../../../objects/decals/proj/index.md)).


![](index.png)

*Orthographic Projection Box*


### See Also


- The *[DecalOrtho](../../../api/library/decals/class.decalortho_cpp.md)* class to manage *Orthographic Decals* via API
- The *[decal_base](../../../content/materials/library/decal_base/index.md)* material to be applied to the decal


## Creating an Orthographic Decal


To create an orthographic decal, perform the following:


1. On the Menu bar, choose *Create -> Decal -> Orthographic*. ![](create_decal_ortho.png)
2. Place the decal on the existing surface (for the decal to be projected, the projection box should intersect the surface) and specify the required [settings](#editing): ![](place_decal_ortho.png) *Placement of the orthographic decal*


## Editing an Orthographic Decal


In the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the orthographic decal:


![](settings_decal_ortho.png)

*Decal Orthotab*


### Decal Ortho


Projection parameters of the orthographic decal:


| Radius | The length of the projection box along the *Z* axis, in units. \| ![](radius_0.png) \| ![](radius_1.png) \| \|---\|---\| \| *Radius = 0.5* \| *Radius = 1* \| The second case shows that the decal is projected only if its projection box intersects the surface. | ![](radius_0.png) | ![](radius_1.png) | *Radius = 0.5* | *Radius = 1* |
|---|---|---|---|---|---|
| ![](radius_0.png) | ![](radius_1.png) |  |  |  |  |
| *Radius = 0.5* | *Radius = 1* |  |  |  |  |
| Width | The length of the projection box along the *X* axis, in units. |  |  |  |  |
| Height | The length of the projection box along the *Y* axis, in units. |  |  |  |  |
| ZNear | The value of the near clipping plane, ranging from 0 to 1. |  |  |  |  |


### Decal Common


Parameters common for all types of decals:


#### Bit Masks


| Viewport Mask | A [*Viewport* mask](../../../principles/bit_masking/index.md#viewport), specifying if the decal can be seen in the camera's viewport. |
|---|---|
| Intersection Mask | The decal's [*Intersection* mask](../../../principles/bit_masking/index.md#intersection_mask) is used paired with the cutout intersection mask of [clutters](../../../objects/objects/mesh_clutter/index.md#cutout_intersection) and [grass](../../../objects/objects/grass/settings.md#cutout_intersection) to cut out the clutter or grass in the areas of intersection with the decal (e.g. can be used to remove grass from the surface of a road projected using decal). |


> **Notice:** You can specify a *Shadow* mask and a *Material* mask in the *[decal_base](../../../content/materials/library/decal_base/index.md)* material.


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

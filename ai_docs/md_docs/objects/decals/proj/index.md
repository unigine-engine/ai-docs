# Projected Decal


A **projected decal** is a [decal](../../../objects/decals/index.md) projected onto a surface by means of perspective projection. You can create an instance of the image projected onto a surface from a single point as a cone. These decals are of the same scale in spite of how far the surface they are projected onto is.


![](decal_proj.png)

*Projected decals*


> **Notice:** Changing of the projection pyramid location relatively to the projection surface changes the size of the decal in accordance with the laws of perspective.


When the human eye views a scene, objects in the distance appear smaller than objects close by � this is known as perspective.


![](projection.png)

*Perspective Projection*


While [orthographic projection](../../../objects/decals/ortho/index.md#orthographic) ignores this effect to allow accurate measurements, perspective definition shows distant objects as smaller to provide additional realism.


![](index.png)

*Perspective Projection Pyramid*


### See Also


- The *[DecalProj](../../../api/library/decals/class.decalproj_cpp.md)* class to manage projected decals via API


## Creating a Projected Decal


To create a projected decal, perform the following:


1. In the Menu bar, choose *Create -> Decal -> Projected*. ![](create_decal_proj.png)
2. Place the decal on the existing surface (for the decal to be projected, the projection pyramid should intersect the surface) and specify the required [settings](#editing): ![](place_decal_proj.png) *Placement of the Projected Decal*


## Editing a Projected Decal


In the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the projected decal:


![](settings_decal_proj.png)

*Nodetab of a projected decal*


### Decal Projected


Projection parameters of the projected decal:


| Radius | The height of the projection pyramid along the *Z* axis, in units. |
|---|---|
| Field of View | The field of view of the decal's projector, in degrees. |
| Aspect | The aspect ratio of the decal, in units. |
| ZNear | The value of the near clipping plane, ranging from 0 to 1. |


### Decal Common


Parameters common for all types of decals:


#### Bit Masks


| Viewport Mask | A [*Viewport* mask](../../../principles/bit_masking/index.md#viewport), specifying if the decal can be seen in the camera's viewport. |
|---|---|
| Intersection Mask | The decal's [*Intersection* mask](../../../principles/bit_masking/index.md#intersection_mask) is used paired with the cutout intersection mask of [clutters](../../../objects/objects/mesh_clutter/index.md#cutout_intersection) and [grass](../../../objects/objects/grass/settings.md#cutout_intersection) to cut out the clutter or grass in the areas of intersection with the decal (e.g. can be used to remove grass from the surface of a road projected using decal). |


> **Notice:** You can specify a *Shadow* mask and a *Material* mask in the *[decal_base](../../../content/materials/library/decal_base/index.md)*material.


#### Visibility Parameters


Parameters controlling the decal's visibility:


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

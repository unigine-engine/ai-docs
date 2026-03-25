# Field Animation


An **animation field** is an object, specifying geometry areas of grass and vegetation that should be animated. It affects animation parameters of leaf and stem materials applied to grass and vegetation.


> **Notice:** These parameters will be affected by the animation field only when the *Field* mode is set for the *Animation* option of the corresponding material on the *States* tab.


An animation field can be used, for example, to create local rotor downwash effects on grass and trees.


![](index.jpg)


> **Notice:** The maximum number of FieldAnimations rendered per frame/bit mask is limited to:
> - **341** (DirectX)


### See also


- The *[FieldAnimation](../../../../api/library/fields/class.fieldanimation_cpp.md)* class to manage animation fields via API
- A set of samples located in the `data/samples/fields/` folder:

  - `animation_00`
  - `animation_01`


## Animating Geometry with Animation Field


To animate some specific part of grass or vegetation with an animation field, do the following:


1. Add an animation field to the world: on the Menu bar, choose *Create -> Field -> Animation* and place the node in the world. ![](add_animation.png) > **Notice:** The animation field will affect only those part of grass or vegetation that is inside it.
2. Set up the added animation field: check the *Ellipse* option (if required), set the size of the field. For example: ![](anim_field_setup.png) ![](anim_field.jpg)
3. In the *[Materials Hierarchy](../../../../editor2/materials_settings/organizing_materials/index.md)* window, select the material applied to grass or vegetation and go to the ***States*** tab in the *Parameters* window. Change the value of the *Animation* option to Field. This will allow the field to affect the grass. ![](anim_field_material.png)
4. Make sure that the *[Field mask](../../../../objects/objects/grass/index.md#field_mask)* of the animation field matches the *Field* mask of the [grass](../../../../objects/objects/grass/index.md#field_mask) object or stem and leaf materials (in case of animating vegetation).
5. In the *Field Animation* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), specify the required animation parameters. For example, you can increase the *Stem* option to 3 so that the movement amplitude of the grass inside the animation field differs from the movement amplitude of all the other polygons. In the result, animation of the grass area inside the animation field will visually differ from the grass outside the field. ![](grass_animated.gif)


## Editing Field Animation


In the *Field Animation* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), the following parameters of the animation field can be adjusted:


![](edit_animation.png)


### Setting Form of Field


| Ellipse | Indicates whether the animation field is ellipsoid-shaped. If unchecked, the animation field has a form of a cube. |
|---|---|


### Setting Bit Masks


| Field Mask | A field mask. A bit mask that specifies an area of the animation field to be applied to grass or vegetation. The animation field will be applied only if both the field and grass (or vegetation) have [matching masks](../../../../principles/bit_masking/index.md). |
|---|---|
| Viewport Mask | A viewport mask. A bit mask for rendering the animation field into the current viewport. For the animation field to be rendered into the viewport, its mask should match the camera viewport mask. |


### Setting Size and Attenuation


| Size | Size of the animation field along the axes in units. - If the *Ellipse* option is unchecked, this is the size of the animation field box along the axes. - If the *Ellipse* option is checked, these are the ellipse radius values along the axes. |
|---|---|
| Attenuation | An attenuation factor indicating how much animation attenuates starting from the center of the animation field to its edges. - By the minimum value of 0, no animation will be visible. - The higher the value, the more intensive animation will be at the edges of the animation field. |


### Setting Animation Parameters


> **Notice:** The field animation effect is not multiplied by [render vegetation animation settings](../../../../editor2/settings/render_settings/vegetation/index.md#animation_stem).


| Stem | Scale for movement amplitude of grass and vegetation stems inside the animation field. |
|---|---|
| Leaf | Scale for rotation angle of vegetation leaves inside the animation field. |
| Scale | Scale for speed of vegetation swaying. |
| Wind | Wind direction inside the animation field. |

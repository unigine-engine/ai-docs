# Field Spacer


A **Field Spacer** is an object, specifying geometry areas of [grass](../../../../objects/objects/grass/index.md) and [water](../../../../objects/objects/water/index.md) that should not be rendered. Inside the *Field Spacer*, geometry is cut off gradually starting from the center of the field.


The *Field Spacer* allows you to dynamically adapt grass and water surface to other objects in the scene. For example:


- A *Field Spacer* can be used to specify area under a building and around it where grass should not grow. Moreover, by using the [attenuation factor](#attenuation), it is possible to create thinner grass around the building.
- A *Field Spacer* can be set for a boat so that water is not rendered inside it.


> **Notice:** A *Field Spacer* affects grass or water only if the *FieldSpacer Interaction* flag is set on the *States* tab of the corresponding material.


| ![](boat_without_spacer.jpg) | ![](boat_with_spacer.jpg) |
|---|---|
| *Boat without theField Spacer: water is inside the boat* | *Boat with theField Spacer: theField Spacercuts water off* |


> **Notice:** The maximum number of *FieldSpacers* rendered per frame/bit mask is limited to:
> - **341** (DirectX)


### See also


- The *[FieldSpacer](../../../../api/library/fields/class.fieldspacer_cpp.md)* class to manage spacer fields via API
- A set of samples located in the `data/samples/fields/` folder:

  - `spacer_00`
  - `spacer_01`
  - `spacer_02`


## Adding Field Spacer


To add a *Field Spacer* in the world via UnigineEditor, do the following:


1. On the Menu bar, choose *Create -> Field -> Spacer*. ![](add_spacer.png)
2. Place the spacer field in the world so that it intersects geometry required to be cut off: > **Notice:** Make sure that the *Spacer interaction* flag is set for materials applied to grass or water.

  - In case of grass, the *Field Spacer* should intersect the surface, on which grass grows.
  - In case of water, the *Field Spacer* should intersect the water surface: | ![](spacer_water.jpg) | |---|


If you are going to use the *Field Spacer* with dynamic objects, it is better to add the field as a child node to this object so that it can correctly affect grass or water geometry.


## Editing Field Spacer


In the *Field Spacer* section (*[Parameters](../../../../editor2/node_parameters/index.md)* window -> *Node* tab), the following parameters of the *Field Spacer* can be adjusted:


![](edit_spacer.png)


### Setting Form of Spacer


| Ellipse | Indicates whether the *Field Spacer* is ellipsoid-shaped. If unchecked, the *Field Spacer* has a form of a cube. |
|---|---|


### Setting Bit Masks


| Field Mask | A field mask. A bit mask that specifies an area of the *Field Spacer* to be applied to grass or water. The *Field Spacer* will be applied to grass or water only if they have [matching masks](../../../../principles/bit_masking/index.md). |
|---|---|
| Viewport Mask | A *Viewport* mask. A bit mask for rendering the *Field Spacer* into the current viewport. For the *Field Spacer* to be rendered into the viewport, its mask should match the camera viewport mask. |


### Setting Size and Attenuation


| Size | Size of the *Field Spacer* along the axes in units. - If the *Ellipse* option is unchecked, this is the size of the *Field Spacer* box along the axes. - If the *Ellipse* option is checked, these are the ellipse radius values along the axes. |  |  |  |  |
|---|---|---|---|---|---|
| Attenuation | An attenuation factor indicating how much geometry is cut off gradually starting from the center of the *Field Spacer*. - By the minimum value of 0, all geometry inside the *Field Spacer* will be rendered. - The higher the value, the less geometry will be rendered inside the *Field Spacer*. \| ![](spacer_atten_5.jpg) \| ![](spacer_atten_15.jpg) \| \|---\|---\| \| *Atten = 5* \| *Atten = 15* \| | ![](spacer_atten_5.jpg) | ![](spacer_atten_15.jpg) | *Atten = 5* | *Atten = 15* |
| ![](spacer_atten_5.jpg) | ![](spacer_atten_15.jpg) |  |  |  |  |
| *Atten = 5* | *Atten = 15* |  |  |  |  |

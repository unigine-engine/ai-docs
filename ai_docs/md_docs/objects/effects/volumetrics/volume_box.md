# Volume Box


*Volume Box* is a cuboid shaped volume that can be used to simulate:


- [Fog](../../../content/materials/library/volume_fog_base/index.md), haze or mist that hides objects behind it. If boxes with fog intersect, denser fog is created.
- [Clouds](../../../content/materials/library/volume_cloud_base/index.md) or shaped fog.
- [Light shafts](../../../content/materials/library/volume_shaft_base/index.md) from the world light source. For sun beams to fall through windows and other openings, the room should be inside the box.


![Volume box with a fog material](box_fog.jpg)

*Volume Box with a fog material on the floor*


![Volume box with a fog material](box_wireframe.jpg)

*Volume Box with a fog material*


### See also


- The *[ObjectVolumeBox](../../../api/library/objects/class.objectvolumebox_cpp.md)* class to edit *Volume Box* objects via API


## Creating a Box Object


To create a Box object, perform the following steps:


1. On the Menu bar, click *Create -> Volume -> Box*. ![](volume_box_create.png)
2. Place the Box object somewhere in the world.
3. Specify the Box object [parameters](#volume_box_parameters).


## Box Parameters


In the *Volume Box* section (*[Parameters](../../../editor2/node_parameters/index.md)* window -> *Node* tab), you can adjust the following parameters of the *Volume Box*:


![](volume_box_params.png)


| Edit Size | Toggles the editing mode for the *Volume Box* node. When enabled, the *Volume Box* sides that can be resized are highlighted with the colored rectangles. To change the size of a side, drag the corresponding rectangle. ![](editing_volume_box.jpg) |
|---|---|
| Size | Length, width, and height of the box (in units) along X, Y, and Z axes. |

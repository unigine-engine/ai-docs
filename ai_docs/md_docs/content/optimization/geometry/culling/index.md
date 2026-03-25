# Occlusion Culling


Object culling allows you not to render objects which are not presented in the viewing frustum. The particular cases of occlusion culling are the following:


- Occluders: *[box](../../../../objects/worlds/world_occluders/occluder_object/index.md), [mesh](../../../../objects/worlds/world_occluders/occluder_mesh/index.md)*.
- [Hardware occlusion queries](../../../../editor2/node_parameters/transformation_common/index.md#query) for objects with heavy shaders.


> **Notice:** As the object's bounding box is used for occlusion culling (it is checked if the bounding box is visible or not), it is recommended to export objects from 3D computer graphics software in local coordinates to make bounds of the mesh closer to geometry.


## Occluders


Occluders allow culling geometry that isn't visible behind them. There are 2 types of occluders:


- [Box-shaped occluder](../../../../objects/worlds/world_occluders/occluder_object/index.md)
- [Mesh-based occluder](../../../../objects/worlds/world_occluders/occluder_mesh/index.md)


The type of occluder to be used is defined by geometry to be culled.


Occluders can be very effective in case of complex environments where there are many objects that occlude each other and are costly to render (they have a lot of polygons and/or heavy shaders).


> **Notice:** Using occluders to cull large objects with a few surfaces may cause additional performance loss. Moreover, occluders aren't effective in scenes with flat objects, or when a camera looks down on the scene from above. So, when using the occluders, you should take into account peculiarities of objects to be culled.


Before using occluders, check the following:


- Rendering of occluders is enabled: in the Menu Bar, *Rendering -> Occlusion Culling -> Occluders* is toggled on.
- Rendering of shadows from the occluded objects is disabled: in the Menu Bar, choose *Rendering -> Occlusion Culling* and toggle *Shadows Culling* on. > **Notice:** You can leave shadows rendering enabled, if necessary.


Usage of occluders is shown in the [Content Optimization](https://youtu.be/Iqsr3fEvnis?t=456) video tutorial.


### Using a Box-Shaped Occluder


The *[occluder](../../../../objects/worlds/world_occluders/occluder_object/index.md)* is a box shape that culls objects' surfaces, bounds of which aren't visible behind it. This is the simplest type of occluders that should be used together with box-shaped objects that block off other objects. For example, you can add an occluder the shape of which coincides with the bounds of a building to avoid rendering of objects behind this building.


![](box_occluder.png)

*Box-shaped occluder inside building*


To create a box-shaped occluder, perform the following:


1. In the Menu Bar, choose *Create -> Optimization -> Occluder* and add the occluder as a child to the node that should occlude other objects.
2. In the *Common* section of the *Node* tab in the *Parameters* window, set the position of the occluder to the parent one. ![](set_to_parent.png)
3. In the *World Occluder* section of the *Node* tab, click **[Edit Size](../../../../objects/worlds/world_occluders/occluder_object/index.md#edit)** to enable the editing mode for the occluder. Resize the occluder by using the colored rectangles on the occluder box sides so that it coincides with the parent node size. > **Notice:** You can also use the *[Size](../../../../objects/worlds/world_occluders/occluder_object/index.md#size)* parameter to set the size along the axes. ![](occluder_size.png)
4. Specify the *[Distance](../../../../objects/worlds/world_occluders/occluder_object/index.md#distance)* between the camera and the occluder, at which the occluder doesn't occlude anything and, therefore, should be disabled to avoid negative impact on the performance. ![](occluder_distance.png)


To check how the occluder works, disable the parent node and then try to toggle the occluder on and off:


![](box_occluder_on.png) ![](box_occluder_off.png)


By default, the front faces of the occluder are used to cull objects. However, if the camera is inside the occluder (e.g. inside the building), occlusion culling won't be performed. To avoid such situation, enable the *[Back Face](../../../../objects/worlds/world_occluders/occluder_object/index.md#back_face)* parameter in the *World Occluder* section of the *Node* tab.


![](back_face.png)


![](back_face_off.png) ![](back_face_on.png)


### Using a Mesh-Based Occluder


The *[occluder mesh](../../../../objects/worlds/world_occluders/occluder_mesh/index.md)* is based on an arbitrary mesh that culls objects' surfaces, bounds of which aren't visible behind it. The occluder mesh is used together with the geometry that cannot be approximated with a box.


To create a mesh-based occluder, perform the following:

1. Prepare a low-poly mesh to be used for the occluder. > **Notice:** It isn't recommended to use the same detailed mesh that is used for the node that should occlude other objects: the mesh for the occluder should be as simple as possible to avoid performance loss. ![](high_poly_mesh.png) ![](low_poly_mesh.png)
2. In the Menu Bar, choose *Create -> Optimization -> Occluder Mesh* and specify the prepared mesh. > **Notice:** You can [load a new mesh](../../../../objects/worlds/world_occluders/occluder_mesh/index.md#load) for the occluder at any time.
3. Add the occluder as a child to the node that should occlude other objects.
4. In the *Common* section of the *Node* tab in the *Parameters* window, set the position of the occluder to the parent one. ![](set_to_parent.png)
5. Specify the *[Distance](../../../../objects/worlds/world_occluders/occluder_mesh/index.md#edit)* between the camera and the occluder, at which the occluder doesn't occlude anything and, therefore, should be disabled to avoid negative impact on the performance. ![](occluder_mesh_distance.png)


## Hardware Occlusion Queries


One more option to cull geometry that is not visible in the camera viewport is to use a **hardware occlusion query**. It allows skipping rendering of objects, the bounding boxes of which are covered by another solid geometry. As a result, the number of rendered polygons is reduced and the performance grows.


To run the hardware occlusion test for the scene before sending data to the GPU, toggle the *Rendering -> Occlusion Culling -> Occlusion Query* flag on in the Menu Bar.


> **Notice:** Culling will be performed for all objects with the *[Culled by Occlusion Query](../../../../editor2/node_parameters/transformation_common/index.md#query)* flag set in the *Node* tab of the *Parameters* window.


To run the hardware occlusion test, perform the following:


1. In the Menu Bar, toggle the *Rendering -> Occlusion Culling -> Occlusion Query* flag on to enable testing for the scene before sending data to the GPU. ![](occlusion_query.png)
2. For all objects, that should be culled, enable the *[Culled by Occlusion Query](../../../../editor2/node_parameters/transformation_common/index.md#query)* flag in the *Node* tab of the *Parameters* window. > **Notice:** Only nodes with this flag set are tested on the hardware occlusion culling. ![](culled_flag.png)


When culling is enabled for the object, an **occlusion query box** is rendered for it.


![](occlusion_query_box.png)

*Material balland its occlusion query box*


> **Notice:** To visualize such boxes, toggle the *Helpers -> Occlusion Queries* option on.


The occlusion query box coincides with the size of the object's bounding box. When this box is overlapped (i.e. it isn't in the camera viewport), it is highlighted **red**, which means the occlusion test is not passed and the mesh will not be drawn.


| ![](occlusion_query_test_0.png) | ![](occlusion_query_test_1.png) |
|---|---|
| *Occlusion query test passed* | *Occlusion query test failed, material ball isn't rendered* |


> **Notice:** Hardware occlusion queries should be used only for objects that use heavy shaders. Otherwise, performance will decrease instead of increasing. It is recommended to enable queries for water or objects with reflections.


You can check the effect of this technique by enabling the second wireframe mode to see all triangles in the scene. Type `render_show_triangles 2` in the console and check the way the occluded polygons act.


An example of using hardware occlusion queries is also available in the [Content Optimization](https://youtu.be/Iqsr3fEvnis?t=647) video tutorial.

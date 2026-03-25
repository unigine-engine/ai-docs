# Occluder Mesh


**Occluder Mesh** is an occluder which is based on an arbitrary mesh. *Occluder Mesh* is used to cull surfaces of objects whose bounding boxes are not visible behind it (see clarification below). Surfaces obscured by the *Occluder* are not sent to the GPU, thereby saving performance.


> **Warning:** Occluders are only **effective for ground-based viewer scenarios** where the camera always remains somewhere near the ground level and does not rise above the objects intended to be culled using occluders.


Occluders perform testing **entirely on the CPU side**, so there are no per-pixel depth tests or GPU occlusion queries for them. During fast occlusion testing, the algorithm creates a **simplified 2D rectangle enclosing the projection of the object's bounding box in screen space** (see the image below) and assigns a single depth value derived from the nearest point of the bounding box along the view direction to it. This rectangle is tested against the **Occluder Buffer**, which contains rough projections of all currently visible occluders rendered at a specific resolution ([controlled globally](../../../../editor2/settings/render_settings/occlusion_culling/index.md#occluders)). All the projections depend on the camera's field of view (FOV) and viewing angle. At certain angles objects that appear to have their surfaces obscured by the occluder may still be rendered because some part (or even a vertex) of the enclosing screen-space rectangle extends beyond the occluded area.


![](occluder_mesh_frame_test.gif)

*The object is culled when a 2D rectangle enclosing its bound (green) iscompletelycovered by the occluder.*


Culling accuracy can be improved by increasing the resolution of the *Occluder Buffer*, but keep in mind that **higher buffer resolution means increased rendering load** and can kill the profit from culling optimization.


> **Notice:** - If any part of the 2D rectangle enclosing the bound of the surface extends beyond the occluder, the surface will not be culled.
> - By default, shadows from the occluded objects remain visible. To disable shadows rendering, run the console command `render_occluders_shadows 1`.


### See also


- General information on *[Occluder](../../../../objects/worlds/world_occluders/index.md)*
- The *[WorldOccluderMesh](../../../../api/library/worlds/class.worldoccludermesh_cpp.md)* class to manage mesh occluders via API
- The sample `<UnigineSDK>/data/samples/worlds/occluder_01`


## Creating Occluder Mesh


Before adding *Occluder Mesh* to a scene, you should prepare a mesh, on which this *Occluder Mesh* will be based. Such mesh is created separately and should be as simple as possible: it should contain the minimum number of polygons.


When the mesh is prepared, you can add *Occluder Mesh* to the scene via UnigineEditor:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Optimization -> Occluder Mesh*. ![](create_occluder_mesh.png)
3. In the file dialog window, choose a mesh (`*.mesh`), on which the occluder will be based.
4. Place the *Occluder Mesh* in the world and [specify the required parameters for it](#edit).


> **Notice:** To display the [buffer](../../../../objects/worlds/world_occluders/index.md#occluder_buffer) that is used for occluders rendered in the viewport, pass 1 to the `render_show_occluder` console command.


### Example


For example, if you have a building that occludes some objects' surfaces, you should prepare a simplified mesh to be used as a base for the *Occluder Mesh* instead of using the detailed mesh.


| [![](mesh_sm.jpg)](mesh.jpg) | [![](occluder_mesh_sm.png)](occluder_mesh.png) |
|---|---|
| *Mesh that represents a building and contains a lot of details* | *Occluderthat is based on the simplified mesh and is rendered into a separate buffer with a low resolution* |


## Editing Occluder Mesh


In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of *Occluder Mesh*:


![](edit_occluder_mesh.png)


| **Distance** | Distance between the camera and the bounding box of the occluder, exceeding which the *Occluder Mesh* becomes disabled. For example, you should disable the occluder at a certain distance if it stops hiding the objects and their surfaces, in order to increase performance. By default, the inf value is used. |
|---|---|


### Loading a New Mesh


To load a new mesh on which *Occluder Mesh* will be based:


1. In the *World Occluder Mesh* section of the *Node* tab, press ![](occluder_mesh_load.png).
2. In the file dialog window that opens, choose the required mesh and press *OK*.


### Saving the Current Mesh


To save the current mesh on which the occluder is based:


1. In the *World Occluder Mesh* section of the *Node* tab, press ![](occluder_mesh_save.png).
2. In the file dialog window that opens, specify a name for the mesh and press *OK*.

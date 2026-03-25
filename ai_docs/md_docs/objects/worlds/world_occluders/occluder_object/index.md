# Occluder


**Occluder** is an invisible box-shaped primitive that is used to cull surfaces of objects whose bounding boxes are not visible behind it (see clarification below). Surfaces obscured by the *Occluder* are not sent to the GPU, thereby saving performance.


> **Warning:** Occluders are only **effective for ground-based viewer scenarios** where the camera always remains somewhere near the ground level and does not rise above the objects intended to be culled using occluders.


Occluders perform testing **entirely on the CPU side**, so there are no per-pixel depth tests or GPU occlusion queries for them. During fast occlusion testing, the algorithm creates a **simplified 2D rectangle enclosing the projection of the object's bounding box in screen space** (see the image below) and assigns a single depth value derived from the nearest point of the bounding box along the view direction to it. This rectangle is tested against the **Occluder Buffer**, which contains rough projections of all currently visible occluders rendered at a specific resolution ([controlled globally](../../../../editor2/settings/render_settings/occlusion_culling/index.md#occluders)). All the projections depend on the camera's field of view (FOV) and viewing angle. At certain angles objects that appear to have their surfaces obscured by the occluder may still be rendered because some part (or even a vertex) of the enclosing screen-space rectangle extends beyond the occluded area.


![](occluder_frame_test.gif)

*The object is culled when a 2D rectangle enclosing its bound (green) iscompletelycovered by the occluder.*


Culling accuracy can be improved by increasing the resolution of the *Occluder Buffer*, but keep in mind that **higher buffer resolution means increased rendering load** and can kill the profit from culiing optimization.


> **Notice:** By default, shadows from the occluded objects remain visible. To disable shadows rendering, run the console command `render_occluders_shadows 1`.


Depending on the *[Back Face](#back_face)* parameter value, the front or back faces of *Occluder* are used to cull surfaces. The **front faces** of *Occluder* are the sides of the *Occluder* that face the camera. The **back faces** of *Occluder* are the sides that are behind the front faces.


Schematically, the *Occluder* faces can be shown as follows:


| ![](front_faces_sm.png) | ![](back_faces_sm.png) |
|---|---|
| *Front faces ofOccluder* | *Back faces ofOccluder* |


> **Notice:** If any part of the 2D rectangle enclosing the bound of the surface extends beyond the occluder, the surface will not be culled.


### See also


- General information on *[Occluder](../../../../objects/worlds/world_occluders/index.md)*
- The *[WorldOccluder](../../../../api/library/worlds/class.worldoccluder_cpp.md)* class to manage *Occluder* via API
- The sample `<UnigineSDK>/data/samples/worlds/occluder_00`


## Creating Occluder


To create *Occluder* via UnigineEditor:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Optimization -> Occluder*. ![](create_occluder.png)
3. Place the *Occluder* in the world and [specify the required parameters for it](#edit).


> **Notice:** To display the [buffer](../../../../objects/worlds/world_occluders/index.md#occluder_buffer) that is used for *Occluder* rendered in the viewport, pass 1 to the `render_show_occluder` console command.


## Editing Occluder


On the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of *Occluder*:


![](edit_occluder.png)


| Edit Size | Toggles the editing mode for the *Occluder* node on and off. When enabled, the *Occluder* box sides that can be resized are highlighted with the colored rectangles. To change the size of a side, drag the corresponding rectangle. ![](editing_mode.jpg) |  |  |  |  |
|---|---|---|---|---|---|
| Back Face | Indicates whether the back faces of the *Occluder* box are used instead of front faces to occlude objects. If unchecked, the front faces will be used. \| [![](back_unchecked_sm.png)](back_unchecked.png) \| [![](back_checked_sm.png)](back_checked.png) \| \|---\|---\| \| *Back Faceis unchecked* \| *Back Faceis checked* \| | [![](back_unchecked_sm.png)](back_unchecked.png) | [![](back_checked_sm.png)](back_checked.png) | *Back Faceis unchecked* | *Back Faceis checked* |
| [![](back_unchecked_sm.png)](back_unchecked.png) | [![](back_checked_sm.png)](back_checked.png) |  |  |  |  |
| *Back Faceis unchecked* | *Back Faceis checked* |  |  |  |  |
| Size | Size of *Occluder* along the axes. |  |  |  |  |
| Distance | Distance between the camera and the bounding box of *Occluder*, at which the *Occluder* becomes disabled (it isn't processed by the CPU, hence it isn't rendered). For example, you should disable *Occluder* at a certain distance if it stops hiding the objects and their surfaces, in order to increase performance. By default, the parameter value is set to inf. |  |  |  |  |

# Setting Up Cameras


The main camera functions are available via the *Camera* panel of the [Editor Viewport](../../editor2/interface/index.md#viewports): you can switch between cameras, add new cameras to the current world, open the [Camera Settings](#camera_settings) window, and toggle the [flashlight](../../editor2/navigation/index.md#camera_utilities) attached to the camera.


![](open_camera_settings.png)

*Camera Panel*


By default, there are 2 cameras in the world:


- *Engine Camera* created from the world script. The view from this camera is rendered in a separate *Engine Viewport*, and you cannot change its settings via UnigineEditor. This camera represents the current player. *Engine Camera* can be changed via the [script](../../api/library/engine/class.game_cpp.md#setPlayer_Player_void).
- *Editor Camera* created from the editor script. This is the default camera in UnigineEditor. > **Notice:** Both *Engine Camera* and *Editor Camera* always exist in the world.


You can also [add new cameras](#add_custom_camera). Such cameras can be used as watchpoints in the world: you can [position](#position_camera) cameras at different points of the world and then switch between them via the *Camera panel* of the [Editor Viewport](../../editor2/interface/index.md#viewports), when necessary.


> **Notice:** The number of cameras is **unlimited**.


## Adding a New Camera


To add a new camera to the current world:


1. Change the position and orientation of the current camera by using the [navigation controls](../../editor2/navigation/index.md#move_camera). > **Notice:** Position, orientation, and settings of the current camera are copied for the new camera.
2. On the *Camera* panel, click ![](add.png). A new camera will be added to the list of the available cameras with the *PlayerDummy* name. ![](new_camera.png) *A new available camera* At the same time, the camera will be added to the world as a *[PlayerDummy](../../objects/players/dummy/index.md)* node. ![](new_camera_node.png) *A newPlayerDummynode*
3. [Change the default camera settings](#setup_camera) to the required ones.


## Positioning the Camera


To set a new position and orientation for the camera, place the camera to the required position and adjust its orientation as necessary by using the [navigation controls](../../editor2/navigation/index.md).


> **Notice:** All camera movements are immediately saved. Consider that when positioning cameras.


You can also position the camera by selecting it in the *World Hierarchy* window and directly changing its transformation via the *[Parameters](../../editor2/node_parameters/transformation_common/index.md#transformation_params)* window.


## Setting Up the Camera


As settings of a new camera are simply copied from the current camera, you may need to change them via the *Camera Settings* window.


To open the *Camera Settings* window, choose the required camera and click ![](camera_settings_icon.png) on the *Camera* panel.


### Camera Settings


The list of available camera settings depends on the camera mode:


- *Perspective mode*
- *Orthographic mode*


Moreover, the Editor Camera has [additional settings](#editor_camera_settings).


| ![](camera_settings.png) | ![](camera_ortho_settings.png) |
|---|---|
| *Perspective Camera Settings* | *Orthographic Camera Settings* |


> **Notice:** Settings of the perspective camera, in turn, depend on the **[Mode](#fov_mode)** of the camera field of view: parameters defining the camera's viewing frustum differ.


| Option | Description |  |  |  |  |
|---|---|---|---|---|---|
| **Name** | Name of the current camera. If you change the camera name, the name of the node (*PlayerDummy*) will be also changed. |  |  |  |  |
| **Projection mode** | Camera projection mode. The available values are: - **[Perspective](../../principles/world_management/index.md#camera_perspective)** - **[Orthographic](../../principles/world_management/index.md#camera_orthographic)** \| ![](perspective_mode.png) \| ![](orthographic_mode.png) \| \|---\|---\| \| *Perspective mode* \| *Orthographic mode* \| | ![](perspective_mode.png) | ![](orthographic_mode.png) | *Perspective mode* | *Orthographic mode* |
| ![](perspective_mode.png) | ![](orthographic_mode.png) |  |  |  |  |
| *Perspective mode* | *Orthographic mode* |  |  |  |  |
| **Height** | Height of the viewing volume which is [represented in the form of a rectangular parallelepiped](../../principles/world_management/index.md#camera_orthographic). The width of the viewing volume will be equal to its height. > **Notice:** The option is available only in the orthographic camera mode. |  |  |  |  |
| **Field of View** *(available only for the perspective mode)* |  |  |  |  |  |
| **Mode** | FOV mode. The available values are: - **Vertical** FOV is used for the standard camera. In this case, the FOV is set in degrees. - **Physically-Based Camera** is used for the physically-based camera with the horizontal FOV. In this case, the FOV is calculated depending on the [film gate](#film_gate) and [focal length](#focal_length) of the camera according to the formula: **FOV = 2 * atan(film_gate / (2 * focal_length)) * UNIGINE_RAD2DEG** \| ![](fov_vertical.png) \| ![](fov_physical.png) \| \|---\|---\| \| *Vertical FOV Settings* \| *Physically-Based Camera Settings* \| | ![](fov_vertical.png) | ![](fov_physical.png) | *Vertical FOV Settings* | *Physically-Based Camera Settings* |
| ![](fov_vertical.png) | ![](fov_physical.png) |  |  |  |  |
| *Vertical FOV Settings* | *Physically-Based Camera Settings* |  |  |  |  |
| **Degrees** | Camera's vertical field of view in degrees. This is the area that can be seen in the viewport (how many degrees the camera covers). > **Notice:** Available for the camera with the [vertical FOV](#fov_mode) only. |  |  |  |  |
| **Focal Length** | The focal length of the physically-based camera lens. > **Notice:** Available for the [physically-based](#fov_mode) camera only. |  |  |  |  |
| **Film Gate** | The film gate for the physically-based camera with horizontal FOV. > **Notice:** Available for the [physically-based](#fov_mode) camera only. |  |  |  |  |
| **Clipping Planes** |  |  |  |  |  |
| **Near** | Distance to the camera near clipping plane. |  |  |  |  |
| **Far** | Distance to the camera far clipping plane. > **Notice:** An extremely big difference between the Near and Far Clipping Planes can cause black screen. Therefore, if the required *Far Clipping Plane* value is outside the range, adjust the *Near Clipping* value proportionately. |  |  |  |  |
| **Masks** |  |  |  |  |  |
| **Viewport** | A *[Viewport](../../principles/bit_masking/index.md#viewport)* bit mask for the camera that enables to selectively display objects, decals and lights in the camera viewport. If at least one bit matches, the object, decal or light will be rendered. The mask can be edited. |  |  |  |  |
| **Reflection Viewport** | A *[reflection viewport](../../principles/bit_masking/index.md#reflection_mask)* bit mask for the reflection camera that enables selective display of reflections from objects. The mask can be edited. |  |  |  |  |
| **Reverberation** | A [reverberation mask](../../principles/bit_masking/index.md#reverb_mask) for the camera determines what reverberation zones can be heard. At least one bit of this mask should match the reverb mask of the sound source and the reverb mask of the reverberation zone. The mask can be edited. |  |  |  |  |
| **Sound** | A [sound mask](../../principles/bit_masking/index.md#source_mask) for the camera that what sound channels can be heard. If at least one bit matches the sound source mask, the sound can be heard. Each bit of the source mask specifies a sound channel. The mask can be edited. |  |  |  |  |


### Editor Camera Settings


In addition to the settings described above, the *Editor Camera* has some specific settings that allow you to change its transformation and then save it as the default one to the world meta file along with the other settings.


> **Notice:** If the world meta file doesn't store Editor Camera transformation, the transformation of the [main](../../objects/players/index.md#main_player) or any other [user camera](#add_custom_camera) will be applied by default.


![](editor_camera_settings.png)


| Option | Description |
|---|---|
| **Position** | Position of the Editor Camera. |
| **Rotation** | Orientation of the Editor Camera. |
| **Save Editor Camera Parameters to World Metadata** | Forces to save the Editor Camera settings to the `.world.meta` file. The Editor Camera settings of each [Editor Viewport](../../editor2/interface/index.md#viewports) should be saved separately. > **Notice:** The saved Editor Camera transformation will be used as the default one. So the Editor Camera will be configured according to it when a new user will open the world for the first time. |


## Rendering the Camera Viewport in a Separate Window


The view from each camera can be rendered into a separate *[Editor Viewport](../../editor2/interface/index.md#viewports)* window.


To render a view from a camera to a separate viewport, perform the following steps:


1. Add a new *Editor Viewport* window, choose *Windows -> Add Editor Viewport*. ![](viewport_window_open.png) A new viewport named *Editor Viewport 2* will open. ![](camera_viewport.png) *New Editor Viewport*
2. Select the required camera to render the view from in the drop-down list of the *Camera panel*. ![](select_camera.png) > **Notice:** You can change the camera at any time, if necessary.


The total number of viewports that can be opened simultaneously is not limited. Each new viewport window has the same functionality as the main *[Editor Viewport](../../editor2/interface/index.md#viewports)* window.


> **Notice:** Each new viewport requires to render the scene one more time, which may lead to a performance drop. Don't forget to [hide](#viewport_show_hide) a viewport when it is not used, or [remove](#viewport_remove) it, when it is no longer needed.


You can use several Editor Viewports to operate with several nodes located far away from each other, or to view different orthographic projections of the scene (Top, Front, and Side views).


### Hiding and Showing Viewports


You can hide the *Editor Viewport* window and show the one that is hidden. To toggle the *Editor Viewport* window, select its name in the *Windows* menu and choose **Show** or **Hide**.


| ![](viewport_hide.png) | ![](viewport_show.png) |
|---|---|
| *Hide the Editor Viewport 1* | *Show the Editor Viewport 2* |


### Removing Viewports


You can remove an *Editor Viewport* window when you no longer need one. To do so, select the name of the *Editor Viewport* window, that you want to remove in the *Windows* menu and choose **Remove**.


![](viewport_remove.png)

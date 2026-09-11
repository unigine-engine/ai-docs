# Scene Navigation


In UnigineEditor, there are controls that are used to move in the scene and control the camera behavior. All the available controls can be found in the *Controls* section of the *[Settings](../../editor2/settings/index.md)* window.


The camera can be moved freely in the scene or relative to a target. In terms of UnigineEditor, the target is a point relative to which the camera is positioned. You can set the target by [focusing](#set_focus) the camera on a selected node or a group of nodes.


> **Notice:** If the camera does not focus on a node, the position of the target coincides with the camera position.


Whether the target is set or not, you can freely navigate in the scene: [move](#move_camera) the camera, [change direction](#rotate) of the camera (horizontally and vertically), [track](#track) the camera or [zoom](#zoom_cam) it in and out.


If the camera is [focused](#set_focus) on a node (in other words � positioned relative to the target), you can also [orbit](#orbit) the camera about the target and [zoom](#dolly) it towards or away from the target by using the dolly zoom.


In addition to the commonly used terms (for example, Move left, Move up and so on), the following terms are used in UnigineEditor:


- Change direction means changing the yaw/pitch angle to rotate the camera around its vertical/horizontal axis respectively.
- Track (Crab) means tracking the camera in the plane which is perpendicular to the view direction.
- Orbit means tumbling around the target.
- Zoom (Dolly) means zooming the camera towards or away from the target so that the camera cannot continue to zoom in when it reaches the target.


The following schemes demonstrate the main navigation controls that are used in UnigineEditor:


| ![](scene_navigation_free.png) | ![](scene_navigation_targeted.png) |
|---|---|
| *Navigation controls used to freely move the camera in the scene* | *Additional navigation controls used to move the camera relative to the target* |


## Focusing the Camera


To set and reset the camera focus, you can use the following default controls:


| Control | Description |
|---|---|
| **F** | Focus the camera on the selected nodes. |
| **G** | Reset the camera focus. |


When you focus the camera on the group of nodes, you should set the pivot point (see [*Pivot Point Toggle*](../../editor2/select_position_nodes/index.md#pivot_point) for details) on the main menu:


- If the pivot point is set to *Center* (![](center.png) is set), the target will be set to the center of selection. ![](center_toggled.png) *TheCenterbutton is active*
- If the pivot point is set to *Pivot* (![](pivot.png) is set), the target will be set to the last selected node. ![](pivot_toggled.png) *ThePivotbutton is active;Node 2is the last selected node*


If you focus the camera on the node (or the group of nodes), the [target](#target) position will coincide with the center of the node (or the group of nodes). Therefore, you will be able to [orbit](#orbit_def) the camera around this target and [zoom (dolly)](#dolly_def) the camera towards or away from this target.


## Moving the Camera


To move in the scene, you can use the following default controls:


| Control | Description |
|---|---|
| **RIGHT-CLICK + Drag** | Change the camera direction. - Press and hold this key and drag the mouse left or right to change the yaw angle. In this case, the camera will rotate around its vertical axis. - Press and hold this key and drag the mouse up or down to change the pitch angle. In this case, the camera will rotate around its horizontal axis. |
| **RIGHT-CLICK + W** | Move the camera forward. |
| **RIGHT-CLICK + S** | Move the camera backward. |
| **RIGHT-CLICK + A** | Move the camera left. |
| **RIGHT-CLICK + D** | Move the camera right. |
| **RIGHT-CLICK + Q** | Move the camera down. |
| **RIGHT-CLICK + E** | Move the camera up. |
| **Alt + MIDDLE CLICK + Drag** | Track (crab) the camera in the plane which is perpendicular to the view direction. |
| **Alt + LEFT CLICK + Drag** | Orbit the camera about the target. |


Also you can change the camera position by setting its coordinates via the *Navigation Panel* of the [Editor Viewport](../../editor2/interface/index.md#viewports) as follows:


![](camera_position.png)


## Zooming the Camera


To zoom the camera, you can use the following default controls:


| Control | Description |
|---|---|
| **WHEEL UP** | Zoom the camera in. > **Notice:** If the camera reaches the [target](#target) and continues zooming, the target will be moved with the camera. |
| **WHEEL DOWN** | Zoom the camera out. > **Notice:** When zooming out, the position of the [target](#target) remains the same. |
| **Alt + RIGHT-CLICK + Drag** | Zoom (dolly) the camera toward or away from the target by using the dolly zoom. |


## Changing the Camera Speed


There are 3 modes of the camera speed. You can switch between them via the *Navigation Panel*. Also you can change the speed value set for one of the speed modes. For example, you can change the value of the 1st speed node as follows:


![](change_speed.png)


In addition, the following controls can be used to change the camera speed:


| Control | Description |
|---|---|
| **Shift** | Speed up the camera movement. Press and hold this key when [moving](#move_camera) the camera. |
| **1** / **2** / **3** | Enable the 1st, the 2nd or the 3rd mode of the camera speed. |


## Camera Utilities


![](flashlight.png)

*Flashlight Settings*


| Control | Description |
|---|---|
| **L** | Toggle a flashlight attached to the camera. |


### Flashlight Settings


| Color | A flashlight color. |
|---|---|
| Intensity | A flashlight color intensity. The higher the value, the brighter the light is. |
| Attenuation | A flashlight attenuation power. It simulates light intensity gradual fading. |
| Radius | A radius of the area illuminated by the flashlight. |
| Field of View | A field of view of the flashlight. This parameter defines the angle of the light clipping in range from 10 to 160 degrees. |


## Using Several Cameras


In a large virtual world, you can use cameras as watchpoints for fast navigation: you can add and position any number of the cameras in different points of the world, save their positions and then switch between them via the *Camera panel* of the [Editor Viewport](../../editor2/interface/index.md#viewports) when it is necessary.


To create such watchpoint:


1. [Add a new camera](../../editor2/camera_settings/index.md#add_custom_camera) to the world.
2. [Position](../../editor2/camera_settings/index.md#position_camera) the camera.


The following pictures show 2 cameras positioned in different points in the world:


| ![](camera_0_panel.png) | ![](camera_0.png) |
|---|---|
| *camera_0camera used as watch-point* | *camera_0camera view* |
| ![](camera_1_panel.png) | ![](camera_1.png) |
| *camera_1camera used as watch-point* | *camera_1camera view* |


When you switch to one of the saved cameras, you can freely move it in the world: changes in its position and orientation won't be saved. To return to the saved position and orientation of the camera, switch to another camera and then choose the required camera again.


## Video Tutorial: The Scene Viewport

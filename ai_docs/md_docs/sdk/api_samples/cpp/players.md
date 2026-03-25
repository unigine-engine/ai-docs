# Player Controllers

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Camera Zoom

This sample demonstrates a zoom and camera focus system that allows the user to inspect predefined targets in the scene and adjust the zoom level. Three info boards are placed throughout the scene, each with an in-world GUI panel showing its distance from the player and its dimensions. These panels update automatically in real time based on the player's position.


The user can select any target using dedicated UI buttons, prompting the camera to focus on the selected object.


Zoom is controlled via a slider that adjusts the camera's field of view. As the FOV changes, related parameters such as mouse sensitivity and render distance scaling are adjusted as well to maintain a consistent experience. A reset button restores all values to default.


This setup is useful for scenarios that require object-focused viewing, such as inspection tools, scene walkthroughs, or any case where adjustable zoom and camera focus help users better understand or explore the scene.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/player_controllers/camera_zoom*
## First-Person Controller

This sample demonstrates a first-person character controller implemented as a component attached to a *PlayerDummy*.


The controller uses [Shape-Surface](../../../principles/physics/collision/index.md#collision_types) collisions to detect ground, walls, and slopes, and applies slope-aware movement to ensure stable walking on inclined geometry. It supports walking, running, jumping, air movement, smooth crouching, and camera rotation with vertical limits. Auto-stepping allows the character to traverse small obstacles, and [Shape-Shape](../../../principles/physics/collision/index.md#collision_types) collisions are used to interact with physical objects by applying impulses.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/player_controllers/first_person_controller*
## Observer Controller

This sample replicates the free camera used in the UnigineEditor. The camera offers the following key features:


- **Fly-Through Mode** Freely move the camera in all directions using keyboard and mouse controls.
- **Focus on Objects** Center the camera on any selected object and adjust distance automatically.
- **Zoom & Pan** Zoom in and out, and pan while preserving view direction.
- **Speed Control Menu** Switch between predefined movement speeds (1-3) or adjust custom speed values.
- **Position Management** Set or teleport the camera to specific world coordinates through the menu.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/player_controllers/observer_controller*
## Orbit Camera Controller

This sample demonstrates an orbital camera rotating around a target.

The *CameraOrbitSample* component enables orbit-style camera movement around a target object using a *[PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md)* node and the *CameraControls* component to process configurable input controls for camera movement and zoom.


The camera behavior can be customized using the exposed parameters: *Angular Speed, Zoom Speed, Min/Max Distance*, and *Min/Max Vertical Angle*. The *Target* parameter defines the object the camera orbits around.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/player_controllers/orbit_camera_controller*
## Persecutor Controller

This sample demonstrates a custom third-person camera built using a *[PlayerDummy](../../../objects/players/dummy/index.md)* node, replicating and extending the behavior of UNIGINE's built-in *[PlayerPersecutor](../../../objects/players/persecutor/index.md)* object.

The component calculates camera position and orientation based on user input (if enabled), target movement, and optional collision detection. The anchor point defines the offset relative to the target, while minimum and maximum angles and distances constrain camera movement. If collision is enabled, the camera uses a collision shape to detect and avoid geometry between itself and the target, adjusting its position accordingly. The camera supports both free and fixed rotation modes. When rotation is fixed, the camera maintains a stable angle relative to the target. Otherwise, it can rotate in response to mouse input.


This setup is useful for third-person gameplay, chase cameras, or situations where built-in logic isn't flexible enough and a fully customizable solution is needed.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/player_controllers/persecutor_controller*
## Spectator Controller

This sample implements a first-person **[Spectator camera](../../../objects/players/spectator/index.md)** controller with configurable movement and physical collision detection using the **[Sphere collision shape](../../../principles/physics/shapes/index.md#sphere)**, assigned to respond to collisions with geometry (e.g. with terrain) in the world.


Movement parameters such as speed, sprint acceleration, turning rate, and mouse sensitivity can be adjusted in real-time using the sliders in the *Parameters* section.


**Use Cases:**


- Building custom camera tools with physical awareness for scene editing or testing purposes.
- First-person 3D scenes navigation and exploring while preserving configurable interaction with the geometry.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/player_controllers/spectator_controller*
## Top-Down Controller

This sample demonstrates how to set up and control a top-down camera controller for real-time strategy or tactics-style gameplay. It implements core features typical for such games, including camera movement, zooming, rotation, edge scrolling, unit selection, and focus tracking. The implementation is based on the *PlayerDummy* node.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/player_controllers/top_down_controller*

## Two-Point Perspective

This sample shows how to simulate a two-point perspective projection using a lens shift technique implemented via a secondary *Dummy Player*. When enabled, the sample dynamically adjusts the projection matrix of a dummy camera to visually align vertical lines while preserving the viewing direction.


The effect is achieved by adjusting the projection matrix of a *[PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md)* instance according to the pitch angle of the active camera. During the rendering phase, the *Dummy Player* temporarily replaces the main camera to apply the modified view.


This approach can be used for architectural visualization or stylized camera effects where a more orthographic-like vertical perspective is desired.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/player_controllers/two_point_perspective*

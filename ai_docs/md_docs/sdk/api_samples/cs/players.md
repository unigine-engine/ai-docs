# Player Controllers

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## CAD-Style Camera Panning

This sample demonstrates a camera moving parallel to the screen plane using the *CameraPanning.cs* component assigned to a *PlayerDummy* node.

The *CameraPanning.cs* component implements a free panning camera that allows movement along the view plane, rotation, and zoom based on mouse input.


The camera position can be adjusted by dragging the scene, and rotation is enabled by holding the right mouse button. Zooming is controlled with the mouse wheel. The responsiveness of movement and rotation is configurable via the *Default Linear Speed, Mouse Sensitivity*, and *Mouse Wheel Sensitivity* parameters in the component properties.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/cad_style_camera_panning*
## Camera First Person

This sample demonstrates a first-person spectator-style camera with free movement.

The *CameraSpectator.cs* component provides free-flight first-person controls by modifying the position and orientation of a *[PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md)* node in real time. The movement and rotation are handled via the *CameraControls.cs* component that defines directional input.


The camera moves in six directions (forward, backward, left, right, up, down) and rotates using pitch and yaw angles. The *Speed* and *Angular Speed* parameters can be adjusted in the component properties to control the camera's movement and rotation responsiveness.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/camera_first_person*
## Camera Zoom

This sample demonstrates a zoom and camera focus system that allows the user to inspect predefined targets in the scene and adjust the zoom level. Three info boards are placed throughout the scene, each with an in-world GUI panel showing its distance from the player and its dimensions. These panels update automatically in real time based on the player's position.


The user can select any target using dedicated UI buttons, prompting the camera to focus on the selected object.


Zoom is controlled via a slider that adjusts the camera's field of view. As the FOV changes, related parameters such as mouse sensitivity and render distance scaling are adjusted as well to maintain a consistent experience. A reset button restores all values to default.


This setup is useful for scenarios that require object-focused viewing, such as inspection tools, scene walkthroughs, or any case where adjustable zoom and camera focus help users better understand or explore the scene.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/camera_zoom*
## First-Person Controller

This sample demonstrates a first-person character controller implemented as a component attached to a *PlayerDummy*.


The controller uses [Shape-Surface](../../../principles/physics/collision/index.md#collision_types) collisions to detect ground, walls, and slopes, and applies slope-aware movement to ensure stable walking on inclined geometry. It supports walking, running, jumping, air movement, smooth crouching, and camera rotation with vertical limits. Auto-stepping allows the character to traverse small obstacles, and [Shape-Shape](../../../principles/physics/collision/index.md#collision_types) collisions are used to interact with physical objects by applying impulses.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/first_person_controller*
## Observer Controller

This sample replicates the free camera used in the UnigineEditor. The camera offers the following key features:


- **Fly-Through Mode** Freely move the camera in all directions using keyboard and mouse controls.
- **Focus on Objects** Center the camera on any selected object and adjust distance automatically.
- **Zoom & Pan** Zoom in and out, and pan while preserving view direction.
- **Speed Control Menu** Switch between predefined movement speeds (1-3) or adjust custom speed values.
- **Position Management** Set or teleport the camera to specific world coordinates through the menu.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/observer_controller*
## Orbit Camera Controller

This sample demonstrates an orbital camera rotating around a target.


The *CameraOrbit.cs* component enables orbit-style camera movement around a target object using a *[PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md)* node. Input is handled via the *CameraControls.cs* component, which provides configurable input controls for camera movement and zoom.


The camera behavior can be customized using the exposed parameters: *Angular Speed, Zoom Speed, Min/Max Distance*, and *Min/Max Vertical Angle*. The *Target* field defines the object the camera orbits around.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/orbit_camera_controller*
## Persecutor Controller

This sample demonstrates a camera following a moving target.


The *CameraPersecutor.cs* component implements a third-person follow camera that smoothly tracks a moving target defined in the *Target* field. The camera adjusts its distance, pitch, and yaw to maintain the desired view of the target, using the *[PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md)* node as its base.


Input is handled via the *CameraControls.cs* component and allows orbiting around the target as well as zooming in and out. The behavior is configurable through parameters such as *Angular Speed, Zoom Speed, Min/Max Distance, Min/Max Vertical Angle*, and the *Use Fixed Angles* toggle. The *Target* field can be manually assigned and defines the object the camera will follow.


The target movement is defined by the *CameraPersecutorTarget.cs* component, which moves the object along a circular path over time to demonstrate dynamic tracking.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/persecutor_controller*
## Spectator Controller

This sample implements a first-person **[Spectator camera](../../../objects/players/spectator/index.md)** controller with configurable movement and physical collision detection using the **[Sphere collision shape](../../../principles/physics/shapes/index.md#sphere)**, assigned to respond to collisions with geometry (e.g. with terrain) in the world.


Movement parameters such as speed, sprint acceleration, turning rate, and mouse sensitivity can be adjusted in real-time using the sliders in the *Parameters* section.


**Use Cases:**


- Building custom camera tools with physical awareness for scene editing or testing purposes.
- First-person 3D scenes navigation and exploring while preserving configurable interaction with the geometry.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/spectator_controller*
## Top-Down Controller

This sample demonstrates how to set up and control a top-down camera controller for real-time strategy or tactics-style gameplay. It implements core features typical for such games, including camera movement, zooming, rotation, edge scrolling, unit selection, and focus tracking.

The logic is implemented across four components: **CameraTopDown**, **CameraSelection, CameraUnitSelection**, and **CameraUnitPathControl**:


- The camera controls are implemented in the **CameraTopDown** component, which handles moving, adjusting zoom levels, and interpreting user input for panning and rotating the view. The camera also supports edge scrolling - when the mouse cursor moves near the edge of the screen, the camera starts moving in that direction. When one or more units are selected, the camera can optionally shift focus to the selection and follow it continuously while a key is held.
- Selection logic is managed by the **CameraSelection** component. It enables rectangular selection of multiple units using a screen-space box and calculates the combined bounding sphere of all selected objects for proper camera focusing.
- The **CameraUnitSelection** component is responsible for visual feedback during selection. It highlights selected units by rendering a visual circle beneath them.
- One of the units in the scene includes the **CameraUnitPathControl** component, which drives its movement along a predefined path that includes multiple waypoints. The unit traverses the path in a loop, demonstrating how moving elements can be integrated into a top-down control system.


This setup provides a flexible base for implementing top-down camera control and unit interaction, useful for strategy games, tactical simulations, or scene overview tools.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/player_controllers/top_down_controller*

# Classes and Components Overview (CPP)


When you first open the VR Template project and see dozens of classes, it can feel a bit overwhelming. Let's walk through the main parts so you know where everything lives and how the pieces fit together.


![VR Template Structure (C++)](../../../learn/13_vr_app/vr_layer_cpp_structure_with_captions.png)


## VRPlayer Class


This is the base class for all players - it defines baseline controls, common player operations, and event management.


> **Notice:** You can check out baseline controls for VR Controllers [here](../../../vr_development/vr_input_cpp.md).


Two player types inherit from *[VRPlayer](../../../api/modules/vr/components/players/class.vrplayer.md)*:


| [VRPlayerPC](../../../api/modules/vr/components/players/class.vrplayerpc.md) | A player with standard PC input (keyboard + mouse or Xbox360 controller) for VR emulation - handy for testing without a headset. |
|---|---|
| [VRPlayerVR](../../../api/modules/vr/components/players/class.vrplayervr.md) | The base class for all VR devices. It handles motion controllers, input tracking, teleportation, haptics, and object interaction - everything shared between controller-based and hand-tracking modes. |


Unlike the PC player (driven by a *[PlayerActor](../../../objects/players/actor/index.md)*), VRPlayerVR has its own physics-based body and movement system:


| [VRPlayerMotor](../../../api/modules/vr/components/players/class.vrplayermotor.md) | Handles physical movement and collision - locomotion, crouching, jumping, stepping over obstacles, and riding moving platforms. |
|---|---|


## Controls-Related Classes


These classes handle input and interaction through VR controllers.


> **Notice:** PC controls are implemented separately in [VRPlayerPC](#class_vrplayerpc).


| [VRController](../../../api/modules/vr/components/players/class.vrcontroller.md) | The base for all VR input - both controllers and hand tracking. It defines the common logic for grabbing, interaction states, and input processing. |
|---|---|


At runtime, the system picks the right controller automatically depending on the VR backend (OpenVR, OpenXR, or Varjo) and whether hand tracking is available:


| [VRHandController](../../../api/modules/vr/components/players/class.vrhandcontroller.md) | Input via physical controllers - button mapping, haptics, teleportation, object interaction, and controller model rendering. |
|---|---|
| [VRHandTracking](../../../api/modules/vr/components/players/class.vrhandtracking.md) | Input via hand tracking - gesture recognition, hand pose updates, and finger-based interaction. |


### Hand Tracking


Two specialized components extend hand tracking for specific devices (only one is active at a time):


| [VRHandTrackingControllerOpenXR](../../../api/modules/vr/components/players/class.vrhandtrackingcontrolleropenxr.md) | Uses OpenXR's built-in hand tracking API. Processes joint data to detect pinch and grab gestures for natural interaction without controllers. |
|---|---|
| [VRHandTrackingControllerUltraleap](../../../api/modules/vr/components/players/class.vrhandtrackingcontrollerultraleap.md) | Available with the Varjo backend (*-vr_app varjo*) when the *[Ultraleap](../../../code/plugins/ultraleap/index_cpp.md)* plugin is loaded. Integrates directly with the Ultraleap SDK for detailed skeletal tracking. |


To animate hand models, two corresponding mappers are used:


| [VRMeshSkinnedHandMapper](../../../api/modules/vr/components/players/class.vrmeshskinnedhandmapper.md) | Maps [*OpenXR* joint data](../../../vr_development/vr_hand_tracking.md#hand_hierarchy) to skinned hand meshes. |
|---|---|
| [UltraleapMeshSkinnedHandMapper](../../../api/modules/vr/components/players/class.ultraleapmeshskinnedhandmapper.md) | Applies [*Ultraleap* skeletal data](../../../code/plugins/ultraleap/index_cpp.md#bones) to the mesh. |


For more details, see *[Hand Tracking](../../../vr_development/vr_hand_tracking.md)*.


## VRPlayerSpawner Class


This class figures out what VR hardware is available and spawns the right player automatically:

- HMD connected -> **[VRPlayerVR](#class_vrplayervr)** with full VR interaction.
- Varjo + *[Ultraleap](../../../code/plugins/ultraleap/index_cpp.md)* plugin -> adds **[VRHandTrackingControllerUltraleap](#class_vrhandtrackingcontrollerultraleap)** for external hand tracking.
- OpenXR hand tracking available -> adds **[VRHandTrackingControllerOpenXR](#class_vrhandtrackingcontrolleropenxr)**.
- No VR device -> **[VRPlayerPC](#class_vrplayerpc)** for desktop fallback.


## Teleportation System


Teleportation lets players relocate by projecting a visible trajectory and selecting a valid destination.


| [PlayerTeleporter](../../../api/modules/vr/components/players/class.playerteleporter.md) | The core teleportation logic - ray visualization, intersection testing, allowed/forbidden area detection, and mask-based validation. |
|---|---|


Depending on the active input system, teleportation is automatically handled by the appropriate implementation:


| [PlayerHandControllerTeleporter](../../../api/modules/vr/components/players/class.playerhandcontrollerteleporter.md) | Teleportation via physical controllers - pull the right stick back to aim, release to teleport. |
|---|---|
| [PlayerHandTrackingTeleporter](../../../api/modules/vr/components/players/class.playerhandtrackingteleporter.md) | Teleportation via hand tracking - hold your right wrist to toggle aiming, open your hand to confirm. |


## Interaction-Related Classes


**[VRInteractable](../../../api/modules/vr/components/class.vrinteractable.md)** is the base class for everything you can interact with. It defines what a user can do with an object - grab it, use it, throw it. You can also [create your own interactable types](../../../vr_development/vr_template/vr_template_new_interactable/index_cpp.md).


The following classes inherit from *VRInteractable*:


| [ObjMovable](../../../api/modules/vr/components/objects/class.objmovable.md) | Objects you can grab, hold, and throw - a ball, a gun, anything you can pick up and drop. |
|---|---|
| [ObjHandle](../../../api/modules/vr/components/objects/class.objhandle.md) | Objects you can turn or move while holding - handles, levers, valves. |
| [ObjHandleTranslatable](../../../api/modules/vr/components/objects/class.objecthandletranslatable.md) | Handles that slide along a limited linear path. Supports toggle animation and sound feedback. |
| [ObjHandleRotatable](../../../api/modules/vr/components/objects/class.objecthandlerotatable.md) | Handles that rotate around a specified axis. Otherwise similar to ObjHandleTranslatable. |
| [ObjSwitch](../../../api/modules/vr/components/objects/class.objswitch.md) | Buttons and on-off switches (including rotary ones) - toggled by grabbing. |
| [ObjLaserPointer](../../../api/templates/template_vr/objects/class.objlaserpointer.md) | Casts a laser ray from the object. > **Notice:** The laser pointer in the demo has both **ObjMovable** and **ObjLaserPointer** attached. |
| [ObjGun](../../../api/templates/template_vr/objects/class.objgun.md) | A firearm you can grab, hold, and shoot. Handles shooting logic, sound/visual effects, bullet decals, and integrates **ObjGunSlide** for the weapon's slide animation. |
| [VRPluggable](../../../api/modules/vr/components/objects/class.vrpluggable.md) | An object that can be plugged into a socket. When released near a matching **VRSocketObject**, it auto-attaches. |
| [NodeSwitchEnableByGrab](../../../api/templates/template_vr/global/class.nodeswitchenablebygrab.md) | Toggles specified nodes on/off when the player grabs the object. |


Supporting components that **do not inherit from** *VRInteractable*:


| [ObjGunSlide](../../../api/templates/template_vr/objects/class.objgunslide.md) | Animates the slide mechanism of a firearm - configurable axis, range, and timing. |
|---|---|
| [VRSocketObject](../../../api/modules/vr/components/objects/class.vrsocketobject.md) | Defines a socket connection point with a specific ID and alignment transform. |
| [VRObjectPhysicalCable](../../../api/modules/vr/components/objects/class.vrobjectphysicalcable.md) | A physics-simulated cable built from rigid body segments. Connects two pluggable ends. |
| [Generator](../../../api/templates/template_vr/objects/class.generator.md) | Activates when both sockets are connected via a cable. Broadcasts a signal to connected receivers. |
| [ObjectPlatform](../../../api/modules/vr/components/objects/class.objectplatform.md) | A movable platform that tracks its velocity - used by [VRPlayerMotor](#class_vrplayermotor) to carry the player. |


These components also toggle nodes but **do not inherit from** *VRInteractable*:


| [NodeSwitchEnableByGesture](../../../api/templates/template_vr/global/class.nodeswitchenablebygesture.md) | Toggles nodes when a specific hand gesture is detected. |
|---|---|
| [NodeSwitchEnableByKey](../../../api/templates/template_vr/global/class.nodeswitchenablebykey.md) | Toggles nodes when a specific controller button is pressed. |


Visual feedback during interaction:


| [ObjectOutliner](../../../api/modules/vr/components/objects/class.objectoutliner.md) | Highlights interactable objects with an outline when your hand gets close. |
|---|---|
| [SocketOutliner](../../../api/modules/vr/components/objects/class.socketoutliner.md) | Highlights sockets when a compatible plug is nearby. |
| [Tooltip](../../../api/modules/vr/components/objects/tooltip/class.tooltip.md) | Shows floating text labels near objects during interaction. |
| [TooltipTextSwitcher](../../../api/templates/template_vr/objects/class.tooltiptextswitcher.md) | Switches tooltip text depending on the object's current state. |
| [ProgressObject](../../../api/modules/vr/components/objects/class.progressobject.md) | An interface for objects that report progress (0-1). Used by **Tooltip** to show a circular progress indicator. |


## Eye Tracking


If your headset supports eye tracking, you can use gaze-based object selection and labeling.


| [EyetrackingPointer](../../../api/templates/template_vr/global/class.eyetrackingpointer.md) | Calculates gaze direction and raycasts into the world to find what the player is looking at. |
|---|---|
| [ObjectLabeling](../../../api/templates/template_vr/global/class.objectlabeling.md) | Displays the name of the gazed object as a floating label that follows the gaze. |


Eye tracking is active only if supported by the hardware and both *[VREyeTracking::isAvailable()](../../../api/library/vr/class.vreyetracking_cpp.md#IsAvailable)* and *[VREyeTracking::isValid()](../../../api/library/vr/class.vreyetracking_cpp.md#IsValid)* return true.


## Object Attachment


Need something to follow the player - a menu on your wrist, a HUD in front of your eyes? These components handle it:


| [AttachToHand](../../../api/modules/vr/components/objects/class.attachtohand.md) | Locks a node to the player's hand. Choose left or right, set the offset, done. |
|---|---|
| [AttachToHead](../../../api/modules/vr/components/objects/class.attachtohead.md) | Locks a node to the headset so it follows your gaze. Optionally updates every frame. |


## MenuBaseUI Class


The base class for all in-world GUI menus.


> **Notice:** These components can only be attached to [GUI objects](../../../objects/objects/gui/index.md).


The following menu components inherit from *[MenuBaseUI](../../../api/modules/vr/components/objects/class.menubaseui.md)*:


| [HandSampleMenuGui](../../../api/templates/template_vr/gui/class.handmenusamplegui.md) | The menu attached to a controller (hand menu). |
|---|---|
| [WorldMenuSampleGui](../../../api/templates/template_vr/gui/class.worldmenusamplegui.md) | The menu placed in the world (world menu). |
| [MixedRealityMenuGui](../../../api/templates/template_vr/gui/class.mixedrealitymenugui.md) | The menu attached to the HMD showing Mixed Reality settings (if supported by your device). |


## Inventory System


The inventory is a spatial, grid-based storage that appears in front of you when activated. Throw objects into cells to store them, grab them back to retrieve.


| [VRInventory](../../../api/modules/vr/components/objects/class.vrinventory.md) | Generates the 3D inventory grid, manages item placement and removal, handles scaling and highlight animations on hover. |
|---|---|
| [VRInventoryItem](../../../api/modules/vr/components/objects/class.vrinventoryitem.md) | Defines how an item is positioned and oriented when placed inside the inventory. |


## VR Template Event System


A simple signal-slot system for connecting components. One component emits an event, others listen and react.


> **Notice:** See [Event Handling](../../../code/fundamentals/events/index_cpp.md) for more about events in UNIGINE.


| [EventSlot](../../../api/modules/vr/components/class.eventslot.md) | An event receiver - derived components implement a callback to respond to incoming events. |
|---|---|
| [EventSignal](../../../api/modules/vr/components/class.eventsignal.md) | An event emitter that broadcasts float, int, and string values to connected listeners. |
| [EventLinkOneToMany](../../../api/modules/vr/components/class.eventlinkonetomany.md) | Connects one signal to multiple slots - binds an emitter to a list of receivers. |


The following components react to events:


| [Lamp](../../../api/templates/template_vr/objects/class.lamp.md) | Toggles a light on or off in response to an incoming event signal. |
|---|---|
| [DoorTranslatable](../../../api/templates/template_vr/objects/class.doortranslatable.md) | Slides a door between open and closed positions in response to an event signal. |


Usage example: a **[Generator](#class_generator)** emits a signal when powered -> **EventLinkOneToMany** forwards it -> a **Lamp** lights up and a **DoorTranslatable** slides open.


## Framework


The framework layer includes the [Component System](../../../principles/component_system/index.md) plus a set of utilities for sound, math, and world management.


### Triggers Class


**[Triggers](../../../api/modules/vr/class.triggers.md)** marks room obstacles for the VR Player (walls, furniture, etc.) and warns you with increasing controller vibration as you get closer.


> **Notice:** Obstacles are not available for *[VRPlayerPC](#class_vrplayerpc)*.


Just create primitives for your room walls and objects and add them as children to the **Obstacles** dummy node (child of the ***VR*** node).


All children of the **Obstacles** node are automatically made invisible - they only serve as trigger volumes.


> **Notice:** Obstacle primitives must have their first surface (index 0) named *"box", "sphere", "capsule"* or *"cylinder"* to be properly converted into trigger volumes.


### Utils


A utility module with helper functions for 3D math, transforms, geometry, visualization, and world management.


### Sound Manager Class


**[SoundManager](../../../api/modules/vr/class.soundmanager.md)** handles audio playback - one-shot effects, looped ambient sounds, sound grouping for variety, and volume control.


| One-shot sounds | *playSound()* - positional, non-looping effects (impacts, clicks). |
|---|---|
| Looped sounds | *playLoopSound()* - continuous sounds that auto-stop after a set duration. |
| Sound grouping | *addSoundGroup()* - group similar sounds and randomize selection for variety. |
| Volume control | *setVolume()* - global volume with separate sound/music channels. |
| Sound warming | *warmAllSounds()* - preloads all groups to avoid playback delays. |


### MaskHolder Class


**[MaskHolder](../../../api/modules/vr/components/class.maskholder.md)** provides centralized access to physics collision and intersection masks used for teleportation, interaction, and grab detection.


### Lifetime


**[Lifetime](../../../api/templates/template_vr/global/class.lifetime.md)** auto-deletes its node after a set duration - used for temporary things like bullet decals and muzzle flash.


### TrajectoryMovement


**[TrajectoryMovement](../../../api/templates/template_vr/global/class.trajectorymovement.md)** moves objects along a parabolic arc - used for teleportation visualization and projectile paths.

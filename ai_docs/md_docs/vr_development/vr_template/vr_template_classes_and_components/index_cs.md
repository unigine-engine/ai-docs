# Classes and Components Overview (CS)


When you first open the VR Template project and see a lot of components, it can feel a bit overwhelming. Let's walk through the main parts so you know where everything lives. All VR components are assigned to nodes organized under the ***vr_layer*** root node:


![VR Template Structure (C#)](../../../learn/13_vr_app/vr_layer_cs_structure_with_captions.png)


## VRPlayer Component


The player is represented by a node hierarchy rooted at ***vr_player*** (a *Player Dummy* camera) with the ***[VRPlayer](../../../api/templates/template_vr_csharp/class.vrplayer.md)*** component assigned. Child nodes represent HMD and controller models, each with their own components for interactions and settings.


## InputSystem Component


***[InputSystem](../../../api/templates/template_vr_csharp/vr_input/class.inputsystem.md)*** is the central hub for all input. It manages available devices, input sources, and event handlers, supporting both VR and PC modes with automatic switching.


The actual input logic lives in specialized classes like ***[VRInput](../../../api/templates/template_vr_csharp/vr_input/class.vrinput.md)*** and ***[PCInput](../../../api/templates/template_vr_csharp/vr_input/class.pcinput.md)***, each handling head position, hand controllers, gestures, buttons, and actions like jump or crouch.


- **General Input Components**

  - ***[InputSystem](../../../api/templates/template_vr_csharp/vr_input/class.inputsystem.md)*** - coordinates input across all platforms.
  - ***[VRInput](../../../api/templates/template_vr_csharp/vr_input/class.vrinput.md)*** - VR-specific input: headset pose, controller tracking, button states.
- **VR Input Components** (active when *vr_input* is enabled)

  - ***[VRGeneralInput](../../../api/templates/template_vr_csharp/vr_input/class.vrgeneralinput.md)*** - general VR actions (movement, jump, fire, crouch) bound to controller buttons/axes.
  - ***[VRControllerInput](../../../api/templates/template_vr_csharp/vr_input/class.vrcontrollerinput.md)*** - per-hand controller input: button presses, touches, axis values.
  - ***[VRHandTrackingInput](../../../api/templates/template_vr_csharp/vr_input/class.vrhandtrackinginput.md)*** - hand tracking input with gesture recognition and per-finger tracking.
- **PC Input Components** (active when *pc_input* is enabled)

  - ***[PCInput](../../../api/templates/template_vr_csharp/vr_input/class.pcinput.md)*** - keyboard and mouse input.
  - ***[PCGeneralInput](../../../api/templates/template_vr_csharp/vr_input/class.pcgeneralinput.md)*** - maps keyboard/mouse to generalized actions for desktop mode.


## VRBaseController Component


Input devices are represented by components inherited from ***[HeadController](../../../api/templates/template_vr_csharp/controllers/class.headcontroller.md)*** (for HMDs) and ***[HandController](../../../api/templates/template_vr_csharp/controllers/class.handcontroller.md)*** (for controllers). They handle tracking and positioning, activating automatically based on the current input system.


- ***[VRBaseController](../../../api/templates/template_vr_csharp/base/class.vrbasecontroller.md)*** - base class for all control components.

  - ***[HeadController](../../../api/templates/template_vr_csharp/controllers/class.headcontroller.md)*** - updates head position.

    - ***[VRHeadController](../../../api/templates/template_vr_csharp/controllers/class.vrheadcontroller.md)*** - uses VR headset tracking data.
    - ***[PCHeadController](../../../api/templates/template_vr_csharp/controllers/class.pcheadcontroller.md)*** - desktop mode.
  - ***[HandController](../../../api/templates/template_vr_csharp/controllers/class.handcontroller.md)*** - updates hand position.

    - ***[VRHandController](../../../api/templates/template_vr_csharp/controllers/class.vrhandcontroller.md)*** - VR controller position and visuals.
    - ***[PCHandController](../../../api/templates/template_vr_csharp/controllers/class.pchandcontroller.md)*** - simulated hand for desktop input.
    - ***[VRHandTracking](../../../api/templates/template_vr_csharp/controllers/class.vrhandtracking.md)*** - hand bones and animations from tracking data.
  - ***[BasestationController](../../../api/templates/template_vr_csharp/controllers/class.basestationcontroller.md)*** - updates VR base station positions and displays their 3D models.

    - ***[VRBasestationController](../../../api/templates/template_vr_csharp/controllers/class.vrbasestationcontroller.md)*** - VR-specific base station tracking.


## VRMovementManager Component


***[VRMovementManager](../../../api/templates/template_vr_csharp/movements/class.vrmovementmanager.md)*** runs all active movement components each frame. Specific behaviors are built as separate components inheriting from ***[VRBaseMovement](../../../api/templates/template_vr_csharp/base/class.vrbasemovement.md)***:


- ***[WalkMovement](../../../api/templates/template_vr_csharp/movements/class.walkmovement.md)*** and ***[PCWalkMovement](../../../api/templates/template_vr_csharp/movements/class.pcwalkmovement.md)*** - moving through the world using controller sticks or keyboard.
- ***[TurnMovement](../../../api/templates/template_vr_csharp/movements/class.turnmovement.md)*** and ***[PCTurnMovement](../../../api/templates/template_vr_csharp/movements/class.pcturnmovement.md)*** - rotating using buttons or mouse.
- ***[TeleportationMovement](../../../api/templates/template_vr_csharp/movements/class.teleportationmovement.md)*** - instant relocation via teleport ray.
- ***[VRHandTrackingTeleportMovement](../../../api/templates/template_vr_csharp/movements/class.vrhandtrackingteleportmovement.md)*** - teleportation via hand gestures.
- ***[CrouchMovement](../../../api/templates/template_vr_csharp/movements/class.crouchmovement.md)*** - crouching on button press.


All movement components are modular - mix and match them in the Editor to build the locomotion scheme you need.


## VRInteractionManager Component


***[VRInteractionManager](../../../api/templates/template_vr_csharp/interactions/class.vrinteractionmanager.md)*** manages interactions between the player and scene objects - tracking hover, grab, and use states. Each interaction type is a separate component derived from ***[VRBaseInteraction](../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)***:


- ***[VRHandMenuInteraction](../../../api/templates/template_vr_csharp/interactions/class.vrhandmenuinteraction.md)*** - UI interaction via controller pointing ray.
- ***[VRHandTrackingMenuInteraction](../../../api/templates/template_vr_csharp/interactions/class.vrhandtrackingmenuinteraction.md)*** - UI interaction via hand tracking gestures.
- ***[VRHandShapeInteraction](../../../api/templates/template_vr_csharp/interactions/class.vrhandshapeinteraction.md)*** - grabbing, using, and hovering over physical objects via a trigger shape.
- ***[VRPCHeadMenuInteraction](../../../api/templates/template_vr_csharp/interactions/class.vrpcheadmenuinteraction.md)*** - menu interaction in desktop mode using mouse.


They're enabled automatically depending on device availability.


## VRBaseInteractable Component


***[VRBaseInteractable](../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)*** is the base for all interactive objects - it defines what a player can do with them. You can also [create your own interactable types](../../../vr_development/vr_template/vr_template_new_interactable/index_cs.md).


The following components inherit from ***VRBaseInteractable***:


| [VRTransformMovableObject](../../../api/templates/template_vr_csharp/interactions/class.vrtransformmovableobject.md) | Objects you can grab, hold, and throw - transform-based movement (no physics). |
|---|---|
| [VRKinematicMovableObject](../../../api/templates/template_vr_csharp/interactions/class.vrkinematicmovableobject.md) | Objects you can grab, hold, and throw - kinematic physics. |
| [VRPhysicMovableObject](../../../api/templates/template_vr_csharp/interactions/class.vrphysicmovableobject.md) | Objects with rigid bodies that you can grab, hold, and throw - full physics simulation. |
| [VRObjectHandle](../../../api/templates/template_vr_csharp/transformations/class.vrobjecthandle.md) | Handles, levers, valves - things you can turn or move while holding. |
| [VRObjectHandleTranslatable](../../../api/templates/template_vr_csharp/interactions/class.vrobjecthandletranslatable.md) | Handles that slide along a limited linear path. Supports toggle animation and sound feedback. |
| [VRObjectHandleRotatable](../../../api/templates/template_vr_csharp/interactions/class.vrobjecthandlerotatable.md) | Handles that rotate around a specified axis. |
| [VRObjectSwitch](../../../api/templates/template_vr_csharp/transformations/class.vrobjectswitch.md) | Buttons and switches - toggled by grabbing. Works with ***VRNodeSwitchEnableByGrab*** for additional effects. |
| [VRNodeSwitchEnableByGrab](../../../api/templates/template_vr_csharp/interactions/class.vrnodeswitchenablebygrab.md) | Toggles one or more nodes on/off when grabbed. |
| [VRNodeSwitchEnableByKey](../../../api/templates/template_vr_csharp/interactions/class.vrnodeswitchenablebykey.md) | Toggles nodes by pressing a button while holding the object. Works in both VR and PC modes. |
| [VRLaserPointer](../../../api/templates/template_vr_csharp/interactions/class.vrlaserpointer.md) | Casts a laser ray. The laser pointer node has both ***VRTransformMovableObject*** and ***VRLaserPointer*** assigned. |
| [VRGun](../../../api/templates/template_vr_csharp/interactions/class.vrgun.md) | A firearm you can grab, hold, and shoot - with sound/visual effects and **VRGunSlide** for slide animation. |
| [VRPluggable](../../../api/templates/template_vr_csharp/interactions/class.vrpluggable.md) | An object that auto-attaches to a matching **VRSocketObject** when released nearby. |
| [VRSelectionTest](../../../api/templates/template_vr_csharp/interactions/class.vrselectiontest.md) | Shows a visual outline on hover/grab - useful for debugging interaction feedback. |


Additional supporting components:


| [VRObjectPlatform](../../../api/templates/template_vr_csharp/interactions/class.vrobjectplatform.md) | A movable platform that carries the player when they stand on it. |
|---|---|
| [VRGunSlide](../../../api/templates/template_vr_csharp/interactions/class.vrgunslide.md) | Animates a firearm's slide mechanism. |
| [VRSocketObject](../../../api/templates/template_vr_csharp/interactions/class.vrsocketobject.md) | Defines a socket connection point for pluggable objects. |
| [VRObjectPhysicalCable](../../../api/templates/template_vr_csharp/interactions/class.vrobjectphysicalcable.md) | A physics-simulated cable connecting two pluggable ends. |
| [Generator](../../../api/templates/template_vr_csharp/interactions/class.generator.md) | Activates when both sockets are connected. Broadcasts a signal to receivers. |


## Inventory System


A spatial, grid-based storage that appears in front of you. Throw objects in, grab them out.


| [VRInventory](../../../api/templates/template_vr_csharp/interactions/class.vrinventory.md) | The grid itself - handles item placement, removal, scaling, and highlight animations. |
|---|---|
| [VRInventoryItem](../../../api/templates/template_vr_csharp/interactions/class.vrinventoryitem.md) | Defines how an item is positioned when placed in the grid. |


## GUI Classes


In-world menu components, all inheriting from ***[VRBaseUI](../../../api/templates/template_vr_csharp/base/class.vrbaseui.md)***:


| [VRMenuSample](../../../api/templates/template_vr_csharp/ui/class.vrmenusample.md) | A sample menu showing basic widget creation and button interaction. |
|---|---|
| [VRMenuSettings](../../../api/templates/template_vr_csharp/ui/class.vrmenusettings.md) | A settings menu for toggling between smooth and step rotation. |


## Object Attachment


Need something to follow the player - a menu on your wrist, a HUD in front of your eyes?


| [VRAttachToHand](../../../api/templates/template_vr_csharp/transformations/class.vrattachtohand.md) | Locks a node to the player's hand. Choose left or right, set the offset. |
|---|---|
| [VRAttachToHead](../../../api/templates/template_vr_csharp/transformations/class.vrattachtohead.md) | Locks a node to the headset so it follows your gaze. |


## Signal System


A one-to-many event system for connecting powered devices:


| [SignalEmitter](../../../api/templates/template_vr_csharp/utils/class.signalemitter.md) | Broadcasts float, int, and string values to connected listeners. |
|---|---|
| **ISignalSlot** | An interface for event receivers. Implement *ReceiveFloat*, *ReceiveInt*, and *ReceiveString* callbacks to respond to signals (see **Lamp**, **DoorTranslatable**). |
| [SignalLinkOneToMany](../../../api/templates/template_vr_csharp/utils/class.signallinkonetomany.md) | Connects one emitter to multiple slots. |


The following components react to signals (implement **ISignalSlot**):


| [Lamp](../../../api/templates/template_vr_csharp/utils/class.lamp.md) | Toggles a light on or off in response to an incoming signal. |
|---|---|
| [DoorTranslatable](../../../api/templates/template_vr_csharp/utils/class.doortranslatable.md) | Slides a door between open and closed positions in response to a signal. |


Example: a **Generator** emits a signal -> **SignalLinkOneToMany** forwards it -> a **Lamp** lights up and a **DoorTranslatable** slides open.


## Visual Feedback


Visual feedback during interaction:


| [ObjectOutliner](../../../api/templates/template_vr_csharp/interactions/class.objectoutliner.md) | Highlights objects with an outline when your hand gets close. |
|---|---|
| [VRSocketOutliner](../../../api/templates/template_vr_csharp/interactions/class.vrsocketoutliner.md) | Highlights sockets when a compatible plug is nearby. |
| [VRTooltip](../../../api/templates/template_vr_csharp/ui/class.vrtooltip.md) | Floating text labels near objects during interaction. |
| [TooltipTextSwitcher](../../../api/templates/template_vr_csharp/ui/class.tooltiptextswitcher.md) | Switches tooltip text based on the current input mode. |


## Framework


The framework layer includes the [Component System](../../../principles/component_system/index.md) and utility classes.


### PlayerMotor


**[PlayerMotor](../../../api/templates/template_vr_csharp/movements/class.playermotor.md)** - physics-based locomotion: movement, collisions, crouching, jumping, stepping over obstacles, slopes, and moving platforms.


### Triggers


**[Triggers](../../../api/modules/vr/class.triggers.md)** - marks room obstacles and warns the player with haptic feedback as they get closer.


### HeadCollision


**[HeadCollision](../../../api/templates/template_vr_csharp/movements/class.headcollision.md)** - detects real-room obstacles near the player's head with visual and haptic warnings.


### MaskHolder


**[MaskHolder](../../../api/templates/template_vr_csharp/utils/class.maskholder.md)** - centralized access to physics masks for teleportation, interaction, and grab detection.


### SoundManager


**[SoundManager](../../../api/templates/template_vr_csharp/utils/class.soundmanager.md)** - audio playback: one-shot effects, looped sounds, grouping, and volume control.


### Lifetime


**[Lifetime](../../../api/templates/template_vr_csharp/utils/class.lifetime.md)** - auto-deletes its node after a set duration.


### TrajectoryMovement


**[TrajectoryMovement](../../../api/templates/template_vr_csharp/utils/class.trajectorymovement.md)** - moves objects along a parabolic arc for teleport visualization.


### Utils


Helper functions for 3D math, transforms, geometry, visualization, and world management.

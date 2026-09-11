# VR Player Controls (CS)


The VR Template comes with two player controllers - one for VR headsets and one for desktop - both with movement and interaction working out of the box. Let's see what they can do.


## Available Players


The VR Template supports two types of player controllers:


- **PC Player** - for standard desktop gameplay using a keyboard, mouse, or gamepad.
- **VR Player** - for immersive virtual reality using VR controllers or hand tracking.


The engine detects your hardware at startup: if a VR headset is connected, you get the VR Player; if not, the PC Player kicks in. The *[InputSystem](../../../api/templates/template_vr_csharp/vr_input/class.inputsystem.md)* component handles this automatically - it detects whether a headset is connected and selects the right input preset.


### VR Player


The VR Player uses a physical motor (*[PlayerMotor](../../../api/templates/template_vr_csharp/movements/class.playermotor.md)*) that tracks your real-world head and hand positions. It handles collisions, slopes, and auto-stepping on stairs so you can move naturally through the environment.


Input is handled by VR controllers or hand tracking - the system switches between them automatically at runtime.


> **Notice:** Hand tracking requires **OpenXR** or **Varjo SDK with Ultraleap plugin**.


Movement is handled with the thumbsticks: the **left stick** moves you through the world, while the **right stick** rotates your view - handy when you need to turn around without physically spinning. Two rotation modes are available: **smooth** (continuous) and **step** (snap turning in fixed-angle increments).


Beyond locomotion, the VR Player lets you:


- **Teleport** - point and jump to a target spot (works with both controllers and hand tracking).
- **Grab objects** - pick things up with the grip button or a grab gesture.
- **Use objects** - interact with what you're holding (pull a trigger, press a button) via the trigger or a hand gesture.
- **Open menus** - bring up an in-world hand menu or inventory.


> **Notice:** All bindings are configurable through the *[VRControllerInput](../../../api/templates/template_vr_csharp/vr_input/class.vrcontrollerinput.md)* and *[VRHandTrackingInput](../../../api/templates/template_vr_csharp/vr_input/class.vrhandtrackinginput.md)* components.


#### Teleportation


Your real-world play area is limited, but virtual worlds aren't - that's where teleportation comes in. Point at a spot and jump there instantly, with no motion sickness involved. It works with both controllers and hand tracking.


##### Restricting Teleportation


By default, it is possible to teleport to any point on the scene. To avoid user interaction errors in VR (e.g., teleporting into walls or ceilings), you can restrict teleportation to certain areas.


The VR Template uses the *[MaskHolder](../../../api/templates/template_vr_csharp/utils/class.maskholder.md)* component to manage teleportation behavior. This component must be present in the world and provides two key masks:


- **Ray Intersection Mask** (*RayIntersectionMask*) - determines which surfaces the teleport ray can detect. Surfaces matching this mask will be considered as potential landing points.
- **Teleport Allowed Mask** (*TeleportAllowedMask*) - determines which of the detected surfaces allow teleportation. If a surface is detected by the ray but doesn't match this mask, teleportation will be forbidden (indicated by a red marker).


![MaskHolder Component (C#)](../../../learn/13_vr_app/mask_holder_cs.png)


To restrict teleportation to specific areas:


1. Create a mesh defining the allowed teleportation area.
2. Set an *[intersection mask](../../../principles/bit_masking/index.md#intersection_mask)* on the mesh surface(s) that matches both masks in **MaskHolder**.
3. For surfaces where teleportation should be forbidden (e.g., walls, ceilings), set an intersection mask that matches only *RayIntersectionMask* but not *TeleportAllowedMask*. The teleport ray will detect these surfaces but display a forbidden marker.


> **Notice:** Multiple meshes can be used to define teleportation areas.


> **Notice:** In most cases, *RayIntersectionMask* should match all physical surfaces so the ray can detect walls and ceilings (displaying a forbidden marker). Surfaces not matching this mask will be invisible to the teleport ray - useful for decorative objects or trigger zones that shouldn't affect teleportation.


For more details on VR input handling, see the [VR Input](../../../vr_development/vr_input_cs.md) article.


### PC Player


No headset? No problem. The PC Player is a standard first-person controller for desktop testing. It uses the same *[VRPlayer](../../../api/templates/template_vr_csharp/class.vrplayer.md)* component with a PC input preset (*[PCInput](../../../api/templates/template_vr_csharp/vr_input/class.pcinput.md)* / *[PCGeneralInput](../../../api/templates/template_vr_csharp/vr_input/class.pcgeneralinput.md)*), supporting keyboard and mouse controls - movement, looking around, jumping, and crouching.


Interaction works the same as in VR: the PC Player projects a ray from the camera (*[PCHandController](../../../api/templates/template_vr_csharp/controllers/class.pchandcontroller.md)*) that lets you grab and use objects with the mouse. All scene objects behave identically regardless of the input method.

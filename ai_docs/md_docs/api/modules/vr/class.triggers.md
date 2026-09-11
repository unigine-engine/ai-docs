# Triggers Class


Triggers is a utility class for managing volumetric trigger zones in VR. It supports multiple primitive shapes (box, sphere, capsule, cylinder) and provides methods to check if a point is inside any trigger volume and calculate penetration depth.


Trigger shapes are determined by the surface name of the object: box, sphere, capsule, or cylinder. When initialized, the class disables collision, intersection, and shadow casting on all trigger objects.


### Usage in VRPlayerVR


In [VRPlayerVR](../../../api/modules/vr/components/players/class.vrplayervr.md), Triggers are used as obstacles to prevent the player's head from passing through geometry. The *vr_obstacles* parameter in [VRPlayerSpawner](../../../api/modules/vr/components/class.vrplayerspawner.md) specifies the root node containing trigger volumes.


When the player's head enters a trigger volume, the following effects occur:

 **Fade-to-black** � screen darkens proportionally to penetration depth **Controller vibration** � both controllers vibrate continuously while inside the trigger **Teleport back** � if the player remains inside longer than *black_screen_max_sec*, they are teleported to the last safe position
### Setup


To create obstacle triggers:

 Create a container node (e.g., NodeDummy) Add child objects with primitive meshes (Box, Sphere, etc.) Name the first surface of each object according to its shape: box, sphere, capsule, or cylinder Position and scale the objects to match your scene geometry (walls, furniture, etc.) Assign the container node to the *vr_obstacles* parameter in VRPlayerSpawner
> **Notice:** Triggers only work in VR mode (VRPlayerVR). They have no effect in PC mode (VRPlayerPC).


### See Also


- **[TriggerInfo](../../../api/modules//.md)**
- **[VRPlayerVR](../../../api/modules/vr/components/players/class.vrplayervr.md)**


## struct TriggerInfo

Structure containing trigger node reference and its shape type.
## Triggers Class

---

## void init ( )

Initializes the trigger system from a root node. Recursively searches all children (including NodeReference contents) for objects with surface names matching trigger types. Disables collision, intersection, and shadow casting on found triggers.
### Arguments

## void addTrigger ( )

Adds a single node as a trigger. The trigger type is determined by the first surface name: box, sphere, capsule, or cylinder. Disables collision, intersection, and shadows on the object.
### Arguments

## isInside ( )

Checks if a world position is inside any registered trigger volume. Also calculates penetration depth accessible via getDepth().
### Arguments

### Return value

true if the position is inside any trigger volume, false otherwise.
## getDepth ( )

Returns the maximum penetration depth calculated during the last isInside() call. Represents the distance from the test point to the nearest trigger surface.
### Return value

Penetration depth from the last isInside() call.
## void renderVisualizer ( )

Renders debug visualization of all trigger volumes using green wireframe boxes. Enables the Visualizer system and draws bounding boxes for each registered trigger.

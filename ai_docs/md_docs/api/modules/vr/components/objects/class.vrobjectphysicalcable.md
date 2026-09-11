# VRObjectPhysicalCable Component

**Inherits from:** ComponentBase


VRObjectPhysicalCable creates a physics-based cable between two points. The cable is rendered as a dynamic mesh and simulates physical behavior including gravity and tension.


Each end of the cable can have a **[VRPluggable](../../../../../api/modules/vr/components/objects/class.vrpluggable.md)** component for connecting to sockets. The cable automatically updates its shape based on the positions of its endpoints.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Cable Endpoints |  |  |
| cable_start | *Node* | Start point of the cable. |
| cable_end | *Node* | End point of the cable. |
| Appearance |  |  |
| material | *Material* | Material applied to the cable mesh. |
| cable_radius | *Float* | Radius of the cable. Default: 0.0125. |
| slices | *Int* | Number of radial slices. Default: 16. |
| subdivisions | *Int* | Number of length subdivisions. Default: 16. |
| Physics |  |  |
| are_ends_fixed | *Toggle* | Whether cable ends are fixed in place. |
| num_segments | *Int* | Number of physics segments. Default: 5. |
| collision_mask | *Mask* | Collision mask for cable segments. |
| Physics Settings |  |  |
| max_impulse | *Float* | Limit applied impulse for better stretched cable mesh generation. Default: 10.0. |
| segment_length | *Float* | Length of each physics segment. Default: 0.25. |
| sphere_mass | *Float* | Mass of each physics sphere. Default: 0.1. |
| sphere_radius | *Float* | Radius of each physics sphere. Default: 0.0125. |
| Socket IDs |  |  |
| socket_id_for_plugs | *Int* | Socket ID for plug connections. Default: 1. |
| socket_id_for_cable_segments | *Int* | Socket ID for cable segment connections. Default: 2. |


### See Also


- **[VRPluggable](../../../../../api/modules/vr/components/objects/class.vrpluggable.md)**
- **[VRSocketObject](../../../../../api/modules/vr/components/objects/class.vrsocketobject.md)**


## VRObjectPhysicalCable Class

---

## getFirstPlug ( )

Returns the pluggable component at the first end of the cable.
### Return value

First plug component.
## getSecondPlug ( )

Returns the pluggable component at the second end of the cable.
### Return value

Second plug component.

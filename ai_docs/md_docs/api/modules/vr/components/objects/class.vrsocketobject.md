# VRSocketObject Component

**Inherits from:** ComponentBase


VRSocketObject defines a connection point for **[VRPluggable](../../../../../api/modules/vr/components/objects/class.vrpluggable.md)** objects. When a pluggable object is released near this socket and has a matching socket ID, it snaps to the socket's transform.


Use sockets to create plug/outlet systems, docking points, or any connection mechanism where objects need to attach at specific locations.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Socket ID | *Int* | Unique ID that pluggable objects must match (*default: -1*). |
| Plugged Transform Node | *Node* | Node defining the transform for plugged objects. |


### See Also


- **[VRPluggable](../../../../../api/modules/vr/components/objects/class.vrpluggable.md)**


## VRSocketObject Class

---

## getPluggedWorldTransform ( )

Returns the world transform where plugged objects should be positioned.
### Return value

World transform for plugged objects.
## getID ( )

Returns the socket's ID for matching with pluggable objects.
### Return value

Socket ID.

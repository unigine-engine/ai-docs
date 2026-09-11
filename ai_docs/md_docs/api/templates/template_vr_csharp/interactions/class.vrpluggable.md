# VRPluggable Component

**Inherits from:** VRBaseInteractable


VRPluggable extends **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** to implement an object that can be plugged into compatible **[VRSocketObject](../../../../api/templates/template_vr_csharp/interactions/class.vrsocketobject.md)** sockets. Compatible socket IDs can be configured and modified at runtime.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Init Socket IDs | *int[]* | Initial array of compatible socket IDs. |


### See Also


- **[VRSocketObject](../../../../api/templates/template_vr_csharp/interactions/class.vrsocketobject.md)**
- **[VRSocketOutliner](../../../../api/templates/template_vr_csharp/interactions/class.vrsocketoutliner.md)**
- **[VRObjectPhysicalCable](../../../../api/templates/template_vr_csharp/interactions/class.vrobjectphysicalcable.md)**


## VRPluggable Class

---

## void AddSocketId ( )

Adds a compatible socket ID to this plug.
### Arguments

## RemoveSocketId ( )

Removes a compatible socket ID from this plug.
### Arguments

### Return value

True if the ID was found and removed.
## void ConnectToSocket ( )

Connects this plug to the specified socket.
### Arguments

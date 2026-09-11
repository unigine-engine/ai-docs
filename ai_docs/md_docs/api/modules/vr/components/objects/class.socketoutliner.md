# SocketOutliner Component

**Inherits from:** ComponentBase


SocketOutliner is a singleton component that manages outline rendering for socket objects in VR. It provides visual feedback by highlighting sockets when pluggable objects are nearby or can be connected.


The component tracks all **[VRSocketObject](../../../../../api/modules/vr/components/objects/class.vrsocketobject.md)** instances and allows individual sockets to be outlined with custom colors.


### See Also


- **[ObjectOutliner](../../../../../api/modules/vr/components/objects/class.objectoutliner.md)**
- **[VRSocketObject](../../../../../api/modules/vr/components/objects/class.vrsocketobject.md)**
- **[VRPluggable](../../../../../api/modules/vr/components/objects/class.vrpluggable.md)**


## SocketOutliner Class

---

## static get ( )

Returns the singleton instance of SocketOutliner.
### Return value

Singleton instance.
## void enableOutlineForSocket ( )

Enables outline rendering for the specified socket with the given color.
### Arguments

## void disableOutlineForSocket ( )

Disables outline rendering for the specified socket.
### Arguments

# VRPluggable Component

**Inherits from:** ComponentBase, VRInteractable


VRPluggable makes an object connectable to **[VRSocketObject](../../../../../api/modules/vr/components/objects/class.vrsocketobject.md)** sockets. When released near a compatible socket, the object snaps into position. When grabbed again, it disconnects from the socket.


Objects can specify which socket IDs they are compatible with. This allows creating plug/cable systems where specific plugs only fit specific sockets.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Init Socket IDs | *Array of Int* | Socket IDs this object can connect to. |


### See Also


- **[VRSocketObject](../../../../../api/modules/vr/components/objects/class.vrsocketobject.md)**


## VRPluggable Class

---

## getSocketNode ( )

Returns the node of the currently connected socket.
### Return value

Connected socket node or nullptr.
## getConnectedSocketID ( )

Returns the ID of the currently connected socket.
### Return value

Socket ID or -1 if not connected.
## isConnected ( )

Returns whether the object is connected to a socket.
### Return value

True if connected.
## getConnectedSocketNode ( )

Returns the node of the currently connected socket.
### Return value

Connected socket node or nullptr.
## getSocket ( )

Returns the VRSocketObject component of the currently connected socket.
### Return value

Connected socket component or nullptr.
## void addSocketId ( )

Adds a compatible socket ID at runtime.
### Arguments

## void connectToSocket ( )

Programmatically connects to a socket.
### Arguments

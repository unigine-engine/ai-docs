# VRInteractable Class


VRInteractable is an interface for objects that can be interacted with by the **VR** player. Components implementing this interface receive callbacks when the player grabs, holds, uses, or throws the object.


Implement this interface on any component that needs to respond to **VR** hand interactions. The **[VRPlayer](../../../../api/modules/vr/components/players/class.vrplayer.md)** system automatically detects VRInteractable components on grabbed nodes and invokes the appropriate methods.


### See Also


- **[ObjMovable](../../../../api/modules/vr/components/objects/class.objmovable.md)**
- **[ObjSwitch](../../../../api/modules/vr/components/objects/class.objswitch.md)**
- **[ObjHandle](../../../../api/modules/vr/components/objects/class.objhandle.md)**


## VRInteractable Class

---

## void grabIt ( )

Called when the player grabs this object.
### Arguments

## void holdIt ( )

Called every frame while the player holds this object.
### Arguments

## void useIt ( )

Called when the player activates the use action while holding this object.
### Arguments

## void throwIt ( )

Called when the player releases this object.
### Arguments

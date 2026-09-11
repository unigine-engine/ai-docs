# ObjMovable Component

**Inherits from:** ComponentBase, VRInteractable


ObjMovable makes an object grabbable and throwable by the **VR** player. When grabbed, the object follows the hand. When released, physics takes over and the object is thrown with the hand's velocity.


The component supports "handy" positions for proper grip alignment, physics-based throwing, impact/slide sounds, and optional attachment to the player's head (for hat-like objects).


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Physics Group |  |  |
| Use Physics | *Toggle* | Enable physics simulation when thrown. |
| Mass List | *Switch* | Object mass preset selection. |
| Grip Group |  |  |
| Use Handy Pos | *Toggle* | Snap to predefined grip position when grabbed. |
| Handy Pos | *Vec3* | Grip position offset for PC mode. |
| Handy Rot Euler | *Vec3* | Grip rotation offset (euler angles) for PC mode. |
| Handy Pos VR | *Vec3* | Grip position offset for VR mode. |
| Handy Rot Euler VR | *Vec3* | Grip rotation offset (euler angles) for VR mode. |
| Can Attach To Head | *Toggle* | Allow attaching to player's head. |
| Hat Def Pos | *Vec3* | Position offset when attached to the player's head. |
| Hat Def Rot Euler | *Vec3* | Rotation offset (euler angles) when attached to the player's head. |
| Sound Group |  |  |
| Use Sounds | *Toggle* | Enable impact and slide sounds. |
| Impact Sound File | *File* | Sound played on collision. |
| Impact Min Dist | *Float* | Minimum audible distance for impact sounds. Default: *0.2*. |
| Impact Max Dist | *Float* | Maximum audible distance for impact sounds. Default: *1000.0*. |
| Slide Sound File | *File* | Looping sound during sliding. |
| Slide Min Dist | *Float* | Minimum audible distance for slide sounds. Default: *0.2*. |
| Slide Max Dist | *Float* | Maximum audible distance for slide sounds. Default: *1000.0*. |


### See Also


- **[VRInteractable](../../../../../api/modules/vr/components/class.vrinteractable.md)**


## ObjMovable Class

---

## getBody ( )

Returns the rigid body used for physics simulation.
### Return value

Physics body.
## void freeze ( )

Freezes the physics body, stopping all movement.
## void unfreeze ( )

Unfreezes the physics body, allowing movement.
## getLocalNodeTransform ( )

Returns the local transformation of the node when held by a hand.
### Return value

Local transform when held.
## void setLocalNodeTransform ( )

Sets the local transformation of the node when held.
### Arguments

## void restoreMass ( )

Restores the original mass of all physics shapes.

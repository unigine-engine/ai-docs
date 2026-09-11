# VRPlayerSpawner Component

**Inherits from:** ComponentBase


VRPlayerSpawner automatically creates the appropriate **[VRPlayer](../../../../api/modules/vr/components/players/class.vrplayer.md)** type based on available hardware. If a **VR** headset is detected, it spawns a **[VRPlayerVR](../../../../api/modules/vr/components/players/class.vrplayervr.md)**; otherwise it creates a **[VRPlayerPC](../../../../api/modules/vr/components/players/class.vrplayerpc.md)** for desktop play.


Add this component to a node where you want the player to spawn. The component configures rotation, movement, and obstacle settings based on the parameter values.


### Node Attachment


The component can be attached to any node. The spawned player inherits the world transform (position and rotation) of the source node.


If the component is attached to a **Player** node (such as **PlayerDummy** or **PlayerActor**), the following parameters are additionally copied to the spawned player:


- **FOV** � field of view
- **ZNear** � near clipping plane
- **ZFar** � far clipping plane
- **Scriptable Materials** � all scriptable materials assigned to the player


For full control over camera settings, it is recommended to attach the component to a **Player** node.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| VR |  |  |
| VR Obstacles | *Node* | Container node for room boundary triggers. Initially disabled on spawn; managed by **[VRPlayerVR](../../../../api/modules/vr/components/players/class.vrplayervr.md)** at runtime. |
| VR Controllers Node | *Node* | Parent node containing VR controllers. |
| Rotation Type | *Switch* | Player rotation mode: Discrete Step or Smooth. Default: *Discrete Step*. |
| Angle Per Step | *Float* | Rotation angle per discrete step in degrees. Visible when Rotation Type is set to Discrete Step. Default: *75.0*. |
| Smooth Rotation Speed | *Float* | Rotation speed in degrees per second for smooth rotation mode. Visible when Rotation Type is set to Smooth. Default: *60.0*. |
| PC |  |  |
| Move Speed | *Float* | PC player movement speed. Default: *2.5*. |
| Acceleration | *Float* | PC player acceleration. Default: *8.0*. |
| Damping | *Float* | PC player movement damping. Default: *8.0*. |
| Hand Length | *Float* | Maximum distance for grabbing objects. Default: *1.3*. |
| Throw Force | *Float* | Initial velocity applied to thrown objects. Default: *7.0*. |


### See Also


- **[VRPlayer](../../../../api/modules/vr/components/players/class.vrplayer.md)**
- **[VRPlayerVR](../../../../api/modules/vr/components/players/class.vrplayervr.md)**
- **[VRPlayerPC](../../../../api/modules/vr/components/players/class.vrplayerpc.md)**


## VRPlayerSpawner Class

---

## getSpawnedPlayer ( )

Returns the VRPlayer component that was spawned.
### Return value

Spawned player component.

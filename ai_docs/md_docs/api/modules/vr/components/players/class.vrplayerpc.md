# VRPlayerPC Component

**Inherits from:** VRPlayer


VRPlayerPC implements **[VRPlayer](../../../../../api/modules/vr/components/players/class.vrplayer.md)** for keyboard/mouse desktop interaction. It provides first-person controls with **WASD** movement, mouse look, and left-click object grabbing.


The player uses a **PlayerActor** for physics-based movement with acceleration and damping. Objects can be grabbed with left mouse click and thrown with configurable force.


> **Notice:** This component is created automatically at runtime by **[VRPlayerSpawner](../../../../../api/modules/vr/components/class.vrplayerspawner.md)** when no VR headset is detected. You should not add this component manually in the editor. All component parameters are configured through VRPlayerSpawner properties.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Move Speed | *Float* | Maximum movement speed in m/s (*default: 2.5*). |
| Acceleration | *Float* | How quickly the player reaches full speed (*default: 8.0*). |
| Damping | *Float* | How quickly the player stops (*default: 8.0*). |
| Hand Length | *Float* | Maximum grab distance in meters (*default: 1.3*). |
| Throw Force | *Float* | Initial velocity when throwing objects in m/s (*default: 7.0*). |


### See Also


- **[VRPlayer](../../../../../api/modules/vr/components/players/class.vrplayer.md)**


## VRPlayerPC Class

---

## getActor ( )

Returns the underlying PlayerActor for physics movement.
### Return value

Actor player.
## void setEnabled ( )

Enables or disables player controls.
### Arguments

## void setGrabNode ( )

Programmatically grabs a node with the player's hand.
### Arguments

## static isGamepadLastControl ( )

Returns whether the gamepad was the most recently used input device.
### Return value

Non-zero if gamepad was the last used input.
## static void setLastControl ( )

Sets which input device was last used.
### Arguments

# PlayerTeleporter Class


PlayerTeleporter is an abstract base class for teleportation systems in VR. It provides the core functionality for ray-based teleportation including target validation, visual feedback, and teleport execution.


Subclasses such as **[PlayerHandControllerTeleporter](../../../../../api/modules/vr/components/players/class.playerhandcontrollerteleporter.md)** and **[PlayerHandTrackingTeleporter](../../../../../api/modules/vr/components/players/class.playerhandtrackingteleporter.md)** implement input-specific teleportation logic.


### See Also


- **[PlayerHandControllerTeleporter](../../../../../api/modules/vr/components/players/class.playerhandcontrollerteleporter.md)**
- **[PlayerHandTrackingTeleporter](../../../../../api/modules/vr/components/players/class.playerhandtrackingteleporter.md)**
- **[VRPlayer](../../../../../api/modules/vr/components/players/class.vrplayer.md)**


## PlayerTeleporter Class

---

## void init ( )

Initializes the teleporter. Called once during setup.
## void update ( )

Updates the teleporter state based on controller input.
### Arguments

## wantTeleport ( )

Returns whether a teleport action has been requested.
### Return value

True if teleport is requested.
## getTeleportPosition ( )

Returns the target position for teleportation.
### Return value

Target teleport position.
## void setEnabled ( )

Enables or disables the teleportation system.
### Arguments

## void setTeleportAllowedMarkerNode ( )

Sets the visual marker node displayed at valid teleport locations.
### Arguments

## void setTeleportForbiddenMarkerNode ( )

Sets the visual marker node displayed at invalid teleport locations.
### Arguments

## void setTeleportationMask ( )

Sets the surface mask that defines which surfaces allow teleportation.
### Arguments

## void setRayIntersectionMask ( )

Sets the mask for ray intersection testing.
### Arguments

## void setAllowedRayMaterial ( )

Sets the material used for the teleport ray when targeting a valid location.
### Arguments

## void setForbiddenRayMaterial ( )

Sets the material used for the teleport ray when targeting an invalid location.
### Arguments

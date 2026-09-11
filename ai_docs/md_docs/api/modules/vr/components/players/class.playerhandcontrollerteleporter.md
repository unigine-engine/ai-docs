# PlayerHandControllerTeleporter Class

**Inherits from:** PlayerTeleporter


PlayerHandControllerTeleporter implements teleportation for VR hand controllers. It extends **[PlayerTeleporter](../../../../../api/modules/vr/components/players/class.playerteleporter.md)** to handle controller-specific input such as thumbstick/trackpad activation.


The teleporter uses the controller's pointing direction to cast a ray and find valid teleport destinations. It is automatically integrated with **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)**.


### See Also


- **[PlayerTeleporter](../../../../../api/modules/vr/components/players/class.playerteleporter.md)**
- **[PlayerHandTrackingTeleporter](../../../../../api/modules/vr/components/players/class.playerhandtrackingteleporter.md)**
- **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)**


## PlayerHandControllerTeleporter Class

---

## void init ( )

Initializes the controller teleporter.
